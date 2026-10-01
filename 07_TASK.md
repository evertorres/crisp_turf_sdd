# 📋 Desglose de Tareas Atómicas y Test-First (`tasks.md`)
> **Ubicación en el repositorio:** `specs/<id>-<nombre-spec>/tasks.md`  
> **Metodología:** Spec-Driven Development (SDD) — Fase de Desglose Táctico y Ejecución TDD.

---

<!-- GUÍA PARA EL LLM:
Este documento descompone el plan técnico ('specs/<id>/plan.md') en una lista estrictamente secuencial de tareas atómicas de 15 a 30 minutos.
Su objetivo es servir de guía táctica determinista para el desarrollador o agente de IA durante la fase de implementación.

Reglas innegociables para el desglose de tareas:
1. Duración: Cada tarea debe resolverse en 15 a 30 minutos de trabajo concentrado. Si una tarea es demasiado grande, divídela en subtareas.
2. Orden estricto por dependencias: Las tareas se ordenan siguiendo el grafo de dependencias técnicas (de modelos base y contratos hacia validadores, motor central, servicios e integración final).
3. Test-First: En 'Archivos', lista SIEMPRE primero el archivo de prueba en 'tests/' y luego el archivo de implementación.
4. Verificación determinista: Cada tarea debe incluir un criterio 'Hecho cuando:' con el comando exacto de terminal que debe ejecutarse y pasar en verde.
5. Cobertura declarada: Cada tarea debe indicar los Requisitos Funcionales (RF) o No Funcionales (RNF) de la spec que satisface.
6. Disciplina de ejecución: El agente solo debe implementar UNA tarea a la vez, ejecutar su comando de verificación y detenerse.
-->

## 🎯 Reglas de Oro para la Descomposición de Tareas

1. **Atomicidad (<30 min):** Cada tarea debe tener un alcance quirúrgico y acotado.
2. **Dependencias Claras:** Ninguna tarea debe depender de componentes que aún no se hayan construido en tareas previas.
3. **Test-First Obligatorio:** Toda tarea de código debe especificar primero el archivo de prueba y luego el archivo de producción.
4. **Verificación Automática:** Prohibido criterios subjetivos como "verificar que funcione". El criterio debe ser un comando ejecutable (`pytest`, `npm test`, `cargo test`, etc.).

---

## 📌 Formato Estándar de una Tarea Atómica

```markdown
- [ ] **Task [N]: [Acción concreta en infinitivo + componente o módulo a crear o modificar]**
  - **Archivos:** `tests/test_[modulo].py`, `[ruta]/[modulo].py`
  - **Cubre:** `RF-[XX]`, `RNF-[YY]` (o Casos Límite específicos)
  - **Hecho cuando:** `[Comando exacto de terminal]` pase al 100% en verde con 0 errores de linter y tipado estricto.
```

---

## 📝 Lista Secuencial de Tareas Atómicas

<!-- GUÍA PARA EL LLM:
Adapta esta lista secuencial según la arquitectura definida en 'specs/<id>/plan.md'.
Mantén el orden de dependencias de abajo hacia arriba (bottom-up).
-->

- [ ] **Task 1: Definición de modelos de datos, esquemas de entrada/salida y validaciones de rango**
  - **Archivos:** `tests/test_models.py`, `models/[entidades].py`
  - **Cubre:** RF-01, RNF-04
  - **Hecho cuando:** `pytest tests/test_models.py` (o comando equivalente del stack) pase al 100% en verde con verificación de tipos sin advertencias.

- [ ] **Task 2: Validador de reglas de vigencia, datos incompletos y casos límite**
  - **Archivos:** `tests/test_validador.py`, `core/[validador].py`
  - **Cubre:** RF-03, Casos Límite (valores anómalos, nulos y caducidad)
  - **Hecho cuando:** `pytest tests/test_validador.py` pase en verde para todos los casos de borde identificados en la spec.

- [ ] **Task 3: Motor de lógica central, scoring y evaluación de umbrales**
  - **Archivos:** `tests/test_calculador.py`, `core/[calculador].py`
  - **Cubre:** RF-01, RF-02, RF-04
  - **Hecho cuando:** `pytest tests/test_calculador.py` confirme la exactitud de los cálculos y las condiciones de disparo de alertas.

- [ ] **Task 4: Módulo de auditoría, trazabilidad inmutable y sanitización de datos sensibles**
  - **Archivos:** `tests/test_audit.py`, `audit/[logger].py`
  - **Cubre:** RF-05, RNF-02 (Cero fugas de información protegida / PII)
  - **Hecho cuando:** `pytest tests/test_audit.py` valide la persistencia estructurada sin exposición de datos sensibles.

- [ ] **Task 5: Orquestador del servicio, integración end-to-end y verificación de latencia**
  - **Archivos:** `tests/test_integration.py`, `service.py`
  - **Cubre:** Flujo completo E2E, RNF-01 (Latencia < X ms)
  - **Hecho cuando:** `pytest tests/test_integration.py` demuestre que el ciclo completo opera dentro de los límites de tiempo estipulados.

- [ ] **Task 6: Validación global de calidad, cobertura total y documentación de cierre**
  - **Archivos:** Suite completa de tests y documentación técnica
  - **Cubre:** Definition of Done (DoD) de la Spec
  - **Hecho cuando:** La suite completa de tests pase al 100%, linter y typechecker reporten 0 errores, y la cobertura alcance el umbral de la Constitución.

---

## ⚡ Protocolo de Ejecución de Tareas para el Agente (Checklist Operativo)

Cada vez que el desarrollador o agente de IA aborde una tarea de esta lista, debe seguir este flujo sin excepciones:

1. **Escribir la prueba primero:** Crear o actualizar el archivo de test en `tests/`.
2. **Comprobar fallo (Red):** Ejecutar el comando del test y confirmar que falla por la razón esperada.
3. **Implementar el código mínimo (Green):** Escribir la lógica necesaria para que la prueba pase.
4. **Ejecutar verificación:** Comprobar que el comando especificado en "Hecho cuando:" pasa en verde.
5. **Prevenir regresiones:** Ejecutar la suite completa para confirmar que no se han roto componentes anteriores.
6. **Validar higiene:** Correr linter y typechecker con cero advertencias.
7. **Actualizar estado:** Marcar con `[x]` el checkbox de la tarea completada en `tasks.md`.
8. **DETENERSE:** Informar al usuario del hito completado y esperar confirmación para la siguiente tarea.

---

## ✅ Checklist de Calidad para el LLM al Generar Tasks (`tasks.md`):
- [ ] Todas las tareas están numeradas consecutivamente y cuentan con checkboxes `[ ]`.
- [ ] Cada tarea tiene una duración estimada de entre 15 y 30 minutos.
- [ ] El orden de tareas respeta estrictamente el grafo de dependencias técnicas.
- [ ] En la sección de archivos, siempre aparece primero el archivo de prueba (`tests/`).
- [ ] El criterio 'Hecho cuando:' contiene el comando exacto y ejecutable de verificación.
- [ ] Cada Requisito Funcional (RF) de la especificación está cubierto por al menos una tarea.
