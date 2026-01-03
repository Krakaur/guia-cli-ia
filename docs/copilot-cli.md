---
layout: page
title: GitHub Copilot CLI - Guía Completa
description: Guía de GitHub Copilot CLI con 13 modelos disponibles, solución al problema de modelos premium en batch
keywords: github copilot cli, copilot batch mode, claude opus copilot, gpt-5.2
permalink: /copilot-cli/
---

# GitHub Copilot CLI

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | 0.0.372+ |
| **Comando** | `copilot` |
| **Región** | 🇺🇸 USA (GitHub/Microsoft) |
| **Instalación** | npm global |
| **Autenticación** | GitHub token |
| **Costo** | Gratis con Student Developer Pack |

---

## 🤖 Modelos Disponibles

### Total: 13 modelos

| Modelo | Familia | Disponibilidad Batch |
|--------|---------|---------------------|
| **claude-sonnet-4.5** | Claude | ⚠️ Requiere activación interactiva |
| claude-haiku-4.5 | Claude | ⚠️ Requiere activación interactiva |
| claude-opus-4.5 | Claude | ⚠️ Requiere activación interactiva |
| **gpt-5.2** | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5.1 | OpenAI | ⚠️ Requiere activación interactiva |
| **gpt-4.1** | OpenAI | ✅ Funciona directo en batch |
| **gpt-4o** | OpenAI | ✅ Funciona directo en batch (DEFAULT) |
| gemini-3-pro-preview | Google | ⚠️ Requiere activación interactiva |

---

## ⚠️ LIMITACIÓN CRÍTICA: Modelos Premium en Batch

### Problema

Modelos premium (Claude Opus, GPT-5.x) **NO funcionan directamente** en modo batch:

```bash
copilot -p "Test" --model gpt-5.2 -s --allow-all-tools
# Error: "Run in interactive mode to enable this model"
```

### Solución: Activación Previa

**Paso 1:** Ejecutar en terminal interactivo real:
```bash
copilot --model gpt-5.2
# Esperar activación
# Ctrl+C para salir
```

**Paso 2:** Después funciona en batch:
```bash
copilot -p "Test" --model gpt-5.2 -s --allow-all-tools
# Ahora funciona ✅
```

### Modelo Default Real en Batch

```bash
# Sin especificar modelo
copilot -p "Test" -s --allow-all-tools
# Usa: gpt-4o (NO el configurado en config.json)
```

---

## 💻 Uso Básico

### Modo Batch (No Interactivo)

```bash
copilot -p "Tu prompt aquí" -s --allow-all-tools
```

**Flags importantes:**
- `-p, --prompt <text>` → Modo no-interactivo
- `-s, --silent` → Solo output del agente (para scripting)
- `--allow-all-tools` → Aprobación automática de herramientas
- `--model <modelo>` → Seleccionar modelo específico

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- Acceso a **13 modelos diferentes** en un solo CLI
- Comparación rápida entre Claude, GPT, Gemini
- Tareas que requieren modelo específico
- Automatización con GPT-4o o GPT-4.1 (únicos batch-ready)

### ❌ No Recomendado Para:
- Batch automatizado con modelos premium (sin activación previa)
- Scripts que requieren modelo específico sin intervención humana
- Procesamiento masivo (rate limits estrictos)

---

## 🔗 Confusión Común: `gh` vs `copilot`

Existen **DOS herramientas diferentes**:

| Herramienta | Paquete | Instalación |
|-------------|---------|-------------|
| `gh copilot` | GitHub CLI | `winget install GitHub.cli` |
| `copilot` | @github/copilot | `npm install -g @github/copilot` |

**Esta guía cubre:** `copilot` standalone (npm)

---

## 📚 Ver También

- [Comparativa](comparativa.html) - ¿Cuándo usar Copilot vs otros?
- [Troubleshooting](troubleshooting.html) - Modelos premium, tokens
- [Informe Completo](https://github.com/Krakaur/guia-cli-ia/blob/main/COPILOT_CLI_INFORME_COMPLETO.md)

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur