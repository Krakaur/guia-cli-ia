---
layout: page
title: GitHub CLI - Guía Completa en Español
description: Tutorial de GitHub CLI (gh) para gestionar repositorios, issues y PRs desde terminal
keywords: github cli, gh cli, tutorial español, gestionar repos terminal
permalink: /github-cli/
---

# GitHub CLI (gh)

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | 2.64.0+ |
| **Comando** | `gh` |
| **Región** | 🇺🇸 USA (GitHub/Microsoft) |
| **Instalación** | winget, brew, apt |
| **Autenticación** | GitHub account (OAuth o PAT) |
| **Costo** | Gratis |

---

## 🚀 Instalación

### Windows

```powershell
winget install GitHub.cli
```

### macOS

```bash
brew install gh
```

### Linux (Debian/Ubuntu)

```bash
sudo apt install gh
```

---

## 🔐 Autenticación

```bash
gh auth login
```

**Opciones:**
1. Selecciona: **GitHub.com**
2. Protocolo: **HTTPS**
3. Autenticación: **Login with a web browser** (recomendado)
4. Autoriza GitHub CLI

### Verificar Estado

```bash
gh auth status
```

---

## 💻 Comandos Esenciales

### Repositorios

```bash
# Listar tus repositorios
gh repo list

# Crear repositorio
gh repo create mi-nuevo-repo --public

# Clonar repositorio
gh repo clone owner/repo

# Ver en navegador
gh repo view --web
```

### Issues

```bash
# Listar issues
gh issue list

# Crear issue
gh issue create --title "Título" --body "Descripción"

# Ver issue
gh issue view 42
```

### Pull Requests

```bash
# Listar PRs
gh pr list

# Crear PR
gh pr create --title "Título" --body "Descripción"

# Mergear PR
gh pr merge 15 --squash
```

---

## 🔗 Diferencia con Copilot CLI

**IMPORTANTE:** Son herramientas **diferentes**:

| Herramienta | Propósito | Instalación |
|-------------|----------|-------------|
| **`gh`** | Gestionar GitHub | `winget install GitHub.cli` |
| **`copilot`** | IA/Modelos | `npm install -g @github/copilot` |

**Para interactuar con IA:** Usa `copilot` standalone, NO `gh copilot`

---

## 🎯 Casos de Uso

### ✅ Ideal Para:
- Crear repos sin abrir navegador
- Gestionar issues y PRs desde terminal
- Automatizar workflows de GitHub
- Scripts de CI/CD

### ❌ No Recomendado Para:
- Interactuar con modelos de IA (usa Copilot CLI)
- Tareas complejas de Git (usa `git` directamente)

---

## 💡 Integración con API

```bash
# Request directo a GitHub API
gh api repos/owner/repo/issues

# POST a API
gh api repos/owner/repo/issues \
  -f title="Nuevo issue" \
  -f body="Descripción"
```

---

## 🎓 Los Magníficos 7 - Completados

GitHub CLI es el **#7** de la colección:

1. ✅ Claude Code
2. ✅ Gemini
3. ✅ Copilot
4. ✅ DeepSeek
5. ✅ Qwen
6. ✅ Codex
7. ✅ **GitHub CLI** 🎉

---

## 📚 Ver También

- [Comparativa](comparativa.html) - ¿Cuándo usar qué?
- [Copilot CLI](copilot-cli.html) - CLI de IA (diferente)
- [Docs Oficiales](https://cli.github.com/manual/)

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur