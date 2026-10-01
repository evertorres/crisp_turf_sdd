# 📜 Constitución del Proyecto: Principios Innegociables de Ingeniería de Software
> **Ubicación en el repositorio:** `docs/constitution.md`  
> **Metodología:** Spec-Driven Development (SDD) — Marco de Gobernanza Técnica y Restricciones Arquitectónicas.

---

<!-- GUÍA PARA EL LLM:
La Constitución define las reglas inviolables del repositorio. Todo agente de IA, desarrollador o revisor de código debe obedecer estos principios en cada archivo creado, modificado o refactorizado.

Al generar o adaptar esta constitución para un proyecto específico:
1. Redacta entre 6 y 8 principios cortos, directos y deterministas.
2. Cada principio debe ser objetivamente verificable mediante herramientas automáticas (linters, typecheckers, tests) o inspección de PR.
3. Máximo 15-25 líneas de texto en total en el archivo final. Evita prosa vaga como 'escribir código limpio'; exige 'cobertura de tests >= X%' o 'tipado estricto sin ANY'.
4. No comiences a implementar código hasta que el humano haya aprobado explícitamente esta constitución.
-->

## 📌 Metadatos
- **Proyecto:** `[Nombre del Proyecto]`
- **Stack Técnico Principal:** `[ej. Python 3.12+ / TypeScript 5+ / Rust / Go / etc.]`
- **Herramientas de Verificación:** `[ej. pytest + mypy + ruff / jest + tsc + eslint / etc.]`
- **Versión & Estado:** `[v1.0 • Aprobado / Pendiente de Aprobación]`

---

## 🏛️ Principios Innegociables

1. **Integridad del Dominio y Falla Segura (Fail-Safe First):**  
   Ante datos de entrada ambiguos, corruptos, fuera de rango o caídas de servicios externos, el sistema fallará de manera controlada, segura y transparente, notificando el error sin alterar estados ni tomar decisiones a ciegas.

2. **Tipado Estricto y Validación en Fronteras:**  
   Todo dato que cruce los límites del sistema (APIs, bases de datos, mensajes, inputs de usuario) debe validarse estrictamente mediante esquemas tipados (`[ej. Pydantic v2 / Zod / Schemas tipados]`). Queda prohibido el uso de tipos genéricos no seguros (`Any`, `Object`, `dict` sin tipar) en funciones de negocio. La verificación estática (`[ej. mypy / tsc]`) debe pasar con cero errores y cero advertencias.

3. **Desarrollo Guiado por Pruebas (Test-First Innegociable):**  
   Ninguna función de negocio, cálculo o endpoint se implementará sin escribir previamente su respectiva prueba unitaria o de integración. La suite de pruebas (`[ej. pytest / vitest]`) debe mantenerse en verde permanentemente. Cobertura mínima obligatoria: **`[ej. >= 85% o >= 90%]`** en lógica de dominio.

4. **Privacidad, Seguridad y Cero Fuga de Secretos (Zero Leakage):**  
   Prohibido registrar información personal identificable (PII), credenciales, API keys o datos confidenciales en logs, trazas de error o repositorios. Se emplearán identificadores pseudoanonimizados y variables de entorno seguras para credenciales.

5. **Arquitectura Modular y Desacoplamiento (Clean / Hexagonal Core):**  
   La lógica de negocio central (dominio) debe permanecer completamente desacoplada de frameworks web, librerías de infraestructura, clientes HTTP o mecanismos de persistencia. Los servicios externos se consumirán a través de interfaces/adaptadores intercambiables.

6. **Estándares y Lenguaje Ubicuo del Dominio:**  
   Toda variable, entidad, evento y mensaje de error debe alinearse con la terminología oficial del negocio (`[ej. glosario del dominio, códigos estándar o nomenclatura aprobada]`). Prohibido inventar alias o sinónimos ambiguos en el código.

7. **Alcance Delimitado y Cero 'Vibe Coding':**  
   Prohibido agregar heurísticas no documentadas, atajos informales, optimizaciones prematuras o librerías externas que no hayan sido formalmente requeridas y aprobadas en la especificación activa (`spec.md`).

8. **Verificabilidad Determinista en CI/CD:**  
   Todo cambio debe superar la suite completa de tests, chequeo de tipos y linters con un único comando local antes de ser integrado. Si una sola prueba falla, la tarea se considera incompleta.

---

## ✅ Checklist de Validación para el LLM al Adaptar este Archivo:
- [ ] ¿Los principios son verificables por un comando o regla objetiva?
- [ ] ¿El stack técnico (lenguaje, linter, test runner) está explícitamente nombrado?
- [ ] ¿El umbral de cobertura de tests tiene un porcentaje numérico exacto?
- [ ] ¿Se eliminaron todas las referencias a dominios o proyectos anteriores?
- [ ] ¿El archivo final es conciso y no supera las 25-30 líneas útiles?
