# 💬 Playbook de Prompts por Fase de SDD (Cheatsheet Operativo)
> **Metodología:** Spec-Driven Development (SDD) — Guía determinista de prompts para interacción con modelos de lenguaje y agentes de código (Claude Code, Antigravity, Cursor, ChatGPT, etc.).

---

<!-- GUÍA PARA EL LLM Y EL INGENIERO:
El éxito del desarrollo guiado por especificaciones depende de NO saltarse fases.
Cada fase tiene un objetivo único, guardrails estrictos y un artefacto de salida bien definido.

Reglas de Oro del Flujo SDD:
1. Configura SIEMPRE 'AGENTS.md' en la raíz antes de iniciar cualquier otra interacción con el agente.
2. NUNCA pidas código en las fases de especificación, arquitectura y desglose táctico.
3. En la fase de Implementación, trabaja TAREA POR TAREA. Escribe siempre el test antes del código.
4. Ante cualquier cambio de requisitos en medio del desarrollo, actualiza la especificación funcional primero.
-->

## 📋 Tabla Resumen de Prompts Esenciales

| Fase SDD | Objetivo de la Fase | Artefacto Generado | Prompt Esencial (Listo para copiar y personalizar) |
|---|---|---|---|
| **0. Inicialización & Guardrails** | Configurar el manual operativo y límites del agente en la raíz. | `AGENTS.md` | `"Lee la plantilla ./01_AGENTS.md. Genera el archivo AGENTS.md para la raíz de este repositorio con la identidad de [Nombre del Proyecto], comandos de test/lint/tipado en [tu stack], estilo de código y guardrails innegociables (cero vibe coding, aislamiento de tarea única, test-first). Espera mi aprobación."` |
| **1. Descubrimiento & Viabilidad** | Alinear la visión de negocio, impacto vs. viabilidad y KPIs. | `docs/canvas.md` | `"NO escribas código. Actúa como Product Manager y Estratega Técnico Senior. Siguiendo ./02_CRISP_DM_CANVAS.md, hazme preguntas puntuales para definir el canvas del proyecto [Nombre]: problema real, usuarios, factibilidad técnica y métricas de éxito. Una vez responda, genera docs/canvas.md."` |
| **2. Ontología de Dominio & U-Fu** | Modelar metas, objetos, operaciones y erradicar tareas parásitas. | `docs/domain_ontology.md` | `"NO escribas código. Actúa como Ingeniero Cognitivo y Especialista en el Marco TURF. Basándote en ./03_TURF_ONTOLOGY_UFU.md, analiza el dominio de [Nombre]: modela usuarios, metas, objetos, operaciones y restricciones (U-Fu), optimizando el flujo para erradicar tareas parásitas. Genera docs/domain_ontology.md."` |
| **3. Constitución** | Establecer principios innegociables de calidad, stack y límites. | `docs/constitution.md` | `"Proponme la constitución de este proyecto siguiendo ./04_CONSTITUTION.md: 6 a 8 principios cortos, directos y objetivamente verificables sobre stack ([tu stack]), calidad de código, pruebas automáticas (cobertura >=[X]%), tipado estricto, privacidad/seguridad y límites de alcance (cero vibe coding). Máx. 25 líneas. Espera mi aprobación antes de continuar."` |
| **4. Spec (Entrevista EARS)** | Entrevistar al usuario para extraer el QUÉ y el POR QUÉ sin código. | `specs/<id>/spec.md` | `"NO escribas código. Actúa como Ingeniero de Requisitos de Software Senior. Hazme preguntas de una en una (máx. 5 preguntas clave) sobre el caso de uso de [nombre del módulo/feature]: casos límite, validaciones, actores y condiciones de borde. Una vez responda, genera specs/<id>/spec.md siguiendo ./05_SPEC_EARS.md con RF numerados en notación formal EARS, historias de usuario, RNF medibles, fuera de alcance explícito y Definition of Done. Solo el QUÉ y el POR QUÉ."` |
| **5. Clarificación QA & Auditoría** | Auditar la spec en busca de ambigüedades antes de planear. | Comentarios / Ajustes a `spec.md` | `"Revisa la spec generada actuando como un Líder de QA y Auditor de Software: detecta ambigüedades, contradicciones lógicas, casos límite no contemplados, suposiciones no verificadas y posibles conflictos con docs/constitution.md. Solo detecta y lista las discrepancias con preguntas puntuales; NO intentes resolverlas todavía."` |
| **6. Modo Plan (Arquitectura)** | Diseñar la arquitectura modular y decisiones técnicas. | `specs/<id>/plan.md` | `"Lee docs/constitution.md y specs/<id>/spec.md. SIN ESCRIBIR CÓDIGO de implementación: genera specs/<id>/plan.md siguiendo la plantilla ./06_PLAN.md con la arquitectura modular de carpetas y archivos, esquemas de datos tipados de entrada/salida (JSON / Pydantic / DTOs), decisiones técnicas justificadas bajo formato ADR (incluyendo la alternativa descartada y por qué) y la estrategia de tests. Indica qué RF cubre cada componente."` |
| **7. Tareas Atómicas** | Desglosar el plan en unidades de trabajo de 15-30 min. | `specs/<id>/tasks.md` | `"Lee specs/<id>/plan.md. Divide el plan siguiendo la plantilla ./07_TASK.md en specs/<id>/tasks.md con una lista de tareas estrictamente secuencial, ordenadas por dependencia técnica, de <30 minutos cada una. Cada tarea debe tener: (1) Checkbox [ ], (2) Título descriptivo, (3) RF asociado, (4) Archivos exactos a crear o modificar (el test primero), y (5) Comando exacto de verificación ('Hecho cuando:'). NO ejecutes ninguna tarea todavía."` |
| **8. Implementación Test-First** | Ejecutar TDD estricto tarea por tarea con parada obligatoria. | Código fuente y tests unitarios | `"Implementa ÚNICAMENTE la tarea [Task N] de specs/<id>/tasks.md. Escribe primero el archivo de prueba correspondiente en tests/. Ejecuta el test para verificar que falle. Luego escribe el código mínimo de implementación necesario para que pase. Ejecuta el comando de test y muéstrame el resultado en verde. Verifica tipado y linter. Marca [x] en tasks.md y DETENTE; espera mi confirmación antes de la siguiente tarea."` |
| **9. Validación Final & Trazabilidad** | Verificar cumplimiento al 100% de la spec frente a los tests. | Reporte de cierre de Spec | `"Recorre specs/<id>/spec.md requisito funcional por requisito funcional (RF-01 a RF-0N): muestra qué test unitario o de integración cubre cada requisito y su estado de ejecución. Ejecuta la suite completa de pruebas, verificación de tipos y linter. Emite el veredicto final: ¿Cumple el software con el 100% de la especificación sin desviaciones?"` |
| **10. Gestión del Cambio** | Modificar requisitos de forma controlada sin romper código. | Diff en `spec.md` + impacto en tests | `"Nuevo requerimiento / cambio de regla: <describe el cambio aquí>. NO toques código de implementación todavía: actualiza primero specs/<id>/spec.md mostrando el diff exacto, explica qué requisitos funcionales se ven afectados y qué archivos de tests deberán ajustarse. Espera mi aprobación."` |

---

## 🔍 Detalle Operativo y Guardrails por Fase

### Fase 0: Inicialización del Agente (`AGENTS.md`)
- **Peligro común:** Empezar a interactuar con un asistente de IA sin configurar su contexto, permitiendo que adopte heurísticas desordenadas o genere código antes de tiempo.
- **Guardrail:** Exigir la creación de `AGENTS.md` en la raíz como primer paso obligatorio, con comandos del stack y guardrails de disciplina estricta.

### Fase 1 & 2: Descubrimiento, Canvas y Ontología TURF
- **Peligro común:** Saltar directo a escribir especificaciones técnicas sin tener clara la viabilidad del negocio o los flujos óptimos de interacción del usuario.
- **Guardrail:** La instrucción `"NO escribas código. Actúa como Product Manager / Ingeniero Cognitivo"` orienta al modelo hacia la extracción de valor y erradicación de tareas parásitas.

### Fase 3: Constitución
- **Peligro común:** Generar un documento genérico lleno de lugares comunes ("escribir código limpio").
- **Guardrail:** Exige herramientas y números: nombra el framework de pruebas, la herramienta de tipado y el porcentaje mínimo de cobertura.

### Fase 4: Spec (Entrevista)
- **Peligro común:** Que el modelo empiece a escribir clases, imports o scripts de inmediato.
- **Guardrail:** La instrucción explícita `"NO escribas código. Solo el QUÉ y el POR QUÉ"` bloquea la generación precipitada de código.

### Fase 5: Clarificación QA
- **Peligro común:** Que el modelo asuma respuestas a dudas críticas de negocio.
- **Guardrail:** La instrucción `"Solo detecta y lista las discrepancias, NO las resuelvas todavía"` fuerza a que las dudas sean resueltas por el humano o stakeholder.

### Fase 6: Modo Plan
- **Peligro común:** Diseñar monolitos sin modularidad o tomar decisiones técnicas sin justificar el trade-off.
- **Guardrail:** Exigir formato ADR (Architectural Decision Record) con alternativa descartada obligatoria para cada decisión clave, conforme a `06_PLAN.md`.

### Fase 7: Tareas Atómicas
- **Peligro común:** Tareas gigantescas como "Implementar backend completo" o tareas sin comando de verificación.
- **Guardrail:** Exigir tareas atómicas de <30 minutos con comando directo tipo `pytest tests/test_x.py` o `npm test`, conforme a `07_TASK.md`.

### Fase 8: Implementación Test-First
- **Peligro común:** El agente se emociona y completa 5 tareas de golpe sin verificar y acumulando errores.
- **Guardrail:** Instrucción estricta: `"Implementa ÚNICAMENTE la tarea Tn... y DETENTE; espera mi confirmación"`.

### Fase 9: Validación Final
- **Peligro común:** Asumir que la funcionalidad está lista solo porque un script corrió.
- **Guardrail:** Matriz de trazabilidad requisito a requisito (RF vs Test).

### Fase 10: Gestión del Cambio
- **Peligro común:** Cambiar el código directamente ante una nueva idea, dejando la especificación desactualizada (desincronización de spec y código).
- **Guardrail:** Regla inquebrantable de SDD: La spec se modifica primero; el código solo se adapta después de que la spec modificada sea aprobada.
