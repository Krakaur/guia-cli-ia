# Qwen CLI

## 📋 Información General

| Atributo | Valor |
|----------|-------|
| **Versión** | 0.6.0+ |
| **Comando** | `qwen` |
| **Región** | 🇨🇳 China (Alibaba Cloud) |
| **Instalación** | npm/pip |
| **Autenticación** | OAuth (2000 llamadas diarias gratis) |
| **Costo** | Gratuito (con límites) |

---

## 🚀 Instalación

### Via npm (Recomendado)

```bash
npm install -g qwen-cli
```

### Verificar Instalación

```bash
qwen --version
# Salida esperada: 0.6.0 (o superior)
```

### Autenticación OAuth

```bash
qwen login
# Abre navegador para autorizar
# 2000 llamadas diarias gratuitas
```

---

## 💻 Uso Básico

### Sintaxis

```bash
qwen -p "Tu prompt aquí"
```

**Flags importantes:**
- `-p, --prompt` → El prompt (modo batch)

---

## 📝 Ejemplos Prácticos

### Ejemplo 1: Consulta Simple

```bash
qwen -p "¿Qué es inteligencia artificial?"
```

### Ejemplo 2: Generación de Código

```bash
qwen -p "Escribe función Python para calcular factorial"
```

### Ejemplo 3: Análisis de Texto

```bash
qwen -p "Resume en 3 puntos: $(cat documento.txt)"
```

---

## ⚠️ PROBLEMA CRÍTICO: No Usar en Batch Largo

### Síntoma

Qwen CLI se **cuelga indefinidamente** en procesamiento batch largo (>10 archivos):

```bash
qwen -p "Analiza documento..."
# Exit code: 4294967295
# Proceso queda esperando indefinidamente
```

### Causa

Qwen CLI tiene problemas de gestión de procesos en Windows PowerShell cuando se ejecuta repetidamente.

### Recomendación

**NO USAR** Qwen como modelo crítico (M2) en sistemas multi-agente con >10 iteraciones.

**Alternativas recomendadas:**
- ✅ **Gemini** - Más estable para batch largo
- ✅ **Codex** - Excelente para automatización
- ✅ **DeepSeek** - Backup rápido

---

## 📊 Formato de Respuestas

### JSON Limpio

Qwen suele responder JSON **sin decoración markdown** (mejor que otros CLIs):

```json
{
  "resultado": "valor"
}
```

**Ventaja:** Parsing más sencillo que Claude/Gemini.

---

## 🎯 Casos de Uso Recomendados

### ✅ Ideal Para:
- Perspectiva china en investigación (triangulación geográfica)
- Consultas individuales (no batch)
- Comparación de respuestas por región
- Tareas donde calidad > velocidad

### ❌ No Recomendado Para:
- **Procesamiento batch automatizado** (se cuelga)
- Sistemas multi-agente como modelo crítico
- Tareas que requieren >10 llamadas consecutivas
- Scripts sin supervisión humana

---

## 🌍 Valor en Triangulación Geográfica

Qwen representa la **perspectiva china** en análisis comparativo:

```python
# Ejemplo: Triangular respuestas por región
us_response = claude_code("¿Cuál es la situación de X?")
cn_response = qwen_cli("¿Cuál es la situación de X?")

# Comparar sesgos regionales
compare_perspectives(us_response, cn_response)
```

**Utilidad académica:** Reducir bias regional en investigación.

---

## 🔧 Configuración

### Límites de API

- 2000 llamadas diarias gratuitas
- Rate limiting después de 100 llamadas/hora

### Verificar Cuota

```bash
qwen quota
# Muestra llamadas restantes del día
```

---

## 🐛 Troubleshooting

### Error 1: Exit Code 4294967295

**Causa:** Proceso colgado (ver [Problema Crítico](#problema-crítico-no-usar-en-batch-largo))

**Solución:** Usar Gemini o Codex en su lugar para batch.

### Error 2: OAuth token expirado

```bash
# Re-autenticar
qwen login
```

### Error 3: Rate limit excedido

**Síntoma:** "Too many requests"

**Solución:** Esperar reset (cada 24 horas a medianoche UTC+8)

---

## 📚 Recursos Adicionales

- [Qwen Platform](https://qwen.aliyun.com)
- [API Documentation](https://help.aliyun.com/zh/dashscope/)
- [Model Info](https://github.com/QwenLM/Qwen)

---

## 🔬 Resultados en Pruebas Cognitivas

### Medieval Logic Puzzle Test

**No ejecutado** en batch debido a problemas de estabilidad.

**Recomendación:** Usar solo para consultas individuales supervisadas.

---

**Última actualización:** Enero 2026
**Autor:** Dr. Hans Krakaur

**Nota:** Qwen es **excelente** para perspectiva china, pero **NO confiable** para automatización batch en Windows.
