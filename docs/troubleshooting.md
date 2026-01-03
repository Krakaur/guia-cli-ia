---
layout: page
title: Troubleshooting - Casos Reales Documentados
description: Soluciones a problemas comunes en CLIs de IA - encoding UTF-8, timeouts, JSON parsing, procesos huérfanos
keywords: troubleshooting ia cli, deepseek encoding error, gemini timeout, json parsing
permalink: /troubleshooting/
---

# Troubleshooting: Casos Reales Documentados

Esta guía contiene soluciones a problemas **reales** encontrados durante meses de uso intensivo de CLIs de IA en investigación académica y desarrollo de sistemas multi-agente.

---

## 📋 Tabla de Contenidos

- [Problemas de Encoding](#problemas-de-encoding)
- [Timeouts y Latencia](#timeouts-y-latencia)
- [Parsing de JSON](#parsing-de-json)
- [Limitaciones de PowerShell](#limitaciones-de-powershell)
- [Procesos Huérfanos](#procesos-huérfanos)
- [Modelos y Autenticación](#modelos-y-autenticación)

---

## 🔤 Problemas de Encoding

### Caso 1: DeepSeek crash con emojis (Windows)

**Síntoma:**
```
UnicodeEncodeError: 'charmap' codec can't encode character '\U0001f680'
```

**Contexto:** DeepSeek genera emojis en respuesta, PowerShell crashea.

**Solución permanente:**
```powershell
[Environment]::SetEnvironmentVariable("PYTHONIOENCODING", "utf-8", "User")
```

**Solución temporal:**
```powershell
$env:PYTHONIOENCODING="utf-8"; deepseek -q "prompt" -r
```

**Lección:** En Windows, SIEMPRE configurar encoding UTF-8 para CLIs Python.

---

### Caso 2: Acentos españoles en prompts largos

**Síntoma:** CLI acepta prompt pero respuesta muestra caracteres corruptos.

**Causa:** Archivo temporal creado sin encoding UTF-8.

**Solución:**
```powershell
# Al crear archivos temporales
$prompt | Out-File -FilePath temp.txt -Encoding UTF8

# NO usar:
$prompt > temp.txt  # Usa encoding del sistema (no UTF-8)
```

---

## ⏱️ Timeouts y Latencia

### Caso 3: Gemini timeout variable (15-68 segundos)

**Contexto:** Mismo prompt, diferente latencia según hora del día.

**Datos empíricos:**
- Latencia mínima: 15 segundos
- Latencia máxima: 68 segundos
- Promedio: ~30 segundos

**Configuración recomendada:**
```python
GEMINI_TIMEOUT = 90000  # 90 segundos (margen de seguridad)
```

**Lección:** No asumir latencias consistentes. Usar timeouts 3x promedio.

---

## 📄 Parsing de JSON

### Caso 5: JSON envuelto en markdown (todos los CLIs)

**Problema:** Todos los CLIs decoran JSON:

```markdown
Aquí está el resultado:

```json
{
  "status": "OK"
}
```

Espero que sea útil!
```

**Solución multi-estrategia:**

```python
import re
import json

def extract_json(text: str) -> dict:
    text = text.strip()
    
    # Estrategia 1: Parseo directo
    try:
        return json.loads(text)
    except json.JSONDecodeError:
        pass
    
    # Estrategia 2: Buscar bloque markdown
    match = re.search(r'```json\s*(.*?)\s*```', text, re.DOTALL)
    if match:
        try:
            return json.loads(match.group(1))
        except json.JSONDecodeError:
            pass
    
    # Estrategia 3: Buscar primer { hasta último }
    first = text.find('{')
    last = text.rfind('}')
    if first != -1 and last != -1:
        try:
            return json.loads(text[first:last+1])
        except json.JSONDecodeError:
            pass
    
    raise ValueError(f"No JSON válido en: {text[:200]}...")
```

**Lección:** Nunca confiar en formato de respuesta. Siempre extraer JSON con fallbacks.

---

## 💻 Limitaciones de PowerShell

### Caso 6: Command line length limit (8191 chars)

**Síntoma:** Prompt largo se trunca silenciosamente.

**Contexto:** Windows PowerShell limita comandos a ~8191 caracteres.

**Solución:** Usar archivo temporal + stdin

```powershell
$prompt | Out-File -FilePath temp.txt -Encoding UTF8
Get-Content temp.txt | claude --allowedTools ""
Remove-Item temp.txt
```

**Lección:** En Windows, NO pasar prompts largos como argumentos de CLI.

---

## 📊 Resumen de Mejores Prácticas

| Problema | Prevención |
|----------|------------|
| Encoding | SIEMPRE configurar UTF-8 en Windows |
| Timeouts | Usar 3x latencia promedio |
| JSON | Implementar multi-estrategia de parsing |
| Prompts largos | Usar archivos temporales + stdin |
| Procesos huérfanos | Limpieza sistemática antes/después |

---

## 📚 Ver También

- [Comparativa de CLIs](comparativa.html) - ¿Cuándo usar qué?
- Guías individuales: [Claude](claude-code.html) · [Gemini](gemini-cli.html) · [DeepSeek](deepseek-cli.html)
- [GitHub Repository](https://github.com/Krakaur/guia-cli-ia)

---

**Contribuye:** Si encuentras nuevos casos, abre un [issue](https://github.com/Krakaur/guia-cli-ia/issues)

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur