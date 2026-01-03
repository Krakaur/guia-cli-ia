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

## 🔧 Configuración Avanzada

### Formato de Respuesta

Claude Code puede responder en formato JSON cuando se solicita explícitamente:

```bash
claude -p "Lista 3 frameworks de Python para ML. Responde SOLO en JSON: {frameworks: []}" --allowedTools ""
```

**Nota:** Respuestas JSON suelen venir envueltas en bloques markdown:
```markdown
```json
{...}
```
```

Requiere parsing con regex: `` `json\s*(.*?)\s*` ``

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

### 3. Respuestas con Decoración Markdown

Incluso con `--allowedTools ""`, Claude puede incluir markdown. Requiere limpieza:

```python
import re

def extract_json(text):
    # Buscar bloque JSON en markdown
    match = re.search(r'```json\s*(.*?)\s*```', text, re.DOTALL)
    if match:
        return match.group(1)
    return text
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

## 🔗 Integración con MCP

Claude Code se integra con **Model Context Protocol (MCP)** en Claude Desktop:

```json
// claude_desktop_config.json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
    }
  }
}
```

---

## 📚 Recursos Adicionales

- [Documentación Oficial](https://code.anthropic.com)
- [GitHub Repository](https://github.com/anthropics/claude-code)
- [Community Forum](https://community.anthropic.com)

---

## 🐛 Troubleshooting

Ver [troubleshooting.md](./troubleshooting.md) para soluciones a problemas comunes.

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur
