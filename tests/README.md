# Test Suite - Guía CLIs de IA

## Propósito

Este test suite valida que los 7 CLIs documentados en la guía:
1. Están instalados correctamente
2. Se comportan como está documentado
3. Son compatibles con workflows multi-agente

## Requisitos JOSS

JOSS (Journal of Open Source Software) requiere tests automatizados que:
- ✅ Verifiquen funcionalidad básica
- ✅ Sean reproducibles
- ✅ No dependan de recursos externos (evitamos consumir APIs)
- ✅ Documenten claims específicos de la guía

## Estructura

```
tests/
├── __init__.py                 # Paquete de tests
├── test_cli_validation.py      # Test suite principal
└── README.md                   # Este archivo
```

## Ejecutar Tests

### Instalación de dependencias
```bash
pip install -r requirements.txt
```

### Comandos básicos

```bash
# Ejecutar todos los tests
pytest

# Ejecutar con verbose
pytest -v

# Ejecutar solo tests rápidos
pytest -m "not slow"

# Ejecutar sin tests que consumen API
pytest -m "not api"

# Generar reporte de cobertura
pytest --cov=tests

# Tests específicos de una clase
pytest tests/test_cli_validation.py::TestCLIAvailability

# Un test específico
pytest tests/test_cli_validation.py::TestCLIAvailability::test_claude_code_available
```

## Niveles de Testing

### Nivel 1: Disponibilidad (Installation)
Verifica que cada CLI está instalado y responde a comandos básicos.

**Tests:**
- `test_claude_code_available()`
- `test_gemini_available()`
- `test_codex_available()`
- `test_copilot_available()`
- `test_deepseek_available()`
- `test_qwen_available()`
- `test_github_cli_available()`

### Nivel 2: Comportamiento Documentado
Valida claims específicos de la guía (ej: "Gemini es stateless", "DeepSeek requiere UTF-8").

**Tests:**
- `test_deepseek_utf8_environment()` - Requisito Windows UTF-8
- `test_claude_code_batch_syntax()` - Sintaxis batch mode
- `test_gemini_no_p_flag()` - Flag -p obsoleta
- `test_codex_git_skip_flag()` - Flag --skip-git-repo-check
- `test_copilot_batch_flags()` - Flags de modo batch

### Nivel 3: Integración Multi-Agente
Verifica que CLIs funcionan con el patrón M1-M2 (executor-critic) de RoundTable Messenger.

**Tests:**
- `test_cli_subprocess_integration()` - Llamadas vía subprocess.run()
- `test_geographic_distribution()` - Triangulación USA/China

## Filosofía de Testing

### 1. Sin Consumo de APIs en CI/CD
- Tests NO hacen llamadas reales a servicios LLM
- Evita rate limits y costos en testing automatizado
- Valida instalación y comportamiento documentado solamente

### 2. Validación de Documentación Empírica
- Tests verifican claims de la guía (GUIA_CLI_AI_SALA.md)
- Cada test referencia sección específica de documentación
- Si un test falla: o el CLI cambió, o la guía necesita actualización

### 3. Validación de Patrón Multi-Agente
- Tests aseguran que CLIs funcionan con subprocess (patrón M1-M2)
- Distribución geográfica documentada para reducción de bias
- Tests de integración validan compatibilidad de workflow

### 4. Windows-First pero Portable
- Desarrollo primario en Windows 11 + PowerShell
- Tests skip funcionalidades específicas de plataforma en no-Windows
- Tests core funcionan en todas las plataformas

## Markers Personalizados

```python
@pytest.mark.slow       # Tests lentos (skip con -m "not slow")
@pytest.mark.api        # Tests que consumen APIs (skip con -m "not api")
@pytest.mark.windows    # Tests solo Windows (skip automático en otras plataformas)
```

## CI/CD Integration

Estos tests están diseñados para ejecutarse en:
- ✅ GitHub Actions
- ✅ GitLab CI
- ✅ Local development
- ✅ Pre-commit hooks

## Contribuciones

Al agregar nuevos tests:
1. Sigue la estructura de 3 niveles
2. Documenta el claim que estás validando
3. Usa markers apropiados (@pytest.mark.slow, etc.)
4. Evita consumir APIs reales
5. Referencia la sección de documentación relevante

## Referencias

- Documentación proyecto: [README.md](../README.md)
- Guía completa: [GUIA_CLI_AI_SALA.md](/mnt/project/GUIA_CLI_AI_SALA.md)
- RoundTable Messenger: [ROUNDTABLE_MESSENGER_COMPLETE_DOCUMENTATION.md](/mnt/project/ROUNDTABLE_MESSENGER_COMPLETE_DOCUMENTATION.md)
- JOSS Guidelines: https://joss.readthedocs.io
