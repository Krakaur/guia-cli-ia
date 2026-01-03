---
layout: page
title: Claude Code CLI - Guía Completa
description: Tutorial paso a paso de Claude Code CLI con ejemplos prácticos y troubleshooting en español
keywords: claude code, claude cli, tutorial español, automatización ia, anthropic
permalink: /claude-code/
---

# Claude Code CLI

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | 2.0.76+ |
| **Comando** | `claude` |
| **Región** | 🇺🇸 USA (Anthropic) |
| **Instalación** | npm global |
| **Autenticación** | Automática al primer uso |
| **Costo** | Gratuito con cuenta Anthropic |

---

## 🚀 Instalación

### Requisitos Previos
- Node.js 18+
- Cuenta en [claude.ai](https://claude.ai)

### Instalación Global

```bash
npm install -g @anthropic-ai/claude-code
```

### Verificar Instalación

```bash
claude --version
# Salida esperada: 2.0.76 (o superior)
```

---

## 💻 Uso Básico

### Modo Batch (No Interactivo)

Para uso en scripts o automatización:

```bash
claude -p "Tu prompt aquí" --allowedTools ""
```

**Flags importantes:**
- `-p, --prompt` → Modo no interactivo
- `--allowedTools ""` → Desactiva ejecución de código (solo respuestas de texto)

### Modo Interactivo

```bash
claude
# Abre sesión interactiva
```

---

## 📝 Ejemplos Prácticos

### Ejemplo 1: Consulta Simple

```bash
claude -p "Explica la diferencia entre async/await y Promises en JavaScript" --allowedTools ""
```

### Ejemplo 2: Análisis de Código

```bash
claude -p "Revisa este código y sugiere mejoras: $(cat script.py)" --allowedTools ""
```

### Ejemplo 3: Generación de Documentación

```bash
claude -p "Genera documentación JSDoc para las funciones en utils.js" --allowedTools ""
```

---

## ⚠️ Limitaciones Conocidas

### 1. Longitud de Prompts en PowerShell

**Problema:** Windows PowerShell tiene límite de ~8191 caracteres en línea de comandos.

**Solución:** Usar archivos temporales con stdin:

```powershell
# Crear archivo temporal con prompt
$prompt = "Prompt muy largo..."
$prompt | Out-File -FilePath temp_prompt.txt -Encoding UTF8

# Ejecutar via stdin
Get-Content temp_prompt.txt | claude --allowedTools ""

# Limpiar
Remove-Item temp_prompt.txt
```

### 2. Timeout en Operaciones Largas

Claude Code puede tomar tiempo en tareas complejas. Usar timeout explícito en PowerShell:

```powershell
$timeout = 180  # 3 minutos
Start-Process -FilePath "claude" -ArgumentList "-p `"$prompt`" --allowedTools ''" -Wait -NoNewWindow -TimeoutSeconds $timeout
```

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- Análisis de código complejo
- Generación de documentación técnica
- Debugging de errores
- Explicaciones detalladas de conceptos
- Tareas que requieren razonamiento profundo

### ❌ No Recomendado Para:
- Respuestas muy rápidas (usa Gemini o GPT-4)
- Tareas puramente de ejecución de código (usa Codex)
- Procesamiento masivo (limitado por rate limits)

---

## 📚 Ver También

- [Comparativa de CLIs](comparativa.html) - ¿Cuándo usar Claude vs otros?
- [Troubleshooting](troubleshooting.html) - Soluciones a problemas comunes
- [GitHub Repository](https://github.com/Krakaur/guia-cli-ia)

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur