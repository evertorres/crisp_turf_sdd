# 🤖 AGENTS.md — Manual Operativo para Agentes de Inteligencia Artificial
> **Ubicación en el repositorio:** `AGENTS.md` (o `CLAUDE.md` / `.cursorrules`) en la raíz del proyecto.  
> **Metodología:** Spec-Driven Development (SDD) — Directivas y Guardrails de Comportamiento para LLMs.

---

<!-- GUÍA PARA EL LLM:
Este archivo es el 'System Prompt de Repositorio' que lee el modelo o agente de IA al interactuar con el código.
Su propósito es establecer límites deterministas para evitar:
1. 'Vibe Coding' (escribir código intuitivo sin seguir especificaciones).
2. Modificar múltiples archivos sin pruebas previas.
3. Ignorar los contratos de la Constitución y la Spec activa.
4. Asumir dependencias externas no autorizadas.

Al adaptar este archivo para un proyecto específico, completa los comandos exactos y convenciones según el stack utilizado.
-->

## 📌 Proyecto
`[Nombre del Proyecto o Módulo]: [Descripción concisa en 2 o 3 oraciones de qué es el software, su objetivo principal y la arquitectura base (ej. API REST modular en Python 3.12 con tipado estricto en Pydantic, desacoplada en dominio y adaptadores, con pruebas unitarias en pytest)].`

---

## ⚡ Comandos Esenciales del Repositorio
<!-- GUÍA PARA EL LLM:
Configura los comandos exactos que el agente debe ejecutar para verificar su trabajo.
Usa las herramientas oficiales del proyecto.
-->
- **Instalar dependencias:** `[ej. uv sync / poetry install / npm install / cargo build]`
- **Ejecutar suite completa de tests:** `[ej. pytest -v tests/ / npm test / cargo test]`
- **Ejecutar test específico:** `[ej. pytest tests/test_modulo.py -k "test_caso" / npm test -- -t "caso"]`
- **Verificación estática de tipos:** `[ej. mypy src/ / tsc --noEmit]`
- **Linter y formateador de código:** `[ej. ruff check src/ && ruff format --check src/ / eslint .]`
- **Reporte de cobertura de pruebas:** `[ej. pytest --cov=src --cov-report=term-missing tests/]`

---

## 📐 Estilo y Convenciones de Código
<!-- GUÍA PARA EL LLM:
Define las convenciones formales del código para garantizar homogeneidad total.
-->
- **Lenguaje y Versión:** `[ej. Python 3.12+ / TypeScript 5.4+ / Rust 2021 / Go 1.22+]`
- **Tipado:** Tipado estricto al 100%. Prohibido el uso de tipos implícitos o `Any`/`unknown` en contratos de dominio.
- **Nomenclatura:**
  - Clases / Tipos: `PascalCase`
  - Funciones / Métodos / Variables: `snake_case` (o `camelCase` según el lenguaje)
  - Constantes globales: `SCREAMING_SNAKE_CASE`
  - Archivos de prueba: `test_<modulo>.py` o `<modulo>.test.ts`
- **Idioma del Código:**
  - Identificadores técnicos, código, comentarios y commits: **Inglés** (ej. `calculate_risk_score`).
  - Textos de cara al usuario, mensajes de negocio y documentación funcional: **Español formal** (o idioma del cliente).
- **Principios de Diseño:** DRY (*Don't Repeat Yourself*), SOLID y Alta Cohesión. Funciones pequeñas con responsabilidad única (<30 líneas).

---

## 🛑 Reglas Innegociables para el Agente (Guardrails)

1. **Lectura Previa Obligatoria:**  
   Antes de sugerir o modificar una sola línea de código, debes leer obligatoriamente:
   - `docs/constitution.md` (Límites y principios del repositorio)
   - La especificación activa en `specs/<id>/spec.md` (Requisitos EARS)
   - El plan técnico en `specs/<id>/plan.md` y `specs/<id>/tasks.md`

2. **Test-First Estricto (TDD):**  
   NUNCA escribas código de implementación sin haber escrito primero la prueba correspondiente en el directorio de tests. Verifica que la prueba falle (rojo) antes de escribir el código mínimo para hacerla pasar (verde).

3. **Aislamiento de Tarea Única:**  
   Trabaja en **UNA SOLA tarea atómica a la vez** (siguiendo el orden secuencial de `tasks.md`). Al completarla, ejecuta la suite de tests, marca el checkbox `[x]` correspondiente y **DETENTE** para solicitar confirmación humana. Prohibido adelantarte a la siguiente tarea por iniciativa propia.

4. **Cero 'Vibe Coding' y Cero Expansión de Alcance:**  
   Prohibido agregar heurísticas, campos opcionales, librerías externas o métodos no documentados explícitamente en la especificación activa. Si consideras que falta algo, formúlalo como pregunta antes de programarlo.

5. **No Destrucción ni Regresiones:**  
   Ninguna tarea se considera completa si introduce regresiones en pruebas previas. Todos los tests existentes deben permanecer en verde.

---

## 🏁 Protocolo de Finalización de Tarea (Checklist de Entrega)
Cada vez que el agente finalice una tarea de `tasks.md`, debe ejecutar en este orden estricto:

1. [ ] Ejecutar el comando del test específico y verificar que pase en verde.
2. [ ] Ejecutar la suite completa de pruebas para descartar regresiones.
3. [ ] Ejecutar el linter y typechecker para confirmar 0 errores y 0 warnings.
4. [ ] Mostrar un diff conciso y claro de los archivos modificados.
5. [ ] Marcar con `[x]` la tarea correspondiente en `tasks.md`.
6. [ ] **DETENERSE:** Explicar brevemente qué se completó y esperar la confirmación del desarrollador para proceder con la siguiente tarea.
