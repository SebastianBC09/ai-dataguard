# Tasks

> **Estado: BORRADOR CONDICIONADO. Pendiente de aprobación académica.** Ninguna tarea está completada: los artefactos de E3 y E4 se redactaron como borrador y su verificación (validación y revisión docente) no se ha realizado. E1 y E2 siguen pendientes de aprobación.
>
> **Coherencia con el Excel (`docs/academic/AI_DataGuard_Plan_de_Trabajo.xlsx`):** los grupos corresponden a E1-E8. Los ítems con la numeración del Excel (1.1, 1.2, 2.1...) conservan su responsable y fechas. Los ítems marcados **(adicional)** no están en el Excel, tienen responsable "por asignar" y no cambian el alcance; sirven para cubrir los requisitos de `specs/`. Este cambio no modifica el Excel.
>
> **Rutas de archivos (C1, abierta):** donde hay dos nombres, el primero es el de `config.yaml` y el segundo el del Excel. Ninguno está elegido.
>
> **Formato de cada tarea:** responsable (Excel) · fechas (2026) · dependencias · artefacto · cómo se verifica.

## 1. E1 - Selección y delimitación

- [ ] 1.1 Formular problema, usuarios y alcance en la ficha E1 (máx. 2 páginas). Verificación: la ficha existe, tiene máximo 2 páginas e incluye usuario, problema, alcance y caso demo según la guía docente.
  - Responsable: Integrante 1 · 12 nov · Depende de: ninguna · Artefacto: `docs/project/project-charter.md` / `docs/project/ficha-e1.md` (C1)
- [ ] 1.2 Revisar E1 con el docente y registrar observaciones. Verificación: existe el registro de la revisión y de la aprobación o las observaciones.
  - Responsable: Equipo completo · 13 nov · Depende de: 1.1 · Artefacto: acta u observaciones de revisión E1
- [ ] 1.3 (adicional) Consultar al docente C4 (ubicación de los 3 escenarios) y C5 (seguimiento a compromisos). Verificación: respuesta del docente registrada, y `design.md` y `specs/` actualizados si cambia el alcance.
  - Responsable: por asignar · Depende de: 1.1

## 2. E2 - Análisis jurídico y reglas

- [ ] 2.1 Investigar normativa y fuentes oficiales. Verificación: cada fuente tiene referencia completa, enlace oficial y fecha de consulta; ninguna se cita sin haberla leído.
  - Responsable: Integrante 2 · 13-16 nov · Depende de: ninguna · Artefacto: `docs/legal/fuentes.md`
- [ ] 2.2 Documentar 5 reglas con condición, evidencia y resultado (`RJ-01` a `RJ-05`). Verificación: cada regla tiene condición, resultado, fundamento con fuente verificada o la marca "pendiente de fuente", y categoría de fundamento.
  - Responsable: Integrante 2 · 15-19 nov · Depende de: 2.1 · Artefacto: `docs/legal/legal-matrix.md` / `docs/legal/matriz-reglas.md` (C1)
- [ ] 2.3 Solicitar validación docente de E2. Verificación: registro de revisión E2 con aprobación o con observaciones.
  - Responsable: Equipo completo · 19 nov · Depende de: 2.2 · Artefacto: registro de revisión E2
- [ ] 2.4 (adicional) Decidir cómo tratar los siete puntos de dolor del Excel con solo cinco reglas (RA-01). Verificación: decisión registrada en `docs/legal/` y en `design.md`.
  - Responsable: por asignar · Depende de: 2.2
- [ ] 2.5 (adicional) Reconciliar `RJ-01` a `RJ-05` de `specs/` y `design.md` con las reglas aprobadas en E2, usando `/opsx-update`. Verificación: los temas provisionales se reemplazan o confirman y `openspec validate initial-mvp` pasa.
  - Responsable: por asignar · Depende de: 2.3

## 3. E3 - Requisitos y diseño conceptual

- [ ] 3.1 Redactar propuesta, alcance y exclusiones. Verificación: `proposal.md` contiene problema, objetivos, alcance, exclusiones, capacidades, riesgos, dependencias y la marca de pendiente de aprobación; revisado por el equipo y el docente.
  - Responsable: Integrante 1 · 12 nov · Depende de: ninguna · Artefacto: `openspec/changes/initial-mvp/proposal.md` (borrador generado)
- [ ] 3.2 Especificar capacidades y escenarios SHALL/WHEN/THEN. Verificación: los cinco `spec.md` existen, `openspec validate initial-mvp --strict` pasa, cada requisito tiene escenarios positivos, negativos y límite, y el equipo los revisó.
  - Responsable: Integrante 1 · 12-17 nov · Depende de: 3.1 · Artefacto: `openspec/changes/initial-mvp/specs/` (borrador generado)
- [ ] 3.3 Definir roles, datos, privacidad y decisiones abiertas. Verificación: `design.md` distingue decisiones acordadas, propuestas, decisiones que requieren aprobación docente y riesgos abiertos, y no nombra tecnologías.
  - Responsable: Integrante 3 · 14-21 nov · Depende de: 3.1 · Artefacto: `openspec/changes/initial-mvp/design.md` (borrador generado)
- [ ] 3.4 (adicional) Redactar el plan de pruebas con `CP-01` a `CP-10`: pasos, datos sintéticos y resultado esperado, sin resultados reales. Verificación: existen al menos 10 casos, cada `RJ` y cada capacidad aparecen en al menos uno, y todos figuran como "previsto, no ejecutado".
  - Responsable: por asignar · Depende de: 3.2 · Artefacto: `docs/testing/test-plan.md` / `docs/testing/casos-prueba.md` (C1)
- [ ] 3.5 (adicional) Resolver con el equipo las decisiones O-01 a O-09 de `design.md` que afecten a `specs/`. Verificación: cada decisión pasa a "acordada" o sigue "abierta" con motivo, y `specs/` queda coherente.
  - Responsable: por asignar · Depende de: 3.3

## 4. E4 - Plan de construcción y trazabilidad

- [ ] 4.1 Desglosar tareas y criterios de finalización. Verificación: este `tasks.md` existe, cada tarea tiene resultado verificable y ninguna tarea futura está marcada como completada.
  - Responsable: Integrante 3 · 12-15 nov · Depende de: 3.2, 3.3 · Artefacto: `openspec/changes/initial-mvp/tasks.md` (borrador generado)
- [ ] 4.2 Adaptar el plan de trabajo y registrar dependencias. Verificación: el Excel refleja los ítems de este `tasks.md` y sus dependencias, y sus fechas coinciden.
  - Responsable: Equipo completo · 12 nov · Depende de: 4.1 · Artefacto: `AI_DataGuard_Plan_de_Trabajo.xlsx` (no lo modifica este cambio)
- [ ] 4.3 (adicional) Registrar la decisión del stack tecnológico (C3), cuando el equipo y el docente la aprueben, con criterios derivados de la guía docente. Verificación: decisión registrada en `design.md` con alternativas y aprobación; esta tarea no elige ninguna tecnología.
  - Responsable: por asignar · Depende de: 3.3 y confirmación docente (DA-05) · Bloquea: 5.1, 5.2, 5.3-5.5 · No bloquea: la revisión de `specs/`
- [ ] 4.4 (adicional) Priorizar las funciones obligatorias para E6 dentro de las cinco capacidades, sin eliminarlas. Verificación: lista priorizada con responsable y fecha por función, aprobada por el equipo (DA-04).
  - Responsable: por asignar · Depende de: 3.5
- [ ] 4.5 (adicional) Asignar responsables de E5 a E8. Verificación: no queda ningún "Por asignar" en el Excel para E5-E8.
  - Responsable: Equipo completo · Depende de: 4.4

## 5. E5 - Construcción funcional (futura)

> Fuera de esta fase. No inicia hasta que E1 y E2 estén aprobadas y C3 esté decidida. Se ejecutaría con `/opsx-apply` solo tras aprobación.

- [ ] 5.1 Flujo de análisis, clasificación y advertencias. Verificación: los escenarios de `document-analysis` e `information-classification` se cumplen con datos sintéticos y las pruebas `CP-01`, `CP-02`, `CP-03` y `CP-07` pasan.
  - Responsable: por asignar (Excel) · 22 nov - 1 dic · Depende de: 2.3, 2.5, 4.3, 4.5
- [ ] 5.2 Políticas, proveedores, auditoría e informes. Verificación: los escenarios de `compliance-policies`, `ai-provider-catalog` y `assessment-reports` se cumplen y las pruebas `CP-04`, `CP-05`, `CP-06` y `CP-10` pasan.
  - Responsable: por asignar (Excel) · 29 nov - 6 dic · Depende de: 5.1, 2.5
- [ ] 5.3 (adicional) Permisos por perfil según la matriz de `design.md`. Verificación: `CP-09` pasa y ningún perfil accede a acciones no permitidas.
  - Responsable: por asignar · Depende de: 3.5, 4.3
- [ ] 5.4 (adicional) Registro mínimo con descarte del contenido original. Verificación: `CP-08` pasa; el registro no contiene contenido original ni valores sensibles completos.
  - Responsable: por asignar · Depende de: 3.5, 4.3
- [ ] 5.5 (adicional) Datos de ejemplo sintéticos para demostración y pruebas. Verificación: revisión del conjunto confirma que no hay datos reales ni contraseñas visibles y que todo está marcado como sintético.
  - Responsable: por asignar · Depende de: 3.4

## 6. E6 - Pruebas y revisión legal (futura)

- [ ] 6.1 Diseñar y ejecutar mínimo 10 casos de prueba. Verificación: cada caso tiene evidencia de su ejecución real (resultado, fecha, persona) y los resultados no se registran antes de ejecutarlos.
  - Responsable: por asignar (Excel) · 7-11 dic · Depende de: 3.4, 5.1, 5.2 · Artefacto: `docs/testing/casos-prueba.md` / `docs/testing/test-plan.md` (C1)
- [ ] 6.2 Revisar la trazabilidad de las 5 reglas y corregir defectos. Verificación: cada `RJ` aprobada en E2 se relaciona con requisitos y pruebas; los defectos están registrados con su estado.
  - Responsable: por asignar (Excel) · 11-13 dic · Depende de: 6.1, 2.5 · Artefacto: evidencias y registro de defectos
- [ ] 6.3 (adicional) Confirmar que las funciones obligatorias priorizadas pasan sus pruebas. Verificación: lista de funciones obligatorias con estado aprobado, y defectos pendientes listados.
  - Responsable: por asignar · Depende de: 4.4, 6.1

## 7. E7 - Documentación y entrega (futura)

- [ ] 7.1 Preparar manual, autoría, licencias y pendientes. Verificación: los documentos existen e incluyen instalación, uso, autoría por integrante, licencias y pendientes (incluidos C1, C3 y C5 con su estado final).
  - Responsable: por asignar (Excel) · 14-17 dic · Depende de: 6.2 · Artefacto: `docs/user-guide/`, `docs/project/`
- [ ] 7.2 Organizar la carpeta EQUIPO_AIDATAGUARD en OneDrive. Verificación: la carpeta contiene plan de proyecto, aplicación, análisis y diseño, pruebas, documentos de soporte y resultado del caso.
  - Responsable: Equipo completo · 17-18 dic · Depende de: 7.1 · Artefacto: paquete final en OneDrive
- [ ] 7.3 (adicional) Incluir el informe exportado de un caso y los aportes individuales. Verificación: el informe exportado proviene de una evaluación real con datos sintéticos y cada integrante tiene su aporte descrito.
  - Responsable: por asignar · Depende de: 6.1
- [ ] 7.4 (adicional) Verificar que el historial de cambios del repositorio registre qué cambió, quién y cuándo. Verificación: el historial de versiones muestra autores y fechas de los artefactos. Hoy el repositorio no tiene commits.
  - Responsable: por asignar · Depende de: 7.1

## 8. E8 - Demostración y sustentación (futura)

- [ ] 8.1 Ensayar los 3 escenarios y la participación de los integrantes. Verificación: guion y evidencias de los ensayos, con `ED-1`, `ED-2` y `ED-3` cronometrados dentro de los 15 minutos.
  - Responsable: Equipo completo · 19-21 dic · Depende de: 6.3, 7.2 · Artefacto: guion y evidencias de demostración
- [ ] 8.2 (adicional) Preparar que cada integrante pueda responder preguntas sobre la parte que aportó. Verificación: lista de preguntas ensayadas por integrante.
  - Responsable: Equipo completo · Depende de: 8.1

## Workflow follow-up

- Revisar `proposal.md`, `specs/`, `design.md` y `tasks.md` con el equipo y el docente antes de cualquier implementación.
- Ejecutar `openspec validate initial-mvp --strict` tras cada corrección con `/opsx-update`.
- No ejecutar `/opsx-apply` hasta que E1 y E2 estén aprobadas, C3 esté decidida y el plan esté aprobado.
- Archivar el cambio solo con las tareas completas y verificadas y la validación estricta sin errores.
