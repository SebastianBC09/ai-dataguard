# Tasks

> **Estado: BORRADOR CONDICIONADO. Pendiente de aprobación académica.** Ninguna tarea está completada: los artefactos de E3 y E4 son un borrador y su verificación (revisión del equipo y del docente) no se ha realizado. E1 y E2 siguen pendientes de aprobación. **No consta en los documentos ninguna fecha de aprobación docente**; este plan no la inventa.
>
> **Coherencia con el Excel (`docs/academic/AI_DataGuard_Plan_de_Trabajo.xlsx`):** los grupos corresponden a E1-E8. Los 17 ítems con la numeración del Excel conservan su responsable y sus fechas. Los 18 ítems **(adicional)** no están en el Excel, tienen responsable "por asignar" y no cambian el alcance. Este cambio **no modifica el Excel**; las discrepancias están en `design.md` ("Discrepancias con el Excel y la guía").
>
> **Decisiones del equipo del 12 nov (D1 a D9, ver `design.md`, DC-14 a DC-22):** dos perfiles (Trabajador y Administrador), condiciones del proveedor, categoría de fundamento principal y secundarias, CT-05, datos sensibles y de menores, formatos (texto esencial; PDF complementario), rutas oficiales, terminología («controles funcionales transversales») y ajuste mínimo de `config.yaml`.
>
> **Discrepancias que afectan a las tareas:**
> - En el Excel, 4.1 (12-15 nov) termina antes que 3.2 (hasta el 17) y 3.3 (hasta el 21). Aquí 4.1 es el **borrador v0** y 4.3 la **revisión final** tras cerrar 3.2, 3.3 y 3.5.
> - También en el Excel, 4.2 (12 nov) termina antes que 4.1 (hasta el 15 nov); 2.2 (desde el 15 nov) empieza antes de que termine 2.1 (hasta el 16); y 5.2 (desde el 29 nov) empieza antes de que termine 5.1 (hasta el 1 dic). Esas dependencias se leen como **inicio parcial**; el Excel no se modifica.
> - El Excel (6.1) "diseña y ejecuta" los casos en E6. Aquí el plan de pruebas se redacta en E3 (3.4, v0) y E4 (4.7, v1), y E6 solo ejecuta.
> - Las fechas de E5 a E8 incluyen fines de semana (22 nov, 13 dic, 19 dic); se mantienen como están y quedan por confirmar.
>
> **Rutas oficiales (DC-20) y su equivalencia con el Excel:** `docs/project/project-charter.md` (Excel: `ficha-e1.md`), `docs/legal/legal-matrix.md` (Excel: `matriz-reglas.md`; las fuentes están en su sección 2, en lugar de `fuentes.md`) y `docs/testing/test-plan.md` (Excel: `casos-prueba.md`).
>
> **Formato de cada tarea:** responsable (Excel) · fechas (2026, del Excel) · dependencias · artefacto · cómo se verifica.

## 1. E1 - Selección y delimitación

- [ ] 1.1 Formular problema, usuarios y alcance en la ficha E1 (máx. 2 páginas). Verificación: la ficha existe, tiene como máximo 2 páginas medidas en el formato final e incluye usuario, problema, alcance y caso demo según la guía docente.
  - Responsable: Integrante 1 · 12 nov · Depende de: ninguna · Artefacto: `docs/project/project-charter.md` (borrador generado; Excel: `ficha-e1.md`)
- [ ] 1.2 Revisar E1 con el docente y registrar observaciones. Verificación: existe el registro de la revisión con la aprobación o las observaciones.
  - Responsable: Equipo completo · 13 nov · Depende de: 1.1 · Artefacto: acta u observaciones de revisión E1
- [ ] 1.3 (adicional) Consultar al docente **C4** (ubicación de los 3 escenarios), **C5** (seguimiento a compromisos) y **C7** (si las cinco reglas deben tener fundamento jurídico directo), e informarle de las rutas oficiales de los documentos. Verificación: respuesta del docente registrada por escrito; `design.md` y `specs/` se actualizan solo si cambia el alcance.
  - Responsable: por asignar · Depende de: 1.1 · Informa a: 1.1, 2.2, 2.4

## 2. E2 - Análisis jurídico y reglas

- [ ] 2.1 Investigar normativa y fuentes oficiales. Verificación: cada fuente tiene referencia completa, enlace oficial y fecha de consulta, y fue contrastada **por una persona del equipo** con el texto oficial; el borrador actual se leyó con asistencia de IA, sin verificación humana.
  - Responsable: Integrante 2 · 13-16 nov · Depende de: ninguna · Artefacto: `docs/legal/legal-matrix.md`, sección 2 (borrador generado; Excel: `fuentes.md`)
- [ ] 2.2 Documentar 5 reglas con condición, evidencia y resultado (`RJ-01` a `RJ-05`). Verificación: cada regla tiene condición, resultado, fundamento con fuente verificada o la marca "pendiente de fuente", categoría de fundamento principal y secundarias, y tipo (regla jurídica preliminar o control funcional).
  - Responsable: Integrante 2 · 15-19 nov · Depende de: 2.1 (inicio parcial: en el Excel solapan el 15-16 nov) y 2.4 · Artefacto: `docs/legal/legal-matrix.md` (borrador generado; Excel: `matriz-reglas.md`)
- [ ] 2.3 Solicitar validación docente de E2. Verificación: registro de revisión E2 con aprobación o con observaciones.
  - Responsable: Equipo completo · 19 nov · Depende de: 2.2 · Artefacto: registro de revisión E2
- [ ] 2.4 (adicional) Decidir qué temas ocupan las 5 reglas frente a los 7 puntos de dolor del Excel y confirmar el tipo de `RJ-03` y `RJ-05` (consulta C7). Verificación: decisión registrada en `docs/legal/` y en `design.md`.
  - Responsable: por asignar · Depende de: 2.1; informado por 1.3
- [ ] 2.5 (adicional) Reconciliar `RJ-01` a `RJ-05` de `specs/` y `design.md` con las reglas aprobadas en E2, usando `/opsx-update`. Verificación: los temas provisionales se reemplazan o confirman, las observaciones pendientes de la sección 10 de `legal-matrix.md` quedan atendidas o justificadas, y `openspec validate initial-mvp --strict` pasa.
  - Responsable: por asignar · Depende de: 2.3

## 3. E3 - Requisitos y diseño conceptual

- [ ] 3.1 Redactar propuesta, alcance y exclusiones. Verificación: `proposal.md` contiene problema, objetivos, alcance, exclusiones, capacidades, riesgos, dependencias y la marca de pendiente de aprobación; revisado por el equipo y el docente.
  - Responsable: Integrante 1 · 12 nov · Depende de: ninguna · Artefacto: `openspec/changes/initial-mvp/proposal.md` (borrador generado)
- [ ] 3.2 Especificar capacidades y escenarios SHALL/WHEN/THEN. Verificación: los cinco `spec.md` existen, `openspec validate initial-mvp --strict` pasa, cada requisito tiene al menos dos escenarios y los esenciales incluyen al menos uno negativo, de límite o de verificación de ausencia; el equipo los revisó.
  - Responsable: Integrante 1 · 12-17 nov · Depende de: 3.1 · Artefacto: `openspec/changes/initial-mvp/specs/` (borrador generado)
- [ ] 3.3 Definir roles, datos, privacidad y decisiones abiertas. Verificación: `design.md` distingue decisiones acordadas, propuestas, decisiones que requieren aprobación docente y riesgos abiertos, y no nombra tecnologías.
  - Responsable: Integrante 3 · 14-21 nov · Depende de: 3.1 · Artefacto: `openspec/changes/initial-mvp/design.md` (borrador generado)
- [ ] 3.4 (adicional) Redactar el plan de pruebas **v0** con `CP-01` a `CP-13` (10 mínimos y 3 adicionales): pasos, datos sintéticos y resultado esperado, sin resultados reales, e incluir las verificaciones documentales `VD-01` a `VD-03`. Verificación: al menos 10 casos, cada `RJ` y cada capacidad cubiertos por los mínimos, y todos marcados "previsto, no ejecutado".
  - Responsable: por asignar · Depende de: 3.2 · Artefacto: `docs/testing/test-plan.md` (borrador generado; Excel: `casos-prueba.md`)
- [ ] 3.5 (adicional) Resolver con el equipo las decisiones O-02 a O-10 que sigan pendientes y que afecten a `specs/` (O-01 ya fue decidida: DC-14), y validar los criterios provisionales (marcas, máscara, certeza, listas de sensibilidad y de menores, condiciones del proveedor). Verificación: cada decisión pasa a "acordada" o sigue "abierta" con motivo, y `specs/` queda coherente.
  - Responsable: por asignar · Depende de: 3.3

## 4. E4 - Plan de construcción y trazabilidad

- [ ] 4.1 Desglosar tareas y criterios de finalización (**borrador v0**). Verificación: este `tasks.md` existe, cada tarea tiene resultado verificable y ninguna tarea futura está marcada como completada.
  - Responsable: Integrante 3 · 12-15 nov · Depende de: 3.1 · Artefacto: `openspec/changes/initial-mvp/tasks.md` (borrador generado)
- [ ] 4.2 Adaptar el plan de trabajo y registrar dependencias. Verificación: el Excel refleja los ítems de este `tasks.md` y sus dependencias, y las fechas coinciden. El equipo decide si lo hace.
  - Responsable: Equipo completo · 12 nov · Depende de: 4.1 (borrador v0 parcial: en el Excel 4.2 termina antes que 4.1) · Artefacto: `AI_DataGuard_Plan_de_Trabajo.xlsx` (no lo modifica este cambio)
