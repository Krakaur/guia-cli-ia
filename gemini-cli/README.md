# Gemini CLI

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | 0.22.4+ |
| **Comando** | `gemini` |
| **Región** | 🇺🇸 USA (Google) |
| **Instalación** | npm global |
| **Autenticación** | API Key de Google AI Studio |
| **Costo** | Gratuito (con límites) |

---

## 🚀 Instalación

### Paso 1: Obtener API Key

1. Ve a [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Crea un proyecto (si no tienes uno)
3. Genera API Key
4. Copia y guarda el key

### Paso 2: Instalar CLI

```bash
npm install -g @google/generative-ai-cli
```

### Paso 3: Configurar API Key

```bash
# Windows PowerShell (permanente)
[Environment]::SetEnvironmentVariable("GEMINI_API_KEY", "tu-api-key-aqui", "User")

# Linux/Mac
echo 'export GEMINI_API_KEY="tu-api-key-aqui"' >> ~/.bashrc
source ~/.bashrc
```

### Verificar Instalación

```bash
gemini --version
# Salida esperada: 0.22.4 (o superior)
```

---

## 💻 Uso Básico

### ⚠️ IMPORTANTE: Sintaxis Sin Flag `-p`

```bash
# ✅ CORRECTO
gemini "Tu prompt aquí"

# ❌ INCORRECTO (obsoleto)
gemini -p "Tu prompt"
```

**Nota crítica:** La sintaxis `gemini -p` fue **deprecada**. Siempre usa el formato sin flag.

---

## 📝 Ejemplos Prácticos

### Ejemplo 1: Consulta Simple

```bash
gemini "¿Cuál es la capital de Francia?"
```

### Ejemplo 2: Análisis de Texto

```bash
gemini "Resume este texto en 3 puntos: $(cat articulo.txt)"
```

### Ejemplo 3: Generación de Código

```bash
gemini "Escribe una función Python que ordene una lista de diccionarios por fecha"
```

---

## 🔧 Configuración y Limitaciones

### Límite de Longitud de Prompts

**Problema:** Prompts >500 caracteres activan modo interactivo (espera confirmación).

**Para automatización (scripts), mantén prompts <200 caracteres:**

```bash
# ✅ Prompt corto (automático)
gemini "Traduce 'Hello' al español"

# ❌ Prompt largo (pedirá confirmación)
gemini "Analiza este documento completo y genera un reporte detallado con introducción, metodología, resultados y conclusiones..."
```

**Solución para prompts largos:**
Usar archivo temporal + stdin:

```powershell
$prompt = "Prompt muy largo..."
$prompt | Out-File -FilePath temp.txt -Encoding UTF8
Get-Content temp.txt | gemini
Remove-Item temp.txt
```

---

## 🔄 Característica STATELESS

### Importante para Multi-Agente

Gemini CLI es **completamente stateless** (sin memoria entre llamadas):

```bash
# Llamada 1
gemini "Mi nombre es Juan"
# Respuesta: "Hola Juan, ¿en qué puedo ayudarte?"

# Llamada 2 (en el mismo terminal)
gemini "¿Cuál es mi nombre?"
# Respuesta: "No tengo información sobre tu nombre"
```

**Implicaciones:**
- ✅ Cada llamada es independiente (predecible)
- ✅ No hay "contaminación" de contexto
- ❌ Debes incluir contexto completo en cada prompt

**Para mantener contexto:**
```bash
# Incluir contexto explícitamente
gemini "Dado que mi nombre es Juan, ¿cuál es mi nombre?"
```

---

## ⏱️ Timeouts y Latencia

### Configuración Recomendada

```powershell
# Timeout mínimo recomendado: 60 segundos
$timeout = 60000  # ms

# Latencia observada: 15-68 segundos
# Promedio: ~30 segundos
```

**Nota:** Gemini puede tener latencia variable. Siempre configurar timeouts generosos.

---

## 🧹 Protocolo de Higiene (Multi-Agente)

### Problema: Procesos Huérfanos

Gemini puede dejar procesos huérfanos que consumen recursos.

### Solución: Limpieza Sistemática

**ANTES de cada llamada:**
```powershell
# Via Round Table MCP
list_sessions()  # Ver procesos activos
force_terminate(pid)  # Matar huérfanos
```

**DESPUÉS de cada llamada (SIEMPRE):**
```powershell
# Incluso si la llamada fue exitosa
force_terminate($pid)
```

---

## 📊 Formato de Respuestas

### JSON con Bloques Markdown

Gemini suele decorar JSON con markdown:

```markdown
```json
{
  "resultado": "valor"
}
```
```

**Parsing requerido:**

```python
import re

def extract_json_gemini(text):
    # Estrategia 1: Buscar bloque markdown
    match = re.search(r'```json\s*(.*?)\s*```', text, re.DOTALL)
    if match:
        return match.group(1)
    
    # Estrategia 2: Buscar primer { hasta último }
    first = text.find('{')
    last = text.rfind('}')
    if first != -1 and last != -1:
        return text[first:last+1]
    
    return text
```

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- Validación rápida de respuestas (modo crítico)
- Consultas simples y directas
- Análisis de texto corto
- Traducción de idiomas
- Resúmenes concisos

### ❌ No Recomendado Para:
- Tareas que requieren memoria de sesión
- Análisis de documentos muy largos
- Procesamiento batch de >10 archivos sin limpieza
- Tareas que requieren ejecución de código

---

## 🔗 Integración con Round Table MCP

Gemini funciona excelentemente como **modelo crítico (M2)** en sistemas multi-agente:

```python
# Ejemplo: M1 propone, M2 (Gemini) valida
m1_output = claude_code("Genera análisis de datos")
m2_validation = gemini(f"Valida este análisis: {m1_output}")

if "APROBADO" in m2_validation:
    save_result(m1_output)
```

---

## ⚠️ Errores Comunes

### Error 1: "API Key not found"

```bash
# Verificar variable de entorno
echo $env:GEMINI_API_KEY  # PowerShell
echo $GEMINI_API_KEY      # Bash
```

**Solución:** Configurar key (ver Paso 3 arriba)

### Error 2: Output Vacío

**Causa:** Gemini respondió pero `read_process_output` retorna vacío.

**Solución:** **JAMÁS** reintentar. Usar `force_terminate` y reportar.

### Error 3: Modo Interactivo Inesperado

**Causa:** Prompt >500 caracteres.

**Solución:** Acortar prompt o usar archivo temporal.

---

## 📚 Recursos Adicionales

- [Google AI Studio](https://makersuite.google.com)
- [Gemini API Docs](https://ai.google.dev)
- [Rate Limits](https://ai.google.dev/pricing)

---

## 🐛 Troubleshooting

Ver [troubleshooting/casos-reales.md](../troubleshooting/casos-reales.md) para debugging avanzado.

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur
