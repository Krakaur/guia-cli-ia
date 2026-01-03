---
layout: page
title: Codex CLI (GPT-5.2) - Mejor para Automatización
description: Guía completa de Codex CLI destacando JSON limpio y estabilidad en batch - ideal para automatización
keywords: codex cli, gpt-5.2, json limpio, automatización ia, batch processing
permalink: /codex-cli/
---

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

## 📏 Modos de Permisos

| Modo | Leer | Ejecutar | Editar | Red |
|------|------|----------|--------|-----|
| **Default** (read-only) | ✅ | ⚠️ Sin side-effects | ❌ | ❌ |
| **`--full-auto`** | ✅ | ✅ | ✅ | ❌ |
| **`--sandbox danger-full-access`** | ✅ | ✅ | ✅ | ✅ |

**Recomendación:** Usar `--full-auto` para mayoría de casos (balance seguridad/funcionalidad).

---

## 🏆 Ventaja Mayor: JSON Limpio

**Codex responde JSON SIN decoración markdown:**

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

## 🚀 Ventajas sobre Otros CLIs

| Característica | Codex | Claude Code | Gemini |
|----------------|-------|-------------|--------|
| JSON limpio | ✅ | ❌ | ❌ |
| Batch estable | ✅ | ✅ | ⚠️ |
| Velocidad | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Calidad código | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| Ejecución código | ✅ | ✅ | ❌ |

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

## 📚 Ver También

- [Comparativa](comparativa.html) - Codex #1 para automatización
- [Claude Code](claude-code.html) - Alternativa para análisis profundo
- [GitHub Repository](https://github.com/Krakaur/guia-cli-ia)

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur