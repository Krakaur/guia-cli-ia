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

## 🚀 Instalación

### Paso 1: Instalar via pip

```bash
pip install deepseek --break-system-packages
```

**Nota:** Flag `--break-system-packages` requerido en algunos sistemas.

### Paso 2: Obtener API Key

1. Regístrate en [DeepSeek Platform](https://platform.deepseek.com)
2. Ve a API Keys
3. Crea nuevo key
4. Copia el token: `sk-xxxxx`

### Paso 3: Verificar Instalación

```bash
deepseek --version
```

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
$env:DEEPSEEK_API_KEY="sk-970bf433f35049b098d414a299ba59fc"
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
$env:DEEPSEEK_API_KEY="sk-970bf433f35049b098d414a299ba59fc"
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

## 📝 Ejemplos Prácticos

### Ejemplo 1: Consulta Simple

```powershell
$env:PYTHONIOENCODING="utf-8"
$env:DEEPSEEK_API_KEY="sk-tu-key"
deepseek -q "¿Qué es Python?" -r
```

### Ejemplo 2: Con Modelo Específico

```powershell
$env:PYTHONIOENCODING="utf-8"
$env:DEEPSEEK_API_KEY="sk-tu-key"
deepseek -q "Escribe función fibonacci" -r -m deepseek-coder
```

### Ejemplo 3: Modo Razonamiento

```powershell
$env:PYTHONIOENCODING="utf-8"
$env:DEEPSEEK_API_KEY="sk-tu-key"
deepseek -q "Explica teorema de Gödel" -r -m deepseek-reasoner
```

---

## 🔧 Archivos Parcheados (Windows)

### Ubicación de Parches

Si el encoding fix no funciona vía variable de entorno, se aplicaron parches directos:

```
C:\Program Files\Python314\Lib\site-packages\cli\deepseek_cli.py
```

**Parche aplicado:**
```python
# Línea ~45
import sys
sys.stdout.reconfigure(encoding='utf-8')
sys.stderr.reconfigure(encoding='utf-8')
```

**Nota:** Este parche se pierde al actualizar el paquete. Preferir variable de entorno.

---

## 📊 Formato de Respuestas

### JSON con Decoración

DeepSeek decora JSON similar a otros CLIs:

```markdown
Aquí está el resultado:

```json
{
  "resultado": "valor"
}
```

Espero que sea útil!
```

**Parsing requerido:** Ver [guía de troubleshooting](../troubleshooting/casos-reales.md#parsing-json)

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

## ⚠️ Limitaciones Conocidas

### 1. Encoding UTF-8
**Ya cubierto** - siempre configurar `PYTHONIOENCODING`

### 2. Rate Limits
Más estrictos que Gemini o Claude Code

### 3. Calidad de Respuestas
Menor consistencia que GPT/Claude en tareas complejas

---

## 🔗 Integración con Round Table MCP

DeepSeek funciona como **modelo de respaldo** en sistemas multi-agente:

```python
# Ejemplo: Fallback si Claude timeout
try:
    response = claude_code(prompt, timeout=60)
except TimeoutError:
    logger.warn("Claude timeout, usando DeepSeek")
    response = deepseek_cli(prompt)
```

---

## 🐛 Troubleshooting

### Error 1: UnicodeEncodeError

**Solución:** Configurar `PYTHONIOENCODING="utf-8"` (ver [Fix Crítico](#fix-crítico-encoding-utf-8-en-windows))

### Error 2: API Key not found

```powershell
# Verificar
echo $env:DEEPSEEK_API_KEY
```

### Error 3: Crash silencioso

**Causa:** Respuesta del modelo contiene emoji/caracteres especiales sin encoding fix.

**Solución:** Ver Fix Crítico arriba.

---

## 📚 Recursos Adicionales

- [DeepSeek Platform](https://platform.deepseek.com)
- [API Documentation](https://platform.deepseek.com/api-docs)
- [Pricing](https://platform.deepseek.com/pricing)

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur

**Token API de prueba (cambiar por el tuyo):**
```
sk-970bf433f35049b098d414a299ba59fc
```
