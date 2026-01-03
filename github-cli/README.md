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

### Verificar Instalación

```bash
gh --version
# Salida esperada: gh version 2.64.0 (o superior)
```

---

## 🔐 Autenticación

### Primera Vez (Interactivo)

```bash
gh auth login
```

**Opciones:**
1. Selecciona: **GitHub.com**
2. Protocolo: **HTTPS**
3. Autenticación: **Login with a web browser** (recomendado)
4. Copia el código de un solo uso
5. Pega en navegador
6. Autoriza GitHub CLI

### Verificar Autenticación

```bash
gh auth status
```

**Salida esperada:**
```
github.com
  ✓ Logged in to github.com account Krakaur (keyring)
  ✓ Git operations protocol: https
  ✓ Token: gho_****
  ✓ Token scopes: 'gist', 'read:org', 'repo', 'workflow'
```

---

## 💻 Comandos Básicos

### Repositorios

```bash
# Listar tus repositorios
gh repo list

# Listar repos de una organización
gh repo list Krakaur

# Crear repositorio
gh repo create mi-nuevo-repo --public

# Clonar repositorio
gh repo clone Krakaur/guia-cli-ia

# Ver repositorio en navegador
gh repo view --web
```

### Issues

```bash
# Listar issues
gh issue list

# Crear issue
gh issue create --title "Agregar nueva feature" --body "Descripción detallada"

# Ver issue específico
gh issue view 42

# Cerrar issue
gh issue close 42
```

### Pull Requests

```bash
# Listar PRs
gh pr list

# Crear PR
gh pr create --title "Fix bug" --body "Descripción del fix"

# Ver PR
gh pr view 15

# Mergear PR
gh pr merge 15 --squash

# Checkout PR localmente
gh pr checkout 15
```

### Gists

```bash
# Crear gist
gh gist create archivo.py --public

# Listar gists
gh gist list

# Ver gist
gh gist view <gist-id>
```

---

## 🤖 Diferencia con Copilot CLI

**Confusión común:** Existen **DOS herramientas diferentes**:

| Herramienta | Paquete | Propósito | Instalación |
|-------------|---------|----------|-------------|
| **`gh` (GitHub CLI)** | GitHub CLI | Gestionar repos, issues, PRs | `winget install GitHub.cli` |
| **`copilot` (standalone)** | @github/copilot | Interactuar con modelos IA | `npm install -g @github/copilot` |
| **`gh copilot`** | Subcomando de gh | Acceso limitado a Copilot | Requiere `gh` instalado |

**Recomendación:** 
- Para **gestionar GitHub**: Usa `gh`
- Para **IA/modelos**: Usa `copilot` standalone (npm)

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- Automatizar workflows de GitHub desde terminal
- Crear repos, issues, PRs sin abrir navegador
- Scripts de CI/CD que interactúan con GitHub
- Gestión rápida de proyectos open-source
- Clonar repos sin copiar URLs

### ❌ No Recomendado Para:
- Interactuar con modelos de IA (usa Copilot CLI)
- Editar código (usa tu IDE)
- Tareas complejas de Git (usa `git` directamente)

---

## 🔗 Integración con Otros Servicios

### GitHub Actions

```bash
# Ver workflows
gh workflow list

# Ver runs de un workflow
gh run list --workflow=ci.yml

# Ver logs de un run
gh run view <run-id> --log
```

### GitHub API

```bash
# Hacer request directo a API
gh api repos/Krakaur/guia-cli-ia/issues

# POST a API
gh api repos/Krakaur/guia-cli-ia/issues \
  -f title="Nuevo issue" \
  -f body="Descripción"
```

---

## 🐛 Troubleshooting

### Error: "gh not found"

**Causa:** No está en PATH

**Solución Windows:**
```powershell
# Verificar instalación
winget list GitHub.cli

# Reinstalar si es necesario
winget install GitHub.cli

# Reiniciar terminal
```

### Error: "authentication required"

**Solución:**
```bash
gh auth login
```

### Error: "insufficient scopes"

**Causa:** Token sin permisos necesarios

**Solución:**
```bash
# Re-autenticar con scopes completos
gh auth login --scopes repo,workflow,gist,read:org
```

---

## 💡 Tips Avanzados

### Aliases

Crear shortcuts personalizados:

```bash
# Crear alias
gh alias set pv 'pr view'

# Ahora puedes usar:
gh pv 15  # Equivalente a: gh pr view 15
```

### Extensiones

Instalar funcionalidad adicional:

```bash
# Buscar extensiones
gh extension search

# Instalar extensión
gh extension install dlvhdr/gh-dash

# Listar extensiones instaladas
gh extension list
```

---

## 📖 Comandos de Referencia Rápida

| Acción | Comando |
|--------|--------|
| Crear repo | `gh repo create` |
| Clonar repo | `gh repo clone owner/repo` |
| Crear issue | `gh issue create` |
| Listar PRs | `gh pr list` |
| Crear PR | `gh pr create` |
| Ver en web | `gh repo view --web` |
| Estado auth | `gh auth status` |
| API request | `gh api <endpoint>` |

---

## 📚 Ver También

- [Comparativa de CLIs](../troubleshooting/comparativa-clis.md) - ¿Cuándo usar gh vs otros?
- [Copilot CLI](../copilot-cli/README.md) - CLI de IA (diferente a gh)
- [GitHub CLI Docs](https://cli.github.com/manual/) - Documentación oficial

---

## 🎓 Proyecto Round Table

GitHub CLI es el **#7 de Los Magníficos 7** - colección de CLIs para investigación multi-agente:

| # | CLI | Región | Propósito |
|---|-----|--------|----------|
| 1 | Claude Code | 🇺🇸 | Análisis profundo |
| 2 | Gemini | 🇺🇸 | Validación rápida |
| 3 | Copilot | 🇺🇸 | 13 modelos |
| 4 | DeepSeek | 🇨🇳 | Perspectiva china |
| 5 | Qwen | 🇨🇳 | Triangulación |
| 6 | Codex | 🇺🇸 | Automatización |
| **7** | **GitHub CLI** | 🇺🇸 | **Gestión repos** |

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur  
**Proyecto:** [guia-cli-ia](https://github.com/Krakaur/guia-cli-ia)