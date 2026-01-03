---
layout: page
title: DeepSeek CLI - Guía con Fix UTF-8 para Windows
description: Tutorial DeepSeek CLI con solución al problema crítico de encoding UTF-8 en Windows
keywords: deepseek cli, deepseek windows error, unicode encode error, utf-8 fix
permalink: /deepseek-cli/
---

# DeepSeek CLI

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | pip (latest) |
| **Comando** | `deepseek` |
| **Región** | 🇨🇳 China (DeepSeek AI) |
| **Instalación** | pip |
| **Autenticación** | API Key |
| **Costo** | Gratis con límites |

---

## ⚠️ FIX CRÍTICO: Encoding UTF-8 en Windows

### Problema

DeepSeek CLI **crashea** en Windows cuando respuestas contienen:
- Emojis (😀, 🚀, etc.)
- Caracteres especiales
- Acentos en volumen alto

**Error típico:**
```
UnicodeEncodeError: 'charmap' codec can't encode character...
```

### Solución: Variable de Entorno

```powershell
# SIEMPRE configurar antes de ejecutar
$env:PYTHONIOENCODING="utf-8"

# Ejemplo de uso completo
$env:PYTHONIOENCODING="utf-8"
$env:DEEPSEEK_API_KEY="sk-tu-key"
deepseek -q "Tu prompt aquí" -r
```

### Hacer Permanente (Recomendado)

```powershell
# PowerShell (permanente para usuario)
[Environment]::SetEnvironmentVariable("PYTHONIOENCODING", "utf-8", "User")
[Environment]::SetEnvironmentVariable("DEEPSEEK_API_KEY", "tu-api-key", "User")
```

---

## 💻 Uso Básico

### Sintaxis Completa

```powershell
$env:PYTHONIOENCODING="utf-8"
$env:DEEPSEEK_API_KEY="sk-tu-key"
deepseek -q "Tu prompt aquí" -r
```

### Flags Importantes

- `-q, --query` → El prompt
- `-r` → Modo respuesta directa (batch, no interactivo)
- `-m, --model` → Seleccionar modelo

### Modelos Disponibles

1. `deepseek-chat` (default) - Conversacional general
2. `deepseek-coder` - Especializado en código
3. `deepseek-reasoner` - Razonamiento avanzado

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- Backup rápido cuando otros CLIs tienen timeout
- Perspectiva china en investigación (triangulación)
- Tareas de código con `deepseek-coder`
- Razonamiento complejo con `deepseek-reasoner`

### ❌ No Recomendado Para:
- Primera opción (problemas de encoding frecuentes)
- Windows sin parches/variables configuradas
- Batch largo sin limpieza de memoria

---

## 🐛 Troubleshooting

### Error 1: UnicodeEncodeError

**Solución:** Configurar `PYTHONIOENCODING="utf-8"` (ver Fix Crítico arriba)

### Error 2: API Key not found

```powershell
# Verificar
echo $env:DEEPSEEK_API_KEY
```

### Error 3: Crash silencioso

**Causa:** Respuesta del modelo contiene emoji/caracteres especiales sin encoding fix.

**Solución:** Ver Fix Crítico arriba.

---

## 📚 Ver También

- [Comparativa](comparativa.html) - DeepSeek como backup
- [Troubleshooting](troubleshooting.html) - Encoding UTF-8 detallado
- [Qwen CLI](qwen-cli.html) - Otra perspectiva china

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur