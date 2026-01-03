# Contribuir a Guía CLIs de IA

¡Gracias por tu interés en contribuir a este proyecto! Esta guía está diseñada para servir a la comunidad hispanohablante de 577 millones de personas, y cada contribución nos ayuda a mejorarla.

## 📋 Tabla de Contenidos

- [Código de Conducta](#código-de-conducta)
- [Cómo Puedo Contribuir](#cómo-puedo-contribuir)
  - [Reportar Problemas](#reportar-problemas)
  - [Sugerir Mejoras](#sugerir-mejoras)
  - [Agregar Nueva CLI](#agregar-nueva-cli)
  - [Mejorar Documentación](#mejorar-documentación)
- [Estándares del Proyecto](#estándares-del-proyecto)
- [Proceso de Pull Request](#proceso-de-pull-request)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Ejecutar Tests](#ejecutar-tests)

---

## 📜 Código de Conducta

Este proyecto sigue nuestro [Código de Conducta](CODE_OF_CONDUCT.md). Al participar, te comprometes a mantener un ambiente acogedor y respetuoso para todos.

---

## 🤝 Cómo Puedo Contribuir

### Reportar Problemas

Si encuentras un bug, error en la documentación, o comportamiento inesperado:

1. **Verifica** que el problema no esté ya reportado en [Issues](https://github.com/Krakaur/guia-cli-ia/issues)
2. **Crea un nuevo issue** con:
   - Título descriptivo
   - Pasos para reproducir el problema
   - Comportamiento esperado vs. observado
   - Sistema operativo y versión de CLI
   - Capturas de pantalla si aplica

**Template de Issue:**
```markdown
## Descripción
[Describe el problema brevemente]

## Pasos para Reproducir
1. Ejecutar comando: `gemini "test"`
2. Observar error: ...

## Comportamiento Esperado
[Qué debería pasar]

## Comportamiento Actual
[Qué está pasando]

## Entorno
- OS: Windows 11 / macOS 14 / Ubuntu 22.04
- CLI: Gemini v0.22.4
- PowerShell / Bash / Zsh
```

### Sugerir Mejoras

¿Tienes ideas para mejorar la guía?

1. **Abre un issue** con tag `enhancement`
2. **Describe** el problema que resolverías
3. **Propón** tu solución
4. **Discute** con la comunidad antes de implementar

**Ejemplos de mejoras bienvenidas:**
- 🌍 Nuevas CLIs de IA
- 📝 Casos de uso adicionales
- 🔧 Troubleshooting de problemas comunes
- 🎨 Mejoras a la documentación web
- 🧪 Nuevos tests

### Agregar Nueva CLI

¿Quieres documentar una nueva CLI de IA?

**Requisitos:**
1. CLI debe estar disponible públicamente
2. Documentación basada en **experiencia empírica** (no traducción de docs oficiales)
3. Al menos 3 casos de uso reales
4. Troubleshooting de 2+ problemas comunes
5. Tests automatizados

**Proceso:**
1. Crea issue: "[Nueva CLI] Nombre de la CLI"
2. Espera aprobación del maintainer
3. Sigue estructura de documentación (ver abajo)
4. Agrega tests en `tests/test_cli_validation.py`
5. Submit PR

### Mejorar Documentación

**Documentación de CLI individual:**
- Ubicación: `nombre-cli/README.md`
- Incluir: instalación, sintaxis, casos de uso, troubleshooting
- Ejemplos ejecutables y verificados

**Documentación web (GitHub Pages):**
- Ubicación: `docs/`
- HTML + CSS simple (sin frameworks)
- Responsive design
- SEO optimizado para español

---

## 📐 Estándares del Proyecto

### Documentación

#### Idioma Principal
- **Español** para toda la documentación de usuario
- Código y comentarios técnicos pueden estar en inglés
- Mensajes de commit en español o inglés

#### Formato
- Markdown para documentos
- Código formateado con estándar del lenguaje (Black para Python, Prettier para JS)
- Headers claros y jerárquicos (`#`, `##`, `###`)

#### Ejemplos
- **Todos los ejemplos deben ser ejecutables**
- Incluir output esperado cuando sea relevante
- Usar sintaxis de bloque de código con lenguaje especificado:

```markdown
\`\`\`bash
# Ejemplo ejecutable
gemini "¿Qué es la gravedad?"
\`\`\`
```

#### Basado en Experiencia Empírica

**✅ CORRECTO (experiencia real):**
```markdown
### Problema: Error con caracteres especiales

**Síntoma:** DeepSeek crashea al mostrar emojis en Windows.

**Solución:** Establecer `PYTHONIOENCODING=utf-8` antes de ejecutar.

**Verificado:** 2025-12-29, Windows 11, DeepSeek pip version
```

**❌ INCORRECTO (especulación):**
```markdown
### DeepSeek probablemente funciona bien con UTF-8
```

### Código

#### Tests
- **Obligatorios** para nuevas CLIs o claims documentados
- No consumir APIs reales (usar mocks/stubs)
- Incluir docstrings explicativos
- Seguir estructura de 3 niveles (ver `tests/README.md`)

#### Python
- Estilo: PEP 8
- Formatter: Black
- Type hints cuando sea posible
- Docstrings en español para funciones públicas

```python
def validar_cli(nombre: str) -> bool:
    """Verifica que una CLI esté instalada y accesible.
    
    Args:
        nombre: Nombre del comando CLI (ej: 'gemini', 'claude')
    
    Returns:
        True si la CLI está disponible, False si no
    """
    # Implementación...
```

### Git y GitHub

#### Commits
- Mensajes claros y descriptivos
- Usar verbos en infinitivo o presente
- Referencia issues cuando aplique

**Ejemplos:**
```
✅ Agregar documentación para Qwen CLI
✅ Fix: Corregir sintaxis de Gemini batch mode
✅ Tests: Validar comportamiento stateless (#12)
❌ updates
❌ fixed stuff
```

#### Branches
- Crear desde `main`
- Nombres descriptivos: `feature/nueva-cli`, `fix/gemini-timeout`, `docs/mejorar-readme`
- Un tema por branch

---

## 🔄 Proceso de Pull Request

### 1. Preparación

```bash
# Fork del repositorio en GitHub
# Luego clonar tu fork:
git clone https://github.com/TU-USUARIO/guia-cli-ia.git
cd guia-cli-ia

# Agregar upstream
git remote add upstream https://github.com/Krakaur/guia-cli-ia.git
```

### 2. Crear Branch

```bash
# Actualizar main
git checkout main
git pull upstream main

# Crear branch para tu contribución
git checkout -b feature/mi-contribucion
```

### 3. Hacer Cambios

```bash
# Editar archivos...

# Agregar cambios
git add .

# Commit con mensaje descriptivo
git commit -m "Agregar documentación para CLI XYZ"

# Push a tu fork
git push origin feature/mi-contribucion
```

### 4. Ejecutar Tests

```bash
# Instalar dependencias
pip install -r requirements.txt

# Ejecutar tests
pytest

# Verificar que todos pasen ✅
```

### 5. Submit Pull Request

1. Ve a tu fork en GitHub
2. Click en "Compare & pull request"
3. Completa template de PR:

```markdown
## Descripción
[¿Qué hace este PR?]

## Tipo de Cambio
- [ ] Bug fix
- [ ] Nueva feature
- [ ] Mejora de documentación
- [ ] Cambio breaking

## Checklist
- [ ] Tests pasan localmente
- [ ] Documentación actualizada
- [ ] Código sigue estándares del proyecto
- [ ] Commit messages son descriptivos

## Screenshots (si aplica)
[Capturas de pantalla]
```

4. Submit!

### 6. Code Review

- Maintainer revisará tu PR
- Puede pedir cambios o aclaraciones
- Una vez aprobado, se hará merge a `main`

**Tiempo típico de review:** 2-5 días

---

## 📁 Estructura del Proyecto

```
guia-cli-ia/
├── README.md                    # Documentación principal
├── LICENSE                      # MIT License
├── CONTRIBUTING.md              # Este archivo
├── CODE_OF_CONDUCT.md           # Código de conducta
├── requirements.txt             # Dependencias Python
├── pytest.ini                   # Configuración pytest
│
├── docs/                        # GitHub Pages (sitio web)
│   ├── index.html              # Landing page
│   ├── comparativa.html        # Comparativa de CLIs
│   └── troubleshooting.html    # Troubleshooting general
│
├── tests/                       # Test suite
│   ├── __init__.py
│   ├── test_cli_validation.py  # Tests principales
│   └── README.md               # Documentación de tests
│
├── claude-code/                 # Documentación Claude Code
│   ├── README.md
│   └── ejemplos/
│
├── gemini-cli/                  # Documentación Gemini
│   ├── README.md
│   └── ejemplos/
│
└── [otras CLIs]/                # Estructura similar
```

---

## 🧪 Ejecutar Tests

### Instalación de Dependencias

```bash
pip install -r requirements.txt
```

### Comandos de Testing

```bash
# Todos los tests
pytest

# Verbose (ver cada test)
pytest -v

# Solo tests rápidos
pytest -m "not slow"

# Tests de una CLI específica
pytest -k "claude"

# Con cobertura
pytest --cov=tests

# Detener en primer fallo
pytest -x
```

### Escribir Nuevos Tests

Sigue la estructura de 3 niveles (ver `tests/README.md`):

```python
class TestNuevaCLI:
    """Tests para nueva-cli."""
    
    def test_nueva_cli_available(self):
        """Verifica que nueva-cli esté instalada."""
        result = subprocess.run(
            ['nueva-cli', '--version'],
            capture_output=True,
            text=True,
            shell=True
        )
        assert result.returncode == 0
```

---

## 🎯 Roadmap del Proyecto

### Fase Actual: Publicación JOSS
- ✅ Documentación completa de 7 CLIs
- ✅ GitHub Pages activo
- ✅ Tests automatizados
- ⏳ CONTRIBUTING.md (este archivo)
- ⏳ CODE_OF_CONDUCT.md
- ⏳ Citation metadata
- ⏳ Paper JOSS

### Futuro (Post-JOSS)
- [ ] CI/CD con GitHub Actions
- [ ] Agregar más CLIs (Mistral, Cohere, etc.)
- [ ] Ejemplos interactivos en web
- [ ] Video tutoriales
- [ ] Traducción a otros idiomas (Português, English)

---

## 📞 Comunicación

### Canales

- **Issues:** Para bugs y feature requests
- **Discussions:** Para preguntas y discusión general (próximamente)
- **Pull Requests:** Para contribuciones de código/docs

### Maintainers

- **@Krakaur** (Wintermute) - Creator & Lead Maintainer

Tiempo de respuesta típico: 1-3 días

---

## ❓ Preguntas Frecuentes

### ¿Puedo contribuir si soy principiante?

¡Absolutamente! Contribuciones de todos los niveles son bienvenidas. Mejorar documentación, reportar bugs, o agregar ejemplos son excelentes primeras contribuciones.

### ¿Debo instalar todas las 7 CLIs para contribuir?

No. Solo instala las CLIs relevantes a tu contribución. Los tests pueden saltearse con `-m "not api"` para CLIs no instaladas.

### ¿Puedo contribuir en inglés?

Preferimos documentación en español para mantener consistencia, pero aceptamos contribuciones en inglés que luego traduciremos.

### ¿Qué pasa si mi PR no es aceptado?

Te daremos feedback específico. La mayoría de los rechazos son por no seguir estándares o necesitar más contexto. Siempre puedes revisar y re-submit.

---

## 🙏 Agradecimientos

Gracias por contribuir a hacer la IA más accesible para hispanohablantes. Cada pull request, issue, o sugerencia nos acerca a ese objetivo.

**¡Feliz coding!** 🚀

---

*Última actualización: 2026-01-03*  
*Para preguntas sobre este documento: abrir issue con tag `documentation`*