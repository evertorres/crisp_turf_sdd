# 🛠️ Plan Técnico y Arquitectura de Módulo (`plan.md`)
> **Ubicación en el repositorio:** `specs/<id>-<nombre-spec>/plan.md`  
> **Metodología:** Spec-Driven Development (SDD) — Fase de Diseño de Arquitectura, Contratos y ADR.

---

<!-- GUÍA PARA EL LLM:
Este documento traduce el 'QUÉ' y 'POR QUÉ' de la especificación funcional ('specs/<id>/spec.md') en el 'CÓMO' técnico ('plan.md').
Define la arquitectura modular, los esquemas y contratos de datos tipados, las decisiones técnicas justificadas (ADR) y la estrategia de tests.

Reglas clave para esta fase:
1. NUNCA escribas código de implementación en esta fase. El plan es puramente conceptual, arquitectónico y contractual.
2. Todo componente técnico debe mapear a al menos un Requisito Funcional (RF) o No Funcional (RNF) de la spec.
3. Toda decisión técnica clave debe documentarse en formato ADR con su alternativa descartada y justificación objetiva.
4. El desglose táctico en tareas ejecutables NO va en este archivo; se genera en 'specs/<id>/tasks.md' siguiendo la plantilla '07_TASK.md'.
-->

## 1. Arquitectura Modular Propuesta
<!-- GUÍA PARA EL LLM:
Diseña una estructura de carpetas limpia y altamente cohesiva. Separa la lógica de dominio puro de los adaptadores, frameworks e infraestructura.
Indica claramente la responsabilidad de cada archivo o submódulo.
-->
```
[nombre_paquete_o_modulo]/
├── models/             # Esquemas de datos tipados, entidades y validadores de dominio (Pydantic / dataclasses / types)
│   ├── [entidad_principal].py   # Modelos de entrada, parámetros y estados
│   └── [resultado_o_evento].py  # Modelos de salida, eventos o DTOs
├── core/               # Lógica de negocio pura (desacoplada de frameworks y persistencia)
│   ├── [calculador_o_motor].py  # Algoritmos, reglas de negocio o cálculos centrales (RF-01, RF-02)
│   └── [validador].py           # Reglas de validación, vigencia y casos límite (RF-03)
├── ports/              # Interfaces / protocolos abstractos (I/O, APIs externas, storage)
│   └── [repositorio_o_api].py
├── adapters/           # Implementaciones concretas de infraestructura (DB, HTTP clients, colas)
│   └── [adaptador_concreto].py
├── audit/              # Registro de trazabilidad, eventos inmutables y telemetría (RF-05)
│   └── [logger_o_tracker].py
├── service.py          # Caso de uso / Orquestador del flujo principal (RF-04)
└── tests/              # Suite de pruebas automatizadas (espejo de la estructura de código)
    ├── conftest.py              # Fixtures, mocks y datos de prueba sintéticos
    ├── test_models.py           # Pruebas de esquemas y validación de tipos
    ├── test_[motor].py          # Pruebas de lógica de cálculo y umbrales
    ├── test_[validador].py      # Pruebas de casos límite y excepciones
    ├── test_[auditoria].py      # Pruebas de log y cero fuga de datos
    └── test_integration.py      # Pruebas end-to-end del orquestador
```

---

## 2. Esquema de Datos Central (Contratos Tipados de Entrada / Salida)
<!-- GUÍA PARA EL LLM:
Modela el contrato representativo de los datos que ingresan y salen del módulo (JSON Schema, Pydantic, Zod o TypeScript interfaces).
Incluye tipos de datos, restricciones de rango y validaciones requeridas.
-->

### Contrato de Entrada (Input Payload)
```json
{
  "entity_id": "REQ-10029",
  "timestamp": "2026-09-30T15:30:00Z",
  "category": "standard",
  "parameters": {
    "metric_primary": 4.5,
    "metric_secondary": 22.0,
    "is_active": true
  },
  "metadata": {
    "source_system": "upstream-service",
    "version": "1.0"
  }
}
```

### Contrato de Salida / Resultado (Output DTO)
```json
{
  "evaluation_id": "EVAL-88219",
  "timestamp": "2026-09-30T15:30:00.120Z",
  "entity_id": "REQ-10029",
  "score": 0.84,
  "level": "HIGH_RISK",
  "action_recommended": "REQUIRE_MANUAL_REVIEW",
  "explanation_factors": [
    "metric_primary exceeds upper threshold (4.5 > 3.0)",
    "metric_secondary abnormal"
  ],
  "requires_ack": true
}
```

---

## 3. Decisiones Técnicas & Alternativas Descartadas (ADR - Architectural Decision Record)
<!-- GUÍA PARA EL LLM:
Registra cada decisión arquitectónica crítica justificando el POR QUÉ se adoptó y qué alternativas se descartaron.
Esto previene que un desarrollador o agente posterior reescriba decisiones fundamentadas.
-->

- **Decisión 1: `[ej. Adopción de Pydantic v2 para validación de datos en tiempo de ejecución]`**  
  - *Alternativa descartada:* `[ej. Diccionarios nativos sin tipar o validadores manuales con if/else.]`  
  - *Razón y Justificación:* `[Garantiza serialización estricta, rendimiento en C/Rust y cumplimiento del Principio 2 de la Constitución.]`

- **Decisión 2: `[ej. Formato de log de auditoría en JSON Lines append-only]`**  
  - *Alternativa descartada:* `[ej. Conexión directa a base de datos relacional externa en este módulo.]`  
  - *Razón y Justificación:* `[Mantiene desacoplamiento de infraestructura, minimiza dependencias y asegura escritura atómica e inmutable.]`

- **Decisión 3: `[ej. Estrategia de fallback determinista ante caídas de servicios externos]`**  
  - *Alternativa descartada:* `[ej. Lanzar un error HTTP 500 no controlado o reintentar indefinidamente.]`  
  - *Razón y Justificación:* `[Cumple con el principio de Falla Segura (Fail-Safe) devolviendo un estado degradado explícito.]`

---

## 4. Matriz de Trazabilidad (Diseño vs. Requisitos)
<!-- GUÍA PARA EL LLM:
Mapea cada componente técnico con los Requisitos Funcionales que satisface y el archivo de prueba que lo validará.
-->
| Módulo / Componente Técnico | Requisitos que Cubre | Archivo de Prueba Asociado |
|---|---|---|
| `models/[entidad].py` | RF-01, RNF-04 | `tests/test_models.py` |
| `core/[validador].py` | RF-03, Casos Límite | `tests/test_validador.py` |
| `core/[calculador].py` | RF-01, RF-02, RF-04 | `tests/test_calculador.py` |
| `audit/[logger].py` | RF-05, RNF-02 (Cero fugas) | `tests/test_audit.py` |
| `service.py` (Orquestador) | Integración E2E, RNF-01 | `tests/test_integration.py` |

---

## 5. Estrategia y Cobertura de Pruebas
<!-- GUÍA PARA EL LLM:
Establece los niveles de prueba requeridos y las premisas de mocking.
-->
- **Pruebas Unitarias de Modelos y Contratos:** Validación de serialización, deserialización y rechazo de payloads inválidos.
- **Pruebas de Lógica Pura (Core):** Verificación de cálculos deterministas, umbrales y manejo estricto de casos límite.
- **Pruebas de Aislamiento:** Uso de dobles de prueba / mocks en puertos de I/O y adaptadores externos.
- **Pruebas de Integración:** Flujo end-to-end del orquestador verificando contratos de entrada a salida.
- **Umbral de Cobertura:** Cobertura de código `>= [X]%` en lógica de dominio según la Constitución.

---

## ✅ Checklist de Calidad para el LLM al Generar el Plan (`plan.md`):
- [ ] La arquitectura modular refleja el stack del proyecto y respeta los principios de `docs/constitution.md`.
- [ ] No contiene código de implementación prematuro (únicamente esquemas, firmas y contratos).
- [ ] Cada decisión técnica en ADR incluye al menos una alternativa descartada y su justificación explícita.
- [ ] Todos los Requisitos Funcionales (RF) y No Funcionales (RNF) de la spec están cubiertos en la matriz de trazabilidad.
- [ ] Se contemplan contratos de entrada y salida completos con tipos de datos y rangos válidos.
