# 🤖 Guía de CLIs de IA en Español

> Documentación completa y práctica para trabajar con interfaces de línea de comandos (CLI) de modelos de lenguaje de última generación.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Estado: Activo](https://img.shields.io/badge/Estado-Activo-success.svg)]()
[![Idioma: Español](https://img.shields.io/badge/Idioma-Español-blue.svg)]()

---

## 📋 Tabla de Contenidos

- [Introducción](#introducción)
- [CLIs Cubiertos](#clis-cubiertos)
- [Instalación Rápida](#instalación-rápida)
- [Estructura del Repositorio](#estructura-del-repositorio)
- [Contribuir](#contribuir)
- [Licencia](#licencia)

---

## 🎯 Introducción

Esta guía nace de **meses de experiencia práctica** trabajando con múltiples CLIs de IA para investigación académica y desarrollo de sistemas multi-agente. A diferencia de documentación oficial que puede ser incompleta o estar en inglés, aquí encontrarás:

- ✅ **Instrucciones probadas empíricamente** en Windows 11
- ✅ **Soluciones a problemas reales** documentados
- ✅ **Comparativas de rendimiento** entre modelos
- ✅ **Casos de uso prácticos** para investigación y desarrollo
- ✅ **Todo en español** 🇪🇸 🇲🇽

---

## 🛠️ CLIs Cubiertos

| CLI | Región | Estado | Documentación |
|-----|--------|--------|---------------|
| **Claude Code** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./claude-code/) |
| **Gemini CLI** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./gemini-cli/) |
| **GitHub Copilot CLI** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./copilot-cli/) |
| **DeepSeek CLI** | 🇨🇳 China | ✅ Operativo | [Ver guía](./deepseek-cli/) |
| **Qwen CLI** | 🇨🇳 China | ✅ Operativo | [Ver guía](./qwen-cli/) |
| **Codex CLI** (GPT-5.2) | 🇺🇸 USA | ✅ Operativo | [Ver guía](./codex-cli/) |
| **GitHub CLI** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./github-cli/) |

**Perspectiva Geográfica:** Esta colección permite **triangular respuestas** de modelos entrenados en diferentes regiones (USA, Europa, China), reduciendo sesgos culturales en investigación académica.

---

## ⚡ Instalación Rápida

### Requisitos Previos
- **Windows 11** (mayoría de comandos)
- **PowerShell 5.1+**
- **Node.js 18+** (para CLIs basados en npm)
- **Python 3.10+** (para CLIs basados en pip)

### Instalación por CLI

Consulta la guía específica de cada CLI en su carpeta correspondiente:

```bash
# Ejemplo: Claude Code
npm install -g @anthropic-ai/claude-code

# Ejemplo: Gemini CLI
npm install -g @google/generative-ai-cli

# Ver guías completas en carpetas individuales
```

---

## 📁 Estructura del Repositorio

```
guia-cli-ia/
├── README.md                    # Este archivo
├── claude-code/
│   ├── README.md               # Guía completa Claude Code
│   ├── ejemplos/               # Ejemplos de uso
│   └── troubleshooting.md      # Problemas comunes
├── gemini-cli/
│   ├── README.md
│   ├── configuracion.md
│   └── limitaciones.md
├── copilot-cli/
│   ├── README.md
│   ├── modelos-disponibles.md
│   └── autenticacion.md
├── deepseek-cli/
│   ├── README.md
│   └── encoding-utf8.md       # Fix crítico para Windows
├── qwen-cli/
│   └── README.md
├── codex-cli/
│   └── README.md
├── github-cli/
│   └── README.md
└── troubleshooting/
    ├── casos-reales.md         # Casos de depuración documentados
    ├── comparativa-clis.md     # Cuándo usar qué CLI
    └── integracion-mcp.md      # Integración con Model Context Protocol
```

---

## 🎓 Casos de Uso

### Investigación Académica
- Revisión de literatura con múltiples perspectivas
- Análisis comparativo de respuestas por región
- Generación de código para análisis de datos

### Desarrollo de Software
- Integración de IA en pipelines de desarrollo
- Automatización de tareas repetitivas
- Generación de documentación técnica

### Sistemas Multi-Agente
- Orquestación de múltiples modelos
- Validación cruzada de resultados
- Reducción de alucinaciones mediante triangulación

---

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Si tienes:

- ✨ Nuevos CLIs para documentar
- 🐛 Correcciones o mejoras
- 📝 Traducciones a otros idiomas
- 💡 Casos de uso adicionales

Por favor:
1. Fork el repositorio
2. Crea una rama (`git checkout -b feature/nueva-cli`)
3. Commit tus cambios (`git commit -m 'Agregar documentación de X'`)
4. Push a la rama (`git push origin feature/nueva-cli`)
5. Abre un Pull Request

---

## 📜 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para detalles.

---

## 👤 Autor

**Dr. Hans Krakaur (Wintermute)**
- Estudiante Doctoral en DSAE, Universidad de Guadalajara
- Investigación: Sistemas Multi-Agente, IA para Sustentabilidad
- GitHub: [@Krakaur](https://github.com/Krakaur)

---

## 🙏 Agradecimientos

Esta documentación fue desarrollada como parte del proyecto **Round Table** para orquestación de sistemas multi-agente en investigación académica.

---

## 📞 Contacto

¿Preguntas? ¿Sugerencias? Abre un [issue](https://github.com/Krakaur/guia-cli-ia/issues) o inicia una [discusión](https://github.com/Krakaur/guia-cli-ia/discussions).

---

**⭐ Si esta guía te resulta útil, considera darle una estrella al repositorio!**
