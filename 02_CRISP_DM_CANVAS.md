# 📋 Canvas Estratégico y Descubrimiento de Producto (CRISP-DM Canvas)
> **Metodología:** Adaptación de CRISP-DM (Cross-Industry Standard Process for Data Mining) al ciclo moderno de desarrollo de software, productos impulsados por datos e Inteligencia Artificial (Lean AI / Data-Product Canvas).

---

<!-- GUÍA PARA EL LLM:
Este documento sirve para alinear la visión del negocio con la viabilidad técnica antes de escribir cualquier especificación formal (spec.md) o código.
Tu objetivo al completar o asistir en este canvas es:
1. Asegurar que el problema de negocio esté claramente definido antes de proponer soluciones técnicas o modelos.
2. Cuantificar el éxito con métricas de negocio reales (KPIs), no solo métricas técnicas (ej. no solo 'accuracy' o 'latencia', sino 'ahorro de horas', 'reducción de errores', 'conversión').
3. Forzar el análisis de viabilidad, datos y riesgos tempranamente (Data Leakage, fatiga de alertas, balance costo-beneficio).
4. No asumas supuestos no documentados: si falta información clave, márcala con [PENDIENTE: stakeholder] o formula preguntas directas al usuario.
-->

## 📌 Metadatos del Proyecto
- **Nombre del Producto / Sistema:** `[Nombre del producto o módulo]`
- **Organización / Empresa / Cliente:** `[Nombre de la organización o contexto]`
- **Equipo Responsable:** `[Roles o nombres de los responsables: Product Owner, Tech Lead, Data/Software Engineer]`
- **Vertical o Dominio de Negocio:** `[ej. Fintech / E-commerce / SaaS B2B / Logística / Salud / EdTech / Ciberseguridad / etc.]`
- **Fecha & Versión:** `[YYYY-MM-DD • Versión 1.0-draft]`

---

## 🎯 Pregunta Estratégica HMW (How Might We? / ¿Cómo podríamos?)

<!-- GUÍA PARA EL LLM:
Formula una única pregunta estratégica orientada a la oportunidad. 
Usa la fórmula:
"¿Cómo podríamos [acción o capacidad de la solución] para [usuario o actor principal] de modo que [beneficio o impacto medible] sin [fricción, riesgo o costo principal]?"

Ejemplos multi-dominio:
- Fintech: "¿Cómo podríamos detectar transacciones potencialmente fraudulentas para analistas de riesgo antes de 300 ms de modo que reduzcamos pérdidas en un 35% sin incrementar la tasa de falsos positivos en clientes legítimos?"
- E-commerce: "¿Cómo podríamos recomendar repuestos compatibles a usuarios no técnicos en el carrito de compras de modo que aumente el ticket promedio en 15% sin saturar la pantalla con opciones irrelevantes?"
- Logística: "¿Cómo podríamos predecir retrasos en rutas de entrega de última milla para despachadores en tiempo real de modo que se reorganicen pedidos 2 horas antes sin elevar los costos de combustible?"
- Salud / SaMD: "¿Cómo podríamos anticipar el riesgo de descompensación en pacientes crónicos para el equipo médico ambulatorio de modo que se prevengan reingresos en un 20% sin generar fatiga de alarmas?"
-->

**Tu pregunta HMW:**  
`¿Cómo podríamos [acción clave] para [usuario objetivo] de modo que [impacto de negocio/usuario cuantificable] sin [riesgo o fricción principal]?`

---

## 📊 Matriz 2x2 de Priorización (Impacto de Negocio vs. Factibilidad Técnica/Datos)

<!-- GUÍA PARA EL LLM:
Evalúa la iniciativa con criterios objetivos para ubicarla en la matriz y justificar si vale la pena construirla ahora.
- Impacto: Grado en que resuelve un dolor crítico, genera ingresos o evita costos/riesgos mayores.
- Factibilidad: Disponibilidad de datos/APIs, claridad de requisitos, complejidad algorítmica y esfuerzo de ingeniería.
-->

- **Impacto de Negocio / Asistencial (Alto / Medio / Bajo):** `[Alto / Medio / Bajo]`
  - *Justificación del Impacto:* `[¿Qué métrica de negocio mejora, qué riesgo mitiga o qué dolor severo resuelve? Justifica con argumentos cualitativos o cuantitativos.]`
- **Factibilidad Técnica y de Datos (Alta / Media / Baja):** `[Alta / Media / Baja]`
  - *Justificación de Factibilidad:* `[¿Están disponibles los datos/APIs? ¿La infraestructura actual lo soporta? ¿Existe riesgo regulatorio o dependencias externas complejas?]`
- **Cuadrante Resultado:**  
  - [ ] ⭐ **Quick Win** *(Alto Impacto / Alta Factibilidad)* → Candidato ideal para MVP inmediato.  
  - [ ] 🏆 **Proyecto Estratégico** *(Alto Impacto / Media-Baja Factibilidad)* → Requiere fase de arquitectura/datos previa.  
  - [ ] ⚠️ **Baja Prioridad** *(Bajo Impacto / Alta Factibilidad)* → Automatización menor o backlog secundario.  
  - [ ] ❌ **Trampa de Esfuerzo** *(Bajo Impacto / Baja Factibilidad)* → Descartar inmediatamente.

---

## 🧱 Tablero Canvas CRISP-DM (6 Cuadrantes Adaptados a Software & Datos)

### 🟦 1. Comprensión del Negocio / Problema (Business Understanding)
<!-- GUÍA PARA EL LLM:
Enfócate en el problema humano y económico, NO en la tecnología. Evita decir 'necesitamos una IA'; explica qué falla hoy en el proceso manual o sistema existente.
-->
- **Problema Concreto y Dolor Actual:**  
  `[Describe el cuello de botella actual, ineficiencia, error recurrente o costo financiero/operativo que motiva este proyecto.]`
- **Stakeholder Sponsor & Dueño del Proceso:**  
  `[¿Quién patrocina el proyecto y qué rol es responsable de validar el éxito de la solución?]`
- **Decisión u Operación que Cambiará con la Solución:**  
  `[¿Qué acción específica tomará un usuario o un proceso automatizado cuando el sistema emita un resultado, predicción o alerta? Si nada cambia tras la salida, el software carece de valor.]`
- **Métricas de Éxito de Negocio (KPI Cuantificable):**  
  `[Métrica objetiva con meta numérica. Ej: 'Reducir el tiempo de procesamiento de facturas de 45 min a 5 min', 'Disminuir la tasa de abandono de carrito en 8%', 'Aumentar detección temprana en un 25%'.]`

---

### 🟨 2. Comprensión del Entorno y Datos / Entradas (Data / System Understanding)
<!-- GUÍA PARA EL LLM:
Mapea qué información entra al sistema, de dónde proviene, su volumen y qué problemas de calidad se anticipan.
-->
- **Fuentes de Datos / Sistemas Upstream:**  
  `[APIs REST, Bases de Datos SQL/NoSQL, archivos CSV/Parquet, colas de mensajería (Kafka/RabbitMQ), telemetría, logs, inputs manuales de usuario.]`
- **Variables Críticas / Entidades del Dominio:**  
  `[Entidades y atributos indispensables para resolver el problema: demográficas, transaccionales, series temporales, eventos históricos, parámetros de configuración.]`
- **Calidad, Datos Faltantes y Sesgos Potenciales:**  
  `[¿Faltan datos de forma aleatoria (MAR) o sistemática (MNAR)? ¿Hay sesgo de muestreo, datos obsoletos, latencias de sincronización o valores inconsistentes?]`
- **Volumen Estimado y Frecuencia de Actualización:**  
  `[Tamaño histórico de la muestra/base de datos, transacciones por segundo (TPS), tasa de crecimiento mensual y modo de actualización (batch vs streaming).]`

---

### 🟪 3. Preparación de Datos / Contratos de Entrada (Data Preparation)
<!-- GUÍA PARA EL LLM:
Define cómo se transforman los insumos crudos en estructuras listas para el consumo del algoritmo, motor de reglas o módulo de software.
-->
- **Ventana de Observación / Contexto de Entrada ($X$):**  
  `[¿Qué historial o contexto temporal se toma en cuenta al momento de la evaluación? Ej: 'Últimas 5 transacciones del usuario', 'Historial clínico de 6 meses', 'Datos de telemetría de los últimos 10 minutos'.]`
- **Ventana de Desenlace / Salida Esperada ($Y$):**  
  `[¿En qué horizonte temporal o formato se predice o ejecuta la salida? Ej: 'Riesgo de fuga en los próximos 30 días', 'Clasificación instantánea de categoría', 'Score acumulado'.]`
- **Criterios de Inclusión y Exclusión:**  
  - *Inclusión:* `[Condiciones para que una entidad o registro sea procesado.]`  
  - *Exclusión:* `[Condiciones para descartar registros (ej. usuarios inactivos > 1 año, registros incompletos en campos clave, anomalías de prueba).]`
- **Ingeniería de Características / Transformaciones de Negocio:**  
  `[Cálculo de agregaciones, ratios, normalizaciones, transformaciones categóricas, cálculo de scores estandarizados o validaciones de esquema.]`
- **Protocolo Anti-Leakage (Cero Fuga de Información):**  
  `[¿Cómo garantizas que el sistema o modelo no use información del futuro o datos que no existirían en el momento de la inferencia en producción? Separación temporal estricta.]`

---

