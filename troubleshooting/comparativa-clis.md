# Comparativa de CLIs: ¿Cuándo Usar Qué?

Esta guía te ayuda a elegir el CLI correcto según tu tarea específica, basada en **experiencia real** de meses de uso intensivo.

---

## 📊 Tabla Comparativa Rápida

| CLI | Región | Mejor Para | Evitar Para | Batch Estable | JSON Limpio |
|-----|--------|------------|-------------|---------------|-------------|
| **Claude Code** | 🇺🇸 | Análisis profundo, código complejo | Tareas simples (sobrecalificado) | ✅ | ❌ |
| **Gemini** | 🇺🇸 | Validación rápida, crítico M2 | Batch largo sin limpieza | ⚠️ | ❌ |
| **Copilot** | 🇺🇸 | Acceso a 13 modelos, comparación | Automatización sin activación previa | ⚠️ | ❌ |
| **DeepSeek** | 🇨🇳 | Backup rápido, perspectiva china | Windows sin UTF-8 fix | ✅ | ❌ |
| **Qwen** | 🇨🇳 | Consultas individuales, triangulación | **Batch automatizado** | ❌ | ✅ |
| **Codex** | 🇺🇸 | **Automatización seria**, scripts | Perspectiva no-USA | ✅ | ✅ |

---

## 🎯 Casos de Uso Específicos

### 1. Automatización de Procesamiento Batch (20+ archivos)

**Primera opción:** 🥇 **Codex CLI**
- JSON limpio (sin parsing complejo)
- Estable en 2000 llamadas
- Rápido y confiable

**Segunda opción:** 🥈 **Claude Code**
- Excelente calidad
- Requiere parsing de JSON
- Más lento que Codex

**NO usar:** ❌ Qwen (se cuelga), Copilot (requiere activación)

---

### 2. Sistema Multi-Agente (M1 Ejecutor + M2 Crítico)

**M1 (Ejecutor):**
- 🥇 Claude Code - Mejor razonamiento
- 🥈 Codex - Más rápido

**M2 (Crítico/Validador):**
- 🥇 **Gemini** - Rápido, stateless (perfecto para validación)
- 🥈 Claude Code - Más exhaustivo pero lento

**NO usar como M2:** ❌ Qwen (problemas de estabilidad)

**Ejemplo comprobado:**
```python
# Arquitectura probada en RoundTable Messenger
M1 = Claude Code  # Genera propuesta
M2 = Gemini       # Valida rápidamente
# Resultado: 100% éxito en 92 PDFs
```

---

### 3. Investigación Académica - Triangulación Geográfica

**Objetivo:** Reducir sesgos regionales comparando perspectivas.

**Configuración recomendada:**

| Perspectiva | CLI | Uso |
|-------------|-----|-----|
| 🇺🇸 USA | Claude Code | Análisis primario |
| 🇺🇸 USA (alternativo) | Codex/Copilot | Verificación |
| 🇨🇳 China | DeepSeek | Contrapunto cultural |
| 🇨🇳 China (alt) | Qwen | **Solo consultas individuales** |

**Workflow:**
```bash
# 1. Análisis USA
us_analysis=$(claude -p "$research_question" --allowedTools "")

# 2. Perspectiva China
cn_analysis=$(deepseek -q "$research_question" -r)

# 3. Comparar diferencias
python compare_perspectives.py us_analysis cn_analysis
```

---

### 4. Desarrollo de Software - Generación de Código

**Primera opción:** 🥇 **Codex CLI (GPT-5.2)**
- Especializado en código
- Ejecución integrada (--full-auto)
- JSON limpio para CI/CD

**Segunda opción:** 🥈 **Claude Code**
- Mejor explicaciones
- Más creativo

**Para código de infraestructura China:** 🇨🇳 DeepSeek Coder

---

### 5. Consultas Rápidas Interactivas

**Primera opción:** 🥇 **Copilot CLI (modo interactivo)**
- Cambio de modelo on-the-fly (/model)
- Acceso a 13 modelos
- Interface amigable

**Segunda opción:** 🥈 **Claude Code (modo interactivo)**
- Mejor conversación
- Memoria de sesión

---

### 6. Debugging de Errores Complejos

**Primera opción:** 🥇 **Claude Code**
- Razonamiento más profundo
- Mejor análisis de stack traces
- Contexto más amplio

**Backup si timeout:** 🥈 DeepSeek
- Más rápido
- Suficiente para errores simples

---

## ⚡ Matriz de Velocidad vs Calidad

