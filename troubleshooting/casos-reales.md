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

### Caso 4: Claude Code timeout en PDFs grandes

**Síntoma:** `claude -p "analiza PDF..."` timeout después de 120 segundos.

**Causa:** PDF de 225 páginas excede contexto procesable en tiempo razonable.

**Solución:** Truncar PDF antes de enviar.

```python
from PyPDF2 import PdfReader, PdfWriter

def truncate_pdf(input_path, max_pages=7):
    reader = PdfReader(input_path)
    writer = PdfWriter()
    
    for i in range(min(max_pages, len(reader.pages))):
        writer.add_page(reader.pages[i])
    
    output_path = f"truncated_{input_path.name}"
    with open(output_path, 'wb') as f:
        writer.write(f)
    
    return output_path
```

**Lección:** Preprocesar documentos grandes antes de enviar a LLM.

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
    
    # Estrategia 4: Buscar primer [ hasta último ]
    first = text.find('[')
    last = text.rfind(']')
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

**Detección:**
```powershell
$cmd = "claude -p '$largoPrompt' --allowedTools ''"
if ($cmd.Length -gt 8000) {
    Write-Warning "Prompt puede truncarse!"
}
```

**Solución 1: Archivo temporal + stdin**
```powershell
$prompt | Out-File -FilePath temp.txt -Encoding UTF8
Get-Content temp.txt | claude --allowedTools ""
Remove-Item temp.txt
```

**Solución 2: Python wrapper**
```python
import subprocess

def call_cli_safe(cli, prompt, timeout=120):
    with tempfile.NamedTemporaryFile(mode='w', encoding='utf-8', 
                                     suffix='.txt', delete=False) as f:
        f.write(prompt)
        temp_file = f.name
    
    try:
        cmd = f'type "{temp_file}" | {cli}'
        result = subprocess.run(cmd, shell=True, capture_output=True,
                               text=True, timeout=timeout, encoding='utf-8')
        return result.stdout
    finally:
        Path(temp_file).unlink()
```

**Lección:** En Windows, NO pasar prompts largos como argumentos de CLI.

---

## 👻 Procesos Huérfanos

### Caso 7: Gemini deja procesos huérfanos

**Síntoma:** Después de usar Gemini 10+ veces, memoria del sistema alta.

**Diagnóstico:**
```powershell
Get-Process | Where-Object {$_.ProcessName -like "*node*"} | 
    Measure-Object -Property WS -Sum

# Resultado: 2GB+ en procesos node.js
```

**Causa:** Gemini CLI inicia proceso Node.js que no siempre termina correctamente.

**Solución: Protocolo de higiene**

```python
# ANTES de cada llamada a Gemini
list_sessions()  # Ver procesos activos
force_terminate(pid)  # Matar huérfanos

# Ejecutar Gemini
result = gemini(prompt)

# DESPUÉS de cada llamada (SIEMPRE)
force_terminate(gemini_pid)
```

**Lección:** CLIs basados en Node.js requieren limpieza activa de procesos.

---

## 🔐 Modelos y Autenticación

### Caso 8: Copilot - modelos premium no funcionan en batch

**Síntoma:**
```bash
copilot -p "test" --model gpt-5.2 -s --allow-all-tools
# Error: "Run in interactive mode to enable this model"
```

**Causa:** Modelos premium requieren activación interactiva previa.

**Solución:**
```bash
# Paso 1: Activar interactivamente (una vez)
copilot --model gpt-5.2
# [Esperar activación, Ctrl+C para salir]

# Paso 2: Ahora funciona en batch
copilot -p "test" --model gpt-5.2 -s --allow-all-tools
```

**Modelos que NO requieren activación:**
- ✅ `gpt-4.1`
- ✅ `gpt-4o`

**Lección:** Documentar qué modelos funcionan en batch vs interactivo.

---

### Caso 9: Token GitHub expirado

**Síntoma:** Copilot falla con 401 Unauthorized.

**Diagnóstico:**
```powershell
# Verificar si token existe
echo $env:COPILOT_GITHUB_TOKEN

# Verificar si es válido (via GitHub API)
$headers = @{
    "Authorization" = "Bearer $env:COPILOT_GITHUB_TOKEN"
}
Invoke-RestMethod -Uri "https://api.github.com/user" -Headers $headers
```

**Solución:**
1. Ir a: https://github.com/settings/tokens
2. Regenerar token
3. Actualizar variable:
```powershell
[Environment]::SetEnvironmentVariable("COPILOT_GITHUB_TOKEN", "nuevo-token", "User")
```

**Lección:** Tokens tienen expiración. Implementar verificación periódica.

---

## 🔄 Modo Interactivo Inesperado

### Caso 10: Gemini entra en modo interactivo (batch corrupto)

**Síntoma:** Script se detiene esperando input del usuario.

**Causa:** Prompt >500 caracteres activa confirmación interactiva.

**Detección:**
```python
if len(prompt) > 500:
    logger.warning(f"Prompt largo ({len(prompt)} chars) - riesgo de modo interactivo")
```

**Solución:** Mantener prompts <200 caracteres para Gemini en automatización.

```python
def truncate_prompt_safe(prompt, max_length=200):
    if len(prompt) <= max_length:
        return prompt
    
    # Truncar inteligentemente (no a media palabra)
    truncated = prompt[:max_length].rsplit(' ', 1)[0]
    return truncated + "..."
```

**Lección:** Cada CLI tiene umbrales diferentes para activar modo interactivo.

---

## 📊 Resumen de Mejores Prácticas

| Problema | Prevención |
|----------|-----------|
| Encoding | SIEMPRE configurar UTF-8 en Windows |
| Timeouts | Usar 3x latencia promedio |
| JSON | Implementar multi-estrategia de parsing |
| Prompts largos | Usar archivos temporales + stdin |
| Procesos huérfanos | Limpieza sistemática antes/después |
| Modelos premium | Activar interactivamente primero |
| Tokens | Verificar validez periódicamente |

---

## 🔬 Metodología de Troubleshooting

### Paso 1: Reproducir con caso mínimo

```bash
# NO hacer:
copilot -p "$complejo_prompt_con_variables" --model $modelo -s --allow-all-tools

# SÍ hacer:
copilot -p "hola" --model gpt-4.1 -s --allow-all-tools
```

### Paso 2: Aislar variable

¿Falla con:
- ✅ Prompt específico → Problema en contenido
- ✅ Modelo específico → Problema en autenticación/disponibilidad
- ✅ Siempre → Problema en instalación/config

### Paso 3: Documentar empíricamente

```markdown
## Issue: Copilot timeout con modelo X

**Intentos:**
1. Timeout 30s → Falla
2. Timeout 60s → Falla
3. Timeout 120s → ✅ Funciona

**Conclusión:** Modelo X requiere timeout mínimo 120s.
```

---

**Contribuye:** Si encuentras nuevos casos, abre un [issue](https://github.com/Krakaur/guia-cli-ia/issues) con:
- Síntoma exacto
- Comando ejecutado
- Output del error
- Solución que funcionó

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur
