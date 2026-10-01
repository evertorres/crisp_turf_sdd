# 📝 Especificación Funcional (Spec Formal en Notación EARS)
> **Ubicación en el repositorio:** `specs/<id>-<nombre-spec>/spec.md` *(ej. `specs/001-autenticacion-oauth/spec.md`)*  
> **Metodología:** Spec-Driven Development (SDD) & Easy Approach to Requirements Syntax (EARS).

---

<!-- GUÍA PARA EL LLM:
La especificación (spec.md) es la FUENTE ÚNICA DE VERDAD funcional del proyecto.
Define el QUÉ y el POR QUÉ, nunca el CÓMO de implementación (lenguajes, clases o frameworks corresponden a plan.md).

Reglas para el LLM al redactar o revisar este documento:
1. Utiliza estrictamente la notación formal EARS para los Requisitos Funcionales (RF).
2. Cada RF debe ser atómico, no ambiguo y testeable con una prueba automatizada.
3. Los Requisitos No Funcionales (RNF) deben tener métricas cuantitativas (ej. no digas 'debe ser rápido', di 'latencia < 200 ms en p95').
4. Los Casos Límite (Edge Cases) son obligatorios: piensa en valores nulos, datos corruptos, timeouts, concurrencia y desbordamientos.
5. El Fuera de Alcance (Out of Scope) debe ser explícito para evitar 'scope creep' (expansión descontrolada del alcance).
6. Si detectas ambigüedades en la solicitud del usuario, NO inventes los requisitos: agrégalos en la sección 'Dudas Abiertas' o pregúntale antes de cerrar la spec.
-->

## 📌 Guía Rápida de Sintaxis EARS (Para el LLM)
| Patrón EARS | Estructura Sintáctica Formal | Cuándo usarlo |
|---|---|---|
| **Ubiquitous (Universal)** | `EL SISTEMA deberá <acción>.` | Requisitos permanentes que siempre aplican, sin condición previa. |
| **Event-driven (Por Evento)** | `CUANDO <evento disparador>, EL SISTEMA deberá <acción>.` | Acciones detonadas por un input de usuario, mensaje o trigger temporal. |
| **State-driven (Por Estado)** | `MIENTRAS <estado activo>, EL SISTEMA deberá <acción>.` | Comportamientos que aplican solo mientras el sistema esté en un modo o estado específico. |
| **Unwanted Behavior (Excepción)** | `SI <condición anómala o error>, ENTONCES EL SISTEMA deberá <acción mitigadora>.` | Manejo de fallos, validaciones inválidas, datos caducos o excepciones. |
| **Optional Feature (Opcional)** | `DONDE <característica habilitada/configurada>, EL SISTEMA deberá <acción>.` | Funcionalidades sujetas a flags de configuración o planes premium. |
| **Complex (Combinado)** | `MIENTRAS <estado>, CUANDO <evento>, EL SISTEMA deberá <acción>.` | Eventos que ocurren únicamente bajo un estado particular del sistema. |

---

## Spec `[ID-001]` — `[Nombre Descriptivo de la Especificación o Módulo]`
- **Estado:** `[Draft | In Review | Approved | Implemented]`
- **Fecha de Creación:** `[YYYY-MM-DD]`
- **Autor / Responsable:** `[Nombre o Rol]`
- **Módulo / Componente:** `[Nombre del módulo o paquete]`

---

## 1. Contexto y Objetivo
<!-- GUÍA PARA EL LLM:
Explica en 1 o 2 párrafos:
1. ¿Cuál es el problema actual que enfrentan los usuarios o el negocio?
2. ¿Qué solución concreta provee este módulo?
3. ¿Qué impacto o valor medible generará una vez implementado?
-->
`[Describe el contexto del problema, la justificación de negocio y el objetivo medible de este desarrollo. Explica por qué es necesario y qué valor aporta al usuario o sistema final.]`

---

## 2. Actores y Usuarios
<!-- GUÍA PARA EL LLM:
Enumera los roles humanos o sistemas externos que interactúan directamente con esta funcionalidad.
-->
- **`[Actor Principal]`:** `[Descripción del rol, qué hace y qué espera recibir de este módulo.]`
- **`[Actor Secundario / Supervisor]`:** `[Rol de auditoría, soporte o aprobación de excepciones.]`
- **`[Sistema / Servicio Externo]`:** `[APIs, colas o bases de datos con las que interactúa este módulo.]`

---

## 3. Historias de Usuario
<!-- GUÍA PARA EL LLM:
Redacta de 2 a 4 historias de usuario clave en formato estándar:
'Como [rol], quiero [capacidad/acción], para [beneficio/propósito de negocio].'
-->
- **HU-01:** Como `[rol de usuario]`, quiero `[acción o funcionalidad esperada]`, para `[beneficio claro o valor obtenido]`.
- **HU-02:** Como `[rol de usuario]`, quiero `[acción o funcionalidad esperada]`, para `[beneficio claro o valor obtenido]`.
- **HU-03:** Como `[rol de usuario]`, quiero `[acción o funcionalidad esperada]`, para `[beneficio claro o valor obtenido]`.

---

## 4. Requisitos Funcionales (EARS)
<!-- GUÍA PARA EL LLM:
Escribe cada requisito funcional usando la notación EARS correspondiente indicada entre paréntesis.
Numeración estricta (RF-01, RF-02, ...).
Asegúrate de incluir al menos: un evento (CUANDO), una excepción (SI... ENTONCES), un estado o ubicuo, y reglas de validación.
-->
- **RF-01 (Event-driven):** CUANDO `[el usuario o sistema ejecute la acción X o ingrese el dato Y]`, EL SISTEMA deberá `[procesar la entrada y calcular o retornar Z en menos de T tiempo]`.
- **RF-02 (State-driven):** MIENTRAS `[el sistema se encuentre en estado X (ej. sesión no autenticada, modo offline, procesamiento pendiente)]`, EL SISTEMA deberá `[bloquear la acción Y y mantener disponible únicamente la acción Z]`.
- **RF-03 (Unwanted / Exception):** SI `[el dato de entrada es nulo, corrupto, está fuera de rango permitido o el servicio externo falla]`, ENTONCES EL SISTEMA deberá `[rechazar la operación de forma segura, registrar el error y responder con el código y mensaje de error específico W]`.
- **RF-04 (Event-driven / Condition):** CUANDO `[el resultado supere el umbral crítico K]`, EL SISTEMA deberá `[despachar una alerta prioritaria, incluir los factores explicativos y requerir confirmación explícita del operador]`.
- **RF-05 (Ubiquitous):** EL SISTEMA deberá `[registrar en un log inmutable de auditoría cada cálculo ejecutado, identificador de transacción, marcas de tiempo y decisiones tomadas, sin incluir datos sensibles]`.

---

## 5. Requisitos No Funcionales (RNF)
<!-- GUÍA PARA EL LLM:
Establece límites cuantitativos de rendimiento, disponibilidad, seguridad y compatibilidad.
-->
- **RNF-01 (Rendimiento / Latencia):** El tiempo de respuesta para `[operación principal]` debe ser `< [X] ms/segundos` en el percentil 95 (`p95`).
- **RNF-02 (Seguridad & Privacidad):** Cero exposición de secretos o credenciales. Los datos sensibles deben almacenarse cifrados o mediante identificadores pseudoanonimizados.
- **RNF-03 (Concurrencia / Escalabilidad):** El sistema debe soportar al menos `[N]` solicitudes simultáneas sin degradación del servicio ni condiciones de carrera.
- **RNF-04 (Interoperabilidad / Contratos):** Los intercambios de datos deben utilizar formatos estándar y tipados `[ej. JSON Schema / OpenAPI 3.0 / Protobuf / etc.]`.

---

## 6. Casos Límite y Condiciones de Borde (Edge Cases)
<!-- GUÍA PARA EL LLM:
Anticipa fallos y situaciones extremas que suelen romper el software si no se diseñan de antemano:
-->
- **Valores Extremos o Fuera de Rango:** `[¿Qué ocurre si el valor numérico es negativo, cero, infinito o superior al máximo teórico? ej. monto = 0 o valor > 1.000.000].`
- **Datos Incompletos o Faltantes:** `[¿Qué ocurre si un registro no contiene atributos opcionales o si un campo obligatorio viene vacío?].`
- **Duplicidad y Concurrencia:** `[¿Qué ocurre si se envían dos solicitudes idénticas con milisegundos de diferencia? (Idempotencia requerida)].`
- **Entidades Nuevas o sin Historial (Cold Start):** `[¿Cómo responde el sistema ante un usuario nuevo o entidad sin datos históricos previos?].`
- **Fallas de Conectividad o Timeouts:** `[¿Qué ocurre si un servicio upstream tarda más de X segundos en responder? (Fallback o circuit breaker)].`

---

## 7. Fuera de Alcance Explícito (Out of Scope)
<!-- GUÍA PARA EL LLM:
Declara explícitamente lo que NO se construirá en este sprint/iteración. Esto protege al equipo de la dispersión de esfuerzos.
-->
- ❌ `[Funcionalidad avanzada planificada para versiones futuras (Fase 2).]`
- ❌ `[Integraciones con sistemas secundarios o proveedores no prioritarios en este MVP.]`
- ❌ `[Automatización total sin revisión humana (si se requiere validación operativa previa).]`
- ❌ `[Soporte para plataformas, protocolos o formatos heredados (legacy) no contemplados.]`

---

## 8. Criterios de Finalización (Definition of Done - DoD)
<!-- GUÍA PARA EL LLM:
Lista las condiciones objetivas y verificables para que la implementación de esta spec se considere 100% terminada.
-->
1. **100% de Requisitos Funcionales cubiertos:** Todos los RF (RF-01 a RF-0N) cuentan con pruebas automatizadas (`unitarias e integración`) pasando en verde.
2. **Casos Límite testeados:** Cada escenario de la sección 6 tiene al menos una prueba negativa o de borde asociada.
3. **Tipado y Calidad Estática:** Verificación de tipos (`[ej. mypy / tsc]`) y linters (`[ej. ruff / eslint]`) ejecutados con 0 errores y 0 warnings.
4. **Cobertura de Código:** Cobertura de pruebas igual o superior a `[ej. 90%]` en la lógica del módulo.
5. **Verificación End-to-End:** Demostración ejecutable (CLI, script de prueba o llamada de API de muestra) con casos de prueba exitosos documentados.

---

## 9. Dudas Abiertas y Supuestos
<!-- GUÍA PARA EL LLM:
Si al momento de generar la spec tienes dudas de diseño o dependes de una decisión de negocio, regístralas aquí con opciones recomendadas.
-->
- [ ] **[NECESITA ACLARACIÓN 1]:** `[¿Pregunta específica sobre una regla de negocio o umbral? (Opción A recomendada vs Opción B).]`
- [ ] **[NECESITA ACLARACIÓN 2]:** `[¿Pregunta sobre el comportamiento en caso de fallo externo? (Fallback silencioso vs Alerta explícita).]`

---

## ✅ Checklist de Calidad para el LLM (Autovalidación)
Antes de entregar esta spec al usuario:
- [ ] Cada RF inicia con la palabra clave EARS en mayúsculas (CUANDO, MIENTRAS, SI... ENTONCES, EL SISTEMA deberá).
- [ ] Ningún RF describe detalles internos de código (clases, tablas SQL, librerías); solo comportamiento observable.
- [ ] Los RNF contienen umbrales numéricos medibles.
- [ ] La sección de Casos Límite tiene al menos 3 escenarios extremos detallados.
- [ ] La sección Fuera de Alcance tiene al menos 2 exclusiones explícitas.