```
Alta Calidad
    ↑
    │     Claude Code
    │         ●
    │                Codex
    │                  ●
    │
    │              Gemini
    │                ●
    │
    │         DeepSeek
    │            ●
    │
    │                     Qwen
    │                       ●
    └─────────────────────────────→
                              Rápido
```

**Interpretación:**
- **Necesitas lo mejor:** Claude Code (acepta esperar)
- **Balance:** Codex (rápido + calidad)
- **Solo rapidez:** Gemini/DeepSeek

---

## 🧪 Resultados de Pruebas Cognitivas

### Medieval Logic Puzzle Test (Diciembre 2025)

| CLI | Resultado | Tiempo | Consenso |
|-----|-----------|--------|----------|
| Claude Code | Sir Richard ✅ | ~45s | 6/7 |
| Gemini | Sir Richard ✅ | ~30s | 6/7 |
| Copilot (GPT-4o) | Sir Richard ✅ | ~25s | 6/7 |
| DeepSeek | Sir Richard ✅ | ~20s | 6/7 |
| Qwen | No probado | - | - |
| Codex | No probado | - | - |

**Conclusión:** Todos llegan a respuesta correcta, diferencia está en velocidad.

---

## 💰 Consideraciones de Costo

### Gratis con Límites

| CLI | Límite Diario | Método Auth |
|-----|---------------|-------------|
| Claude Code | ~ (rate limited) | claude.ai account |
| Gemini | ~ (rate limited) | API key gratis |
| Copilot | ∞ | Student Pack (gratis) |
| DeepSeek | ~ (rate limited) | API key |
| Qwen | 2000 llamadas | OAuth |
| Codex | 2000 llamadas | OpenAI account |

**Para uso académico:** Todos suficientes si distribuyes carga.

---

## 🛠️ Facilidad de Instalación

| CLI | Instalación | Complejidad | Problemas Comunes |
|-----|-------------|-------------|-------------------|
| Claude Code | npm | ⭐ Fácil | Ninguno |
| Gemini | npm | ⭐ Fácil | Ninguno |
| Copilot | npm | ⭐⭐ Media | Activación modelos premium |
| DeepSeek | pip | ⭐⭐⭐ Difícil | **UTF-8 encoding** |
| Qwen | npm | ⭐ Fácil | OAuth inicial |
| Codex | npm | ⭐⭐ Media | Git repo check |

**Más fácil empezar:** Gemini o Claude Code

---

## 📝 Recomendaciones Finales por Perfil

### Para Estudiantes / Principiantes
1. **Gemini** - Gratis, fácil, rápido
2. Claude Code - Aprende con mejores explicaciones
3. Copilot - Experimenta con muchos modelos

### Para Investigadores
1. **Claude Code** - Análisis profundo
2. **Gemini** - Validación
3. **DeepSeek** - Perspectiva china
4. Codex - Automatización de análisis

### Para Developers
1. **Codex** - Generación de código
2. Claude Code - Debugging complejo
3. Copilot - CI/CD integration

### Para Automatización / DevOps
1. **Codex** - Primera opción (JSON limpio)
2. Claude Code - Tareas complejas
3. Gemini - Validación rápida

---

## ⚠️ Errores Comunes de Selección

### ❌ ERROR 1: Usar Qwen para batch largo
**Problema:** Se cuelga después de ~10 archivos
**Solución:** Usar Gemini o Codex

### ❌ ERROR 2: Usar Copilot premium en batch sin activar
**Problema:** Error "Run in interactive mode"
**Solución:** Activar modelo interactivamente primero, O usar GPT-4o

### ❌ ERROR 3: Usar DeepSeek sin UTF-8 fix
**Problema:** Crash con emojis
**Solución:** `$env:PYTHONIOENCODING="utf-8"`

### ❌ ERROR 4: Usar Claude para tareas triviales
**Problema:** Lento e innecesario
**Solución:** Usar Gemini para validaciones simples

---

## 🎓 Lección Principal

**No existe "el mejor CLI".**

Existe el CLI correcto para **tu tarea específica**:

- 📚 **Profundidad:** Claude Code
- ⚡ **Velocidad:** Gemini/DeepSeek
- 🤖 **Automatización:** Codex
- 🌍 **Triangulación:** USA (Claude) + China (DeepSeek)
- 🧪 **Experimentación:** Copilot (13 modelos)

**Usa la herramienta correcta para el trabajo.**

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur

**Feedback:** Si descubres nuevos casos de uso, comparte en [Discussions](https://github.com/Krakaur/guia-cli-ia/discussions)
