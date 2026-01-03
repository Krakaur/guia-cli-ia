---
layout: page
title: Gemini CLI - Guía Completa en Español
description: Tutorial de Gemini CLI con sintaxis correcta, troubleshooting y casos de uso reales
keywords: gemini cli, google ai, tutorial español, stateless cli
permalink: /gemini-cli/
---

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

---

## 🧹 Protocolo de Higiene (Multi-Agente)

### Problema: Procesos Huérfanos

Gemini puede dejar procesos huérfanos que consumen recursos.

### Solución: Limpieza Sistemática

**ANTES de cada llamada:**
- Verificar procesos activos
- Matar huérfanos

**DESPUÉS de cada llamada (SIEMPRE):**
- Terminar proceso explícitamente

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

## 📚 Ver También

- [Comparativa](comparativa.html) - ¿Cuándo usar Gemini vs otros?
- [Troubleshooting](troubleshooting.html) - Output vacío, timeouts
- [Claude Code](claude-code.html) - Alternativa para análisis profundo

---

**Última actualización:** Enero 2026  
**Autor:** Dr. Hans Krakaur