# Codex CLI (GPT-5.2)

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | 0.77.0+ |
| **Comando** | `codex` |
| **Región** | 🇺🇸 USA (OpenAI) |
| **Instalación** | npm global |
| **Autenticación** | Automática al primer uso |
| **Modelo** | GPT-5.2 (último de OpenAI) |

---

## 🚀 Instalación

### Requisitos Previos
- Node.js 18+
- Cuenta OpenAI (gratis para empezar)

### Instalación Global

```bash
npm install -g codex-cli
```

### Verificar Instalación

```bash
codex --version
# Salida esperada: 0.77.0 (o superior)
```

---

## 💻 Uso Básico

### Modo Batch (Recomendado para Automatización)

```bash
codex exec "Tu prompt aquí" --full-auto --skip-git-repo-check
```

**Flags críticos:**
- `exec` → Subcomando para ejecución
- `--full-auto` → Modo automático completo (lee, ejecuta, edita)
- `--skip-git-repo-check` → Bypasea validación de Git repo

### ⚠️ Sin `--skip-git-repo-check` fuera de repo Git

```bash
codex exec "prompt"
# Error: "Not in a Git repository"
```

**Solución:** SIEMPRE agregar `--skip-git-repo-check` si no estás en repo Git.

---

## 🔐 Modos de Permisos

| Modo | Leer | Ejecutar | Editar | Red |
|------|------|----------|--------|-----|
| **Default** (read-only) | ✅ | ⚠️ Sin side-effects | ❌ | ❌ |
| **`--full-auto`** | ✅ | ✅ | ✅ | ❌ |
| **`--sandbox danger-full-access`** | ✅ | ✅ | ✅ | ✅ |

**Recomendación:** Usar `--full-auto` para mayoría de casos (balance seguridad/funcionalidad).

---

## 📝 Ejemplos Prácticos

### Ejemplo 1: Consulta Simple

```bash
codex exec "Explica async/await en JavaScript" --full-auto --skip-git-repo-check
```

### Ejemplo 2: Generación de Código

```bash
codex exec "Crea función Python para ordenar lista de diccionarios por fecha" --full-auto --skip-git-repo-check
```

### Ejemplo 3: Análisis de Archivo

```bash
codex exec "Analiza el código en utils.py y sugiere mejoras" --full-auto
# (dentro de repo Git, no necesita --skip-git-repo-check)
```

---

## 📊 Formato de Respuestas

### JSON Limpio (Sin Decoración)

**Ventaja mayor:** Codex responde JSON **sin bloques markdown**:

```json
{
  "status": "OK",
  "resultado": "valor"
}
```

**NO requiere regex** para extraer JSON (a diferencia de Claude/Gemini).

**Parsing directo:**
```python
import json

response = codex_cli(prompt)
data = json.loads(response)  # ✅ Funciona directamente
```

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- **Automatización** (JSON limpio, confiable)
- **Generación de código** (GPT-5.2 excelente)
- **Scripts sin supervisión** (estable en batch)
- **Tareas que requieren ejecución** (con --full-auto)
- **Cuando otros CLIs tienen timeout** (rápido)

### ❌ No Recomendado Para:
- Tareas que requieren acceso a red (sin --sandbox danger-full-access)
- Análisis muy complejo (Claude es mejor)
- Perspectiva no-USA (usa Qwen/DeepSeek)

---

## 🔧 Límites y Cuotas

### Rate Limits

- **2000 llamadas diarias** (plan gratuito)
- Sin límite por hora (mejor que Qwen)

### Verificar Uso

```bash
codex quota
# Muestra llamadas restantes del día
```

---

## 🚀 Ventajas sobre Otros CLIs

| Característica | Codex | Claude Code | Gemini |
|----------------|-------|-------------|--------|
| JSON limpio | ✅ | ❌ | ❌ |
| Batch estable | ✅ | ✅ | ⚠️ |
| Velocidad | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Calidad código | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| Ejecución código | ✅ | ✅ | ❌ |

---

## 🔗 Integración con Round Table

Codex es **excelente** como ejecutor (M1) en sistemas multi-agente:

```python
# M1: Codex genera propuesta
m1_output = codex_exec(
    "Analiza datos y genera reporte JSON",
    full_auto=True,
    skip_git=True
)

# Parsing directo (sin regex)
data = json.loads(m1_output)

# M2: Gemini valida
m2_validation = gemini(f"Valida este análisis: {data}")
```

**Ventaja:** JSON limpio elimina errores de parsing.

---

## 🐛 Troubleshooting

### Error 1: "Not in a Git repository"

**Solución:** Agregar `--skip-git-repo-check`

### Error 2: "Permission denied"

**Causa:** Modo default no permite edición.

**Solución:** Usar `--full-auto`

### Error 3: Timeout

**Causa:** Tarea muy larga.

**Solución:** Codex es rápido, si timeout → problema de red o tarea imposible.

---

## 📚 Recursos Adicionales

- [Codex CLI GitHub](https://github.com/openai/codex-cli)
- [OpenAI Platform](https://platform.openai.com)
- [GPT-5.2 Documentation](https://platform.openai.com/docs/models/gpt-5)

---

## 🔬 Resultados en Pruebas Cognitivas

### Medieval Logic Puzzle Test

**Pendiente de ejecutar** (CLI instalado pero no usado en test original).

**Expectativa:** Excelente dado GPT-5.2 capabilities.

---

## 💡 Recomendación Estratégica

**Para automatización seria:** Codex CLI es **primera opción**.

**Razones:**
1. JSON limpio (sin parsing complejo)
2. Estable en batch (2000 llamadas/día)
3. GPT-5.2 (modelo potente)
4. Rápido (< timeouts de otros CLIs)
5. Ejecución de código integrada

**Trade-off:** Solo perspectiva USA (triangular con Qwen/DeepSeek para investigación).

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur

**Próximos pasos:** Ejecutar cognitive tests para comparar con Claude/Gemini.