### 🟧 4. Arquitectura / Modelado / Lógica Central (Modeling & Core Logic)
<!-- GUÍA PARA EL LLM:
Establece la naturaleza de la solución técnica: ¿es un motor de reglas determinista, un modelo de Machine Learning supervisado/no supervisado, un sistema LLM/RAG, o un pipeline de cálculo?
-->
- **Naturaleza de la Tarea Técnica:**  
  `[ej. Clasificación binaria / Regresión / Motor de Reglas de Negocio / Clasificador LLM con Structured Outputs / Clustering / Sistema de Recomendación / Pipeline ETL]`
- **Estrategia de Partición y Validación:**  
  `[Split Train/Validation/Test estratificado por entidad o tiempo (ej. 70/15/15), validación cruzada temporal (Time-Series Split), pruebas con datos de reserva histórica.]`
- **Familias de Soluciones / Algoritmos Candidatos:**  
  - *Línea Base (Baseline simple e interpretable):* `[ej. Heurística / Reglas fijas / Regresión Logística / Modelo determinista]`  
  - *Solución Avanzada:* `[ej. XGBoost / LightGBM / Transformer / Agente con Embeddings]`
- **Manejo de Desbalanceo, Incertidumbre y Calibración:**  
  `[Estrategias para clases minoritarias (SMOTE, Class Weights), ajuste de umbral de decisión (Threshold Tuning) y calibración de probabilidades (Platt scaling / Isotonic).]`

---

### 🟩 5. Evaluación Técnica y de Valor (Evaluation)
<!-- GUÍA PARA EL LLM:
Separa las métricas técnicas de las métricas operativas. Un modelo puede tener buen AUC pero destruir valor si el costo del falso positivo es inaceptable.
-->
- **Métricas Técnicas Prioritarias:**  
  `[Precisión, Recall, PR-AUC, ROC-AUC, F1-Score, MAE/RMSE, Latencia de inferencia p95/p99, Throughput (req/s).]`
- **Análisis de Costo-Beneficio de Decisiones (Decision Analysis):**  
  `[¿Cuál es el costo de un Falso Positivo (falsa alarma, fricción al usuario) vs. el costo de un Falso Negativo (evento crítico ignorado)? Definir umbral de corte óptimo.]`
- **Auditoría de Equidad, Sesgos y Robustez (Fairness & Bias):**  
  `[Verificación de paridad de desempeño por segmentos demográficos, geográficos o tipos de cuenta. Evaluación ante entradas maliciosas o ruido.]`
- **Criterio Formal de Aprobación para Producción (Go / No-Go):**  
  `[Condiciones mínimas innegociables para autorizar despliegue (ej. 'Precision > 0.85 con Recall > 0.75 y latencia < 200ms en el set de prueba independiente').]`

---

### 🟥 6. Despliegue, Integración y Ciclo de Vida (Deployment & Operations)
<!-- GUÍA PARA EL LLM:
Diseña cómo vivirá el sistema en producción dentro del flujo del usuario real, cómo se evitará la fricción operativa y cómo se monitoreará el deterioro con el tiempo.
-->
- **Modo de Ejecución e Inferencia:**  
  `[API REST síncrona / Inferencia en tiempo real (event-driven) / Procesamiento batch programado (cron/nightly) / Worker en segundo plano / Integración por Webhook]`
- **Estrategia de Interfaz & Prevención de Fatiga:**  
  `[¿Cómo se presenta el resultado al usuario para no saturarlo? (ej. alertas escalonadas solo para riesgo alto, tarjetas informativas contextuales, explicabilidad en 1 pantalla).]`
- **Monitoreo Continuo y Detección de Deriva (Drift Monitoring):**  
  `[Monitoreo de Data Drift (cambio en la distribución de inputs: test KS / PSI), Concept Drift (deterioro de métricas de negocio), errores HTTP y latencia p99.]`
- **Plan de Contingencia, Reentrenamiento y Gobernanza:**  
  `[Fallback determinista si el modelo/API falla (circuito cerrado o degradación elegante), política de actualización periódica y supervisión humana (Human-in-the-loop).]`

---

## ✅ Checklist de Calidad para el LLM (Autovalidación)
Antes de dar por cerrado este canvas, verifica:
- [ ] La pregunta HMW contiene actor, beneficio medible y fricción a evitar.
- [ ] El cuadrante de priorización está justificado tanto por impacto como por viabilidad.
- [ ] La métrica de negocio (KPI) del cuadrante 1 es cuantitativa y comprobable.
- [ ] Se contempló explícitamente el protocolo anti-leakage en el cuadrante 3.
- [ ] El criterio de Go / No-Go en el cuadrante 5 tiene umbrales numéricos definidos.
- [ ] El modo de despliegue en el cuadrante 6 especifica cómo se integrará con el usuario o sistema final.
