# 🤖 Guía de CLIs de IA en Español

> Documentación completa y práctica para trabajar con interfaces de línea de comandos (CLI) de modelos de lenguaje de última generación.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Estado: Activo](https://img.shields.io/badge/Estado-Activo-success.svg)]()
[![Idioma: Español](https://img.shields.io/badge/Idioma-Español-blue.svg)]()
[![CLIs: 7/7](https://img.shields.io/badge/CLIs-7%2F7_Completos-brightgreen.svg)]()
[![GitHub Pages](https://img.shields.io/badge/Sitio-GitHub_Pages-blue.svg)](https://krakaur.github.io/guia-cli-ia)
[![Tests](https://img.shields.io/badge/tests-passing-brightgreen.svg)]()
[![JOSS](https://img.shields.io/badge/JOSS-in_review-yellow.svg)](https://joss.theoj.org)

---

## 🎉 Los Magníficos 7 - COMPLETOS

**Primera guía completa en español** cubriendo los 7 CLIs más importantes para investigación y desarrollo con IA.

🌐 **Sitio Web:** [krakaur.github.io/guia-cli-ia](https://krakaur.github.io/guia-cli-ia)

📄 **Publicación Académica:** En revisión para [Journal of Open Source Software (JOSS)](https://joss.theoj.org)

---

## 📋 Tabla de Contenidos

- [Introducción](#introducción)
- [CLIs Cubiertos](#clis-cubiertos)
- [Instalación Rápida](#instalación-rápida)
- [Estructura del Repositorio](#estructura-del-repositorio)
- [Testing](#testing)
- [Casos de Uso](#casos-de-uso)
- [Cómo Citar](#cómo-citar)
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
- ✅ **Tests automatizados** que validan cada claim

---

## 🛠️ CLIs Cubiertos

### Los Magníficos 7 🎉

| # | CLI | Región | Estado | Documentación |
|---|-----|--------|--------|---------------|
| 1 | **Claude Code** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./claude-code/) |
| 2 | **Gemini CLI** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./gemini-cli/) |
| 3 | **GitHub Copilot CLI** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./copilot-cli/) |
| 4 | **DeepSeek CLI** | 🇨🇳 China | ✅ Operativo | [Ver guía](./deepseek-cli/) |
| 5 | **Qwen CLI** | 🇨🇳 China | ✅ Operativo | [Ver guía](./qwen-cli/) |
| 6 | **Codex CLI** (GPT-5.2) | 🇺🇸 USA | ✅ Operativo | [Ver guía](./codex-cli/) |
| 7 | **GitHub CLI** | 🇺🇸 USA | ✅ Operativo | [Ver guía](./github-cli/) |

**Perspectiva Geográfica:** Esta colección permite **triangular respuestas** de modelos entrenados en diferentes regiones (USA, China), reduciendo sesgos culturales en investigación académica.

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

## 📚 Recursos Adicionales

### 🌐 Sitio Web

Visita [krakaur.github.io/guia-cli-ia](https://krakaur.github.io/guia-cli-ia) para:
- Navegación optimizada
- SEO completo
- Búsqueda integrada
- Versión web-friendly

### 📄 Guías Especiales

- **[Comparativa de CLIs](./troubleshooting/comparativa-clis.md)** - ¿Cuándo usar qué?
- **[Casos Reales](./troubleshooting/casos-reales.md)** - Problemas documentados y soluciones
- **[Integración MCP](./troubleshooting/integracion-mcp.md)** - Uso con Model Context Protocol

---

## 📚 Estructura del Repositorio

```
guia-cli-ia/
├── README.md                    # Este archivo
├── CONTRIBUTING.md              # Guía de contribución
├── CODE_OF_CONDUCT.md           # Código de conducta
├── CITATION.cff                 # Metadata para citaciones
├── docs/                        # Sitio GitHub Pages
│   ├── index.md                 # Landing page
│   ├── claude-code.md
│   ├── gemini-cli.md
│   ├── copilot-cli.md
│   ├── deepseek-cli.md
│   ├── qwen-cli.md
│   ├── codex-cli.md
│   ├── github-cli.md
│   ├── comparativa.md
│   └── troubleshooting.md
├── tests/                       # Test suite automatizado
│   ├── test_cli_validation.py   # Tests de validación
│   └── README.md                # Documentación de tests
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

## 🧪 Testing

Este proyecto incluye un **test suite automatizado** que valida:

✅ Instalación correcta de los 7 CLIs  
✅ Comportamientos documentados (ej: Gemini es stateless, DeepSeek requiere UTF-8)  
✅ Compatibilidad con workflows multi-agente (patrón M1-M2)  
✅ Triangulación geográfica USA/China  

### Ejecutar Tests

```bash
# Instalar dependencias
pip install -r requirements.txt

# Ejecutar todos los tests
pytest

# Tests específicos
pytest tests/test_cli_validation.py -v

# Ver documentación completa
cat tests/README.md
```

**Filosofía de testing:** Los tests NO consumen APIs reales, validando solo instalación y comportamiento documentado. Esto permite CI/CD sin rate limits.

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

## 📚 Cómo Citar

Si usas esta guía en tu investigación o trabajo, por favor cítala:

### BibTeX

```bibtex
@software{krakaur_guia_clis_ia_2026,
  author = {Krakaur, Hans (Wintermute)},
  title = {Guía de CLIs de IA en Español: Documentación Práctica con Triangulación Geográfica},
  year = {2026},
  publisher = {GitHub},
  journal = {Journal of Open Source Software},
  url = {https://github.com/Krakaur/guia-cli-ia},
  doi = {10.XXXX/joss.XXXXX},
  note = {In review for JOSS}
}
```

### APA 7th Edition

```
Krakaur, H. (2026). Guía de CLIs de IA en Español: Documentación Práctica con 
    Triangulación Geográfica [Computer software]. Journal of Open Source Software. 
    https://github.com/Krakaur/guia-cli-ia
```

### IEEE

```
H. Krakaur, "Guía de CLIs de IA en Español: Documentación Práctica con Triangulación 
Geográfica," Journal of Open Source Software, 2026. [Online]. Available: 
https://github.com/Krakaur/guia-cli-ia
```

**Nota:** El DOI será asignado tras aceptación en JOSS. Esta sección se actualizará con el DOI oficial.

---

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Este proyecto sigue estándares de código abierto rigurosos.

### Antes de Contribuir

Por favor lee:
- 📋 **[Guía de Contribución](CONTRIBUTING.md)** - Proceso detallado, estándares, ejemplos
- 🤝 **[Código de Conducta](CODE_OF_CONDUCT.md)** - Normas de la comunidad

### Tipos de Contribuciones Bienvenidas

- ✨ Nuevos CLIs para documentar
- 🐛 Correcciones o mejoras a documentación existente
- 🧪 Tests adicionales
- 📝 Traducciones a otros idiomas
- 💡 Casos de uso adicionales
- 🔧 Soluciones a problemas (troubleshooting)

### Proceso Rápido

1. **Fork** el repositorio
2. **Crea una rama** (`git checkout -b feature/nueva-cli`)
3. **Haz tus cambios** (siguiendo [CONTRIBUTING.md](CONTRIBUTING.md))
4. **Ejecuta tests** (`pytest`)
5. **Commit** (`git commit -m 'Agregar documentación de X'`)
6. **Push** (`git push origin feature/nueva-cli`)
7. **Abre un Pull Request**

**Tiempo típico de review:** 2-5 días

### Reporte de Issues

Encontraste un problema? [Abre un issue](https://github.com/Krakaur/guia-cli-ia/issues/new) con:
- Descripción clara del problema
- Pasos para reproducir
- Sistema operativo y versión de CLI
- Comportamiento esperado vs. observado

---

## 📜 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para detalles.

**En resumen:** Puedes usar, modificar y distribuir este proyecto libremente, incluso para uso comercial, siempre que mantengas el aviso de copyright.

---

## 👤 Autor

**Dr. Hans Krakaur (Wintermute)**
- Estudiante Doctoral en DSAE, Universidad de Guadalajara
- Investigación: Sistemas Multi-Agente, IA para Sustentabilidad
- GitHub: [@Krakaur](https://github.com/Krakaur)
- Sitio: [krakaur.github.io/guia-cli-ia](https://krakaur.github.io/guia-cli-ia)

---

## 🚀 Proyecto Round Table

Esta documentación fue desarrollada como parte del proyecto **Round Table** para orquestación de sistemas multi-agente en investigación académica.

**Otros proyectos relacionados:**
- [RoundTable MCP Server](https://sala.krakaurcorp.uk/mcp) - Servidor MCP para memoria persistente
- [Paper-Search MCP](https://academic.krakaurcorp.uk/mcp) - Búsqueda académica

---

## 📞 Contacto

¿Preguntas? ¿Sugerencias? 

- 💬 [Abre un issue](https://github.com/Krakaur/guia-cli-ia/issues)
- 📧 [Inicia una discusión](https://github.com/Krakaur/guia-cli-ia/discussions)
- 👥 Consulta [CONTRIBUTING.md](CONTRIBUTING.md) para guías de contribución

---

## 🌟 Agradecimientos

Gracias a todos los que han contribuido a hacer la IA más accesible para la comunidad hispanohablante de **577 millones de personas**.

**⭐ Si esta guía te resulta útil, considera darle una estrella al repositorio!**

---

*Última actualización: 2026-01-03 | Versión: 1.0 | Estado: En revisión JOSS*
