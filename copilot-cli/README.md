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

## 🚀 Instalación

### Prerequisitos
- GitHub account
- **GitHub Student Developer Pack** (para uso gratuito)

### Instalación

```bash
npm install -g @github/copilot
```

### Verificar Instalación

```bash
copilot --version
# Salida esperada: 0.0.372 · Commit 5534560
```

### Autenticación

```bash
# Configurar token como variable de entorno (permanente)
[Environment]::SetEnvironmentVariable("COPILOT_GITHUB_TOKEN", "ghp_TU_TOKEN_AQUI", "User")
```

**⚠️ Obtener Token:**
1. Ve a GitHub → Settings → Developer settings → Personal access tokens
2. Generate new token (classic)
3. Scopes necesarios: `copilot`

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
- `--no-color` → Desactivar colores (útil para pipes)
- `--stream off` → Desactivar streaming

### Modo Interactivo

```bash
copilot

# Dentro del modo interactivo:
/model claude-sonnet-4.5  # Cambiar modelo
/help                     # Ver comandos
```

---

## 🤖 Modelos Disponibles

### Total: 13 modelos

| Modelo | Familia | Disponibilidad Batch |
|--------|---------|---------------------|
| **claude-sonnet-4.5** | Claude | ⚠️ Requiere activación interactiva |
| claude-haiku-4.5 | Claude | ⚠️ Requiere activación interactiva |
| claude-opus-4.5 | Claude | ⚠️ Requiere activación interactiva |
| claude-sonnet-4 | Claude | ⚠️ Requiere activación interactiva |
| **gpt-5.2** | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5.1 | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5 | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5.1-codex-max | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5.1-codex | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5.1-codex-mini | OpenAI | ⚠️ Requiere activación interactiva |
| gpt-5-mini | OpenAI | ⚠️ Requiere activación interactiva |
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

**Paso 1:** Ejecutar en terminal interactivo real (no via MCP):
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

## 🔧 Configuración

### Ubicación del Config

```
C:\Users\PC\.copilot\config.json
```

### Ejemplo config.json

```json
{
  "default_model": "claude-sonnet-4.5",
  "github_token_source": "environment",
  "auto_approve_tools": false
}
```

**Nota:** `default_model` en config **NO se aplica en batch**. Debes especificar con `--model`.

---

## 📝 Ejemplos Prácticos

### Ejemplo 1: Consulta Simple (Modelo Default)

```bash
copilot -p "Explica async/await en JavaScript" -s --allow-all-tools
```

### Ejemplo 2: Con Modelo Específico

```bash
copilot -p "Analiza este código" --model gpt-4.1 -s --allow-all-tools
```

### Ejemplo 3: Sin Streaming (Para Parsing)

```bash
copilot -p "Dame JSON con 3 frameworks Python" --stream off -s --allow-all-tools
```

### Ejemplo 4: Sin Colores (Para Logs)

```bash
copilot -p "Lista archivos del proyecto" --no-color -s --allow-all-tools > output.txt
```

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

## 🔗 Integración con GitHub (vs GitHub CLI)

### ⚠️ Confusión Común

Existen **DOS herramientas diferentes**:

| Herramienta | Paquete | Instalación | Uso |
|-------------|---------|-------------|-----|
| `gh copilot` | GitHub CLI | `winget install GitHub.cli` | Subcomando de gh |
| `copilot` | @github/copilot | `npm install -g @github/copilot` | CLI standalone |

**En este sistema:** Usamos **`copilot`** standalone (npm), NO `gh copilot`.

---

## 🐛 Troubleshooting

### Error 1: "No model available"

**Causa:** Copilot Pro no activado.

**Solución:**
1. Ir a: https://github.com/settings/copilot
2. Habilitar Copilot Pro (gratis con Student Pack)

### Error 2: Token expirado

```bash
# Verificar token
echo $env:COPILOT_GITHUB_TOKEN

# Regenerar en: https://github.com/settings/tokens?type=beta
```

### Error 3: Modelo no funciona en batch

**Causa:** Modelo premium sin activación previa.

**Solución:** Ver [Limitación Crítica](#limitación-crítica-modelos-premium-en-batch) arriba.

---

## 📊 Comparación con Otras CLIs

| Característica | Copilot CLI | Claude Code | Gemini CLI |
|----------------|-------------|-------------|------------|
| Modelos disponibles | 13 | 1 | 1 |
| Batch sin activación | 2/13 | Sí | Sí |
| Gratis con Student Pack | ✅ | ✅ | ✅ |
| Respuestas JSON limpias | ❌ | ❌ | ❌ |
| Stateless | ✅ | ✅ | ✅ |

---

## 📚 Recursos Adicionales

- [Documentación Oficial](https://docs.github.com/en/copilot/github-copilot-in-the-cli)
- [GitHub Copilot Settings](https://github.com/settings/copilot)
- [Logs](C:\Users\PC\.copilot\logs\)

---

## 🔬 Resultados en Pruebas Cognitivas

### Medieval Logic Puzzle Test

**Modelo:** GPT-4o (default batch)
**Resultado:** Sir Richard ganador, Sir John perdedor ✅
**Coincidencia:** 6/7 modelos (consenso mayoritario)

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur

**Basado en:** [COPILOT_CLI_INFORME_COMPLETO.md](../../docs/COPILOT_CLI_INFORME_COMPLETO.md)