- [ ] 4.3 (adicional) **Revisión final** de `tasks.md` tras cerrar 3.2, 3.3 y 3.5. Verificación: las dependencias coinciden con el contenido final de `specs/` y `design.md`, y `openspec validate initial-mvp --strict` pasa.
  - Responsable: por asignar · Hasta: cierre de E4 (21 nov, Excel) · Depende de: 3.2, 3.3, 3.5
- [ ] 4.4 (adicional) **Hito C3:** registrar la decisión del stack tecnológico, con criterios derivados de la guía docente (web, computador o celular; sin pagos; IA opcional; entorno controlado; persistencia; informe exportable). Verificación: decisión registrada en `design.md` con alternativas y aprobación; esta tarea **no** elige ninguna tecnología. Fecha límite: cierre de E4 (21 nov, Excel), antes de E5 (22 nov). La fecha de aprobación docente no está definida; si la decisión no está aprobada, E5 no inicia.
  - Responsable: por asignar · Depende de: 3.3 y confirmación docente (DA-05) · Bloquea: 5.1 a 5.6 · No bloquea: la revisión de `specs/`
- [ ] 4.5 (adicional) Priorizar el orden de entrega (fases A, B y C de `design.md`) y confirmar las funciones obligatorias para E6, sin eliminar capacidades. Verificación: lista con responsable y fecha por fase, aprobada por el equipo (DA-04).
  - Responsable: por asignar · Depende de: 3.5
- [ ] 4.6 (adicional) Asignar responsables de E5 a E8. Verificación: no queda ningún "Por asignar" en el Excel para E5-E8.
  - Responsable: Equipo completo · Depende de: 4.5
- [ ] 4.7 (adicional) Redactar el plan de pruebas **v1**: fijar resultados esperados que dependen de las reglas aprobadas y de las decisiones pendientes, y completar `VD-01` a `VD-03` y los datos de la sección 6 del plan. Verificación: cada `CP` referencia sus requisitos y sus `RJ` validadas; si E2 no está aprobada, los casos dependientes quedan marcados "provisional".
  - Responsable: por asignar · Hasta: cierre de E4 (21 nov, Excel) · Depende de: 3.4 y de E2 aprobada (2.3)

## 5. E5 - Construcción funcional (futura)

> Fuera de esta fase. No inicia hasta que E1 y E2 estén aprobadas y C3 esté decidida y aprobada. Se ejecutaría con `/opsx-apply` solo tras aprobación. Orden: primero la fase A (flujo mínimo), luego la B (salvaguardas).

- [ ] 5.1 Flujo de análisis, clasificación y advertencias (fase A). Verificación: se cumplen los escenarios de `document-analysis` (DOC-01, 02, 05, 07) e `information-classification` (CLA-01 a 05) con datos sintéticos, y pasan `CP-01`, `CP-02`, `CP-03` y `CP-08`.
  - Responsable: por asignar (Excel) · 22 nov - 1 dic · Depende de: 2.5, 4.4, 4.6, 4.7
- [ ] 5.2 Políticas, proveedores, auditoría e informes (fases A y B). Verificación: se cumplen los escenarios de `compliance-policies`, `ai-provider-catalog` y `assessment-reports` en sus requisitos esenciales, y pasan `CP-04`, `CP-05`, `CP-06`, `CP-07` y `CP-12`.
  - Responsable: por asignar (Excel) · 29 nov - 6 dic · Depende de: 5.1 (inicio parcial: en el Excel solapan el 29 nov - 1 dic) y 2.5
- [ ] 5.3 (adicional) Permisos por perfil (Trabajador y Administrador) según la matriz de `design.md` (DOC-01, CLA-06, POL-10, REP-04, REP-06, REP-08). Verificación: `CP-11` pasa y ningún perfil accede a acciones no permitidas.
  - Responsable: por asignar · Depende de: 3.5, 4.4
- [ ] 5.4 (adicional) Privacidad y minimización: descarte del original, enmascarado, registro mínimo y controles funcionales de `RJ-05` (DOC-04, 06, 08; REP-03, 05, 07; POL-07). Verificación: `CP-09`, `CP-10` y `CP-13` pasan; el registro no contiene contenido original ni valores sensibles completos.
  - Responsable: por asignar · Depende de: 3.5, 4.4
- [ ] 5.5 (adicional) Datos de ejemplo sintéticos para demostración y pruebas, conforme a la sección 6 del plan de pruebas (datos `DS-xx`, proveedores `PF-x` y políticas `PO-xx`), incluido un catálogo de proveedores precargado. Verificación: revisión del conjunto confirma que no hay datos reales ni contraseñas visibles y que todo está marcado como sintético o «ejemplo».
  - Responsable: por asignar · Depende de: 3.4
- [ ] 5.6 (adicional) Requisitos complementarios (fase C: DOC-03 PDF con texto extraíble, DOC-09, DOC-10; PRV-04, PRV-05; REP-09), solo si el plazo lo permite. Verificación: para cada uno que se implemente, sus escenarios se cumplen; los no implementados quedan listados como pendientes.
  - Responsable: por asignar · Depende de: 5.1, 5.2, 5.4

## 6. E6 - Pruebas y revisión legal (futura)

- [ ] 6.1 Ejecutar los casos de prueba (mínimo 10). Verificación: cada caso ejecutado tiene evidencia real (resultado, fecha, persona); ningún resultado se registra antes de ejecutarlo. Nota: el Excel dice "diseñar y ejecutar"; el diseño ya se hizo en 3.4 y 4.7.
  - Responsable: por asignar (Excel) · 7-11 dic · Depende de: 4.7, 5.1, 5.2, 5.3, 5.4 · Artefacto: actas de ejecución según `docs/testing/test-plan.md` (Excel: `casos-prueba.md`)
- [ ] 6.2 Revisar la trazabilidad de las 5 reglas y corregir defectos, incluidas las verificaciones documentales `VD-01` a `VD-03` del plan de pruebas (catálogo precargado, registro de reglas y bordes de la entrada de texto). Verificación: cada `RJ` aprobada en E2 se relaciona con requisitos y pruebas; los defectos están registrados con su estado.
  - Responsable: por asignar (Excel) · 11-13 dic · Depende de: 6.1, 2.5 · Artefacto: evidencias y registro de defectos
- [ ] 6.3 (adicional) Confirmar que las funciones obligatorias priorizadas pasan sus pruebas. Verificación: lista de funciones obligatorias con estado aprobado, y defectos pendientes listados.
  - Responsable: por asignar · Depende de: 4.5, 6.1

## 7. E7 - Documentación y entrega (futura)

- [ ] 7.1 Preparar manual, autoría, licencias y pendientes. Verificación: los documentos existen e incluyen instalación, uso, autoría por integrante, licencias y pendientes (incluidos C3, C4, C5 y C7 con su estado final).
  - Responsable: por asignar (Excel) · 14-17 dic · Depende de: 6.2 · Artefacto: `docs/user-guide/` (sin ruta oficial en `config.yaml`; por definir), `docs/project/`
- [ ] 7.2 Organizar la carpeta EQUIPO_AIDATAGUARD en OneDrive. Verificación: la carpeta contiene plan de proyecto, aplicación, análisis y diseño, pruebas, documentos de soporte y resultado del caso.
  - Responsable: Equipo completo · 17-18 dic · Depende de: 7.1 · Artefacto: paquete final en OneDrive
- [ ] 7.3 (adicional) Incluir el informe exportado de un caso y los aportes individuales. Verificación: el informe exportado proviene de una evaluación real con datos sintéticos y cada integrante tiene su aporte descrito.
  - Responsable: por asignar · Depende de: 6.1
- [ ] 7.4 (adicional) Verificar que el historial de cambios del repositorio registre qué cambió, quién y cuándo, y versionar los documentos de `docs/` y los cambios de OpenSpec que hoy no están en un commit. Verificación: el historial de versiones muestra autores y fechas de los artefactos.
  - Responsable: por asignar · Depende de: 7.1

## 8. E8 - Demostración y sustentación (futura)

- [ ] 8.1 Ensayar los 3 escenarios y la participación de los integrantes. Verificación: guion y evidencias de los ensayos con `ED-1`, `ED-2` y `ED-3` dentro de los 15 minutos; `ED-1` incluye la evidencia de privacidad (conexiones externas bloqueadas, controles CT-01 a CT-05 «aplicado» y revisión del registro sin el texto evaluado).
  - Responsable: Equipo completo · 19-21 dic · Depende de: 6.3, 7.2 · Artefacto: guion y evidencias de demostración
- [ ] 8.2 (adicional) Preparar que cada integrante pueda responder preguntas sobre la parte que aportó. Verificación: lista de preguntas ensayadas por integrante.
  - Responsable: Equipo completo · Depende de: 8.1

## Workflow follow-up

- Revisar `proposal.md`, `specs/`, `design.md` y `tasks.md` con el equipo y el docente antes de cualquier implementación.
- Ejecutar `openspec validate initial-mvp --strict` tras cada corrección con `/opsx-update`; la validación indica solo estructura correcta, no aprobación académica.
- No ejecutar `/opsx-apply` hasta que E1 y E2 estén aprobadas, C3 esté decidida y aprobada, y el plan esté aprobado.
- Archivar el cambio solo con las tareas completas y verificadas y la validación estricta sin errores.
