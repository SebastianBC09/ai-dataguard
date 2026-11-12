# Proposal

> **Estado: BORRADOR CONDICIONADO. Pendiente de aprobación académica.**
> E1 (selección y delimitación) y E2 (análisis del contexto legal) **no han sido aprobadas** por el docente. Todo lo que dependa de ellas se marca como provisional. Esta propuesta es solo especificación y planificación; no hay código, ni stack, ni funcionalidad implementada.

## Why

Los trabajadores de organizaciones colombianas, en especial de pequeñas y medianas empresas, pueden introducir datos personales o información corporativa confidencial en herramientas de IA generativa sin conocer las condiciones del proveedor ni las implicaciones jurídicas. El análisis de riesgos del plan de trabajo señala como puntos de dolor la exposición de datos a IA externa, la divulgación de información reservada, la ausencia de políticas y la falta de trazabilidad. AI DataGuard apoya la decisión humana **antes** de divulgar, sin certificar cumplimiento jurídico. El proyecto integrador exige una especificación verificable antes de construir (E3 y E4).

## Problema y justificación

- **Problema:** no existe un paso preventivo, explicable y trazable entre el trabajador y la herramienta de IA generativa que le avise de datos sensibles, riesgos jurídicos preliminares y condiciones del proveedor.
- **Justificación académica:** la guía docente pide un problema real, un usuario concreto, una aplicación que se use de principio a fin y guarde información, y un plan verificable. La aplicación "apoya la revisión humana; no certifica cumplimiento legal ni sustituye asesoría jurídica".
- **Fuente de los riesgos:** hoja "Puntos de Dolor" de `docs/academic/AI_DataGuard_Plan_de_Trabajo.xlsx`. Sus pesos relativos (0,22 / 0,19 / 0,16 / 0,13 / 0,12 / 0,10 / 0,08) **no tienen fuente ni método documentado** en los archivos revisados. Deben tratarse como estimación del equipo hasta que se justifiquen.

## What Changes

- Se crea la especificación inicial del MVP de AI DataGuard en cinco capacidades: 43 requisitos con identificador estable (`DOC-`, `CLA-`, `POL-`, `PRV-`, `REP-`), `SHALL` y escenarios `WHEN/THEN`. Cada requisito está clasificado como MVP esencial (37) o complementario (6); la evolución posterior se documenta en `design.md`.
- Se redacta un diseño conceptual que separa decisiones acordadas, propuestas pendientes, decisiones que requieren aprobación docente, y riesgos y alternativas abiertos.
- Se distinguen **tres tipos de elementos de evaluación** (reglas jurídicas preliminares, políticas organizacionales y controles funcionales) y se separa la **clasificación de sensibilidad** del **resultado de riesgo**.
- Se unifica el comportamiento cuando **no se selecciona proveedor**: la evaluación continúa, queda registrada como incompleta y exige revisión humana ante hallazgos relevantes.
- Se define un plan de tareas alineado con las etapas E1-E8 y con el Excel, sin marcar nada futuro como completado, con el plan de pruebas preparado en E3-E4 y ejecutado en E6.
- Se documentan las cinco reglas con identificadores provisionales `RJ-01` a `RJ-05`, **sin** presentarlas como obligaciones confirmadas.
- Se incorporan las decisiones del equipo del 12 nov (D1 a D9: dos perfiles, condiciones del proveedor, categoría de fundamento principal y secundarias, CT-05, datos sensibles y de menores, formatos de entrada, rutas oficiales, terminología y configuración) y se mantienen abiertas C3, C4, C5, C7 y las decisiones O-xx pendientes.
- No se escribe código, no se selecciona stack y no se modifican los documentos del docente.

## Capabilities

### New Capabilities
- `document-analysis`: ingreso y análisis preventivo de texto directo (entrada esencial) y de PDF con texto extraíble (complementario), en un entorno controlado y sin transmisión de contenido a terceros; continúa aunque no haya proveedor seleccionado.
- `information-classification`: identificación de indicadores de sensibilidad y clasificación en Pública, Interna, Confidencial o Restringida, o «pendiente de revisión» cuando falta información, con la lista ampliada de datos sensibles y los indicios de datos de menores; nunca asigna «Pública» de forma automática.
- `compliance-policies`: evaluación de reglas jurídicas preliminares (`RJ-01` a `RJ-04`), políticas organizacionales y controles funcionales transversales (`RJ-05`), con resultados formulados como alertas que requieren revisión humana.
- `ai-provider-catalog`: consulta de condiciones de tratamiento de información de proveedores de IA generativa, con fuente y fecha de verificación; el proveedor es opcional y las condiciones que no intervienen en el resultado se presentan como información para revisión humana.
- `assessment-reports`: generación de informes, registro mínimo de evaluaciones y decisiones humanas, y trazabilidad.

### Modified Capabilities
<!-- Ninguna. El proyecto no tiene specs existentes (`openspec list --specs` vacío al crear este cambio). -->

## Usuarios

| Perfil | Necesidad | Estado |
|---|---|---|
| Trabajador | Evaluar un texto antes de usarlo con IA generativa y entender el motivo de cada alerta. | Decidido por el equipo (DC-14). |
| Administrador | Gestionar políticas organizacionales, revisar los casos pendientes (función de revisión de cumplimiento) y consultar evaluaciones y trazabilidad. | Decidido por el equipo (DC-14); pendiente de aprobación docente de E1. |

El responsable de cumplimiento no es un tercer perfil: es una responsabilidad asignable al Administrador (DC-14). Enfoque inicial: pymes colombianas. Se asume una sola organización por instancia (supuesto, ver O-09).

## Objetivos

1. Detectar y explicar indicadores de datos personales e información corporativa confidencial antes de su divulgación.
2. Evaluar el contenido frente a las cinco reglas jurídicas preliminares y frente a políticas organizacionales, sin emitir certificaciones.
3. Informar las condiciones de tratamiento de los proveedores de IA con fuente y fecha.
4. Registrar de forma mínima evaluaciones y decisiones humanas, sin conservar documentos originales salvo necesidad justificada.
5. Cumplir los mínimos académicos: 5 reglas documentadas, 10 casos de prueba previstos, 3 escenarios de demostración y un recorrido de evaluación de principio a fin con informe exportable.

## Alcance del MVP

- Recorrido de evaluación de principio a fin: ingreso, análisis, clasificación de sensibilidad, resultado de riesgo (reglas, políticas y controles), consulta opcional de proveedor, informe y registro de la decisión humana. Se entrega en fases: A (flujo mínimo), B (salvaguardas) y C (complementarios).
- Persistencia de la información pertinente, minimizada (ver `design.md`).
- Dos perfiles con permisos diferenciados: Trabajador y Administrador (DC-14).
- Datos de ejemplo sintéticos; ningún dato personal real ni contraseñas a la vista.

## Exclusiones

- Selección de stack, lenguajes, frameworks o bases de datos (aplazado, ver C3).
- Formatos de documento distintos del PDF con texto extraíble, que es complementario (DC-19).
- Cualquier implementación en esta fase (`/opsx-apply` y `/opsx-archive` no se ejecutan).
- Certificación de cumplimiento, dictámenes jurídicos o sustitución de asesoría jurídica.
- Transmisión de documentos sensibles a proveedores externos para evaluarlos.
- Capacidades o módulos distintos de las cinco acordadas.
- Pagos y funciones fuera de las cinco capacidades. La guía docente indica "sin pagos" y "la IA es opcional".
- Despliegue en producción y soporte multiorganización (supuesto, ver O-09).

## Trazabilidad académica

| Etapa | Fechas del Excel (2026) | Estado | Relación con este cambio |
|---|---|---|---|
| E1 Selección y delimitación | 12 nov | **Pendiente de aprobación docente** | Esta propuesta usa su alcance como borrador. |
| E2 Análisis jurídico y reglas | 13-19 nov | **Pendiente de aprobación docente** | Define `RJ-01` a `RJ-05` como marcadores. |
| E3 Requisitos y diseño | 12-21 nov | En borrador | `proposal`, `specs/`, `design` y plan de pruebas v0. |
| E4 Plan de construcción | 12-21 nov | En borrador | `tasks.md`, hito C3 y plan de pruebas v1. |
| E5 Desarrollo | 22 nov - 6 dic | Futuro | Fuera de esta fase. No inicia sin E1, E2 y C3 aprobadas. |
| E6 Pruebas y revisión | 7-13 dic | Futuro | 13 casos previstos (10 mínimos), **no ejecutados**; E6 solo los ejecuta. |
| E7 Plan y entrega | 14-18 dic | Futuro | Fuera de esta fase. |
| E8 Sustentación | 19-21 dic | Futuro | Tres escenarios previstos. |

## Tratamiento de las reglas jurídicas (`RJ-01` a `RJ-05`)

Los cinco identificadores son marcadores provisionales. Su contenido sale de E2 y aún no existe ni está aprobado. `docs/legal/legal-matrix.md` (borrador E2) asigna a cada regla un nombre y un objetivo derivados de la hoja "Puntos de Dolor" del Excel; son una hipótesis de trabajo, no contenido jurídico, y E2 puede reemplazarlos.

Se distinguen tres **tipos** de elementos de evaluación:

- **Reglas jurídicas preliminares** (`RJ-01` a `RJ-04`; `RJ-03` evalúa la existencia de políticas aplicables).
- **Políticas organizacionales**, definidas por el Administrador y no atribuidas a ninguna `RJ`.
- **Controles funcionales transversales** (`RJ-05`): reglas del propio sistema (sin transmisión externa, descarte del original, enmascarado, registro sin contenido, revisión humana), no detección de contenido.

Si las cinco reglas deben tener fundamento jurídico directo es una consulta docente abierta (**C7**).

Además, el fundamento de cada regla se clasifica en cuatro categorías, que se mantienen en los artefactos posteriores:

1. **Obligación legal respaldada por fuente verificada:** ninguna confirmada por verificación humana todavía; la matriz E2 localizó textos con asistencia de IA.
2. **Interpretación pendiente de revisión jurídica.**
3. **Política corporativa propuesta.**
4. **Regla funcional propia de AI DataGuard.**

Cada regla tiene una categoría principal y, si corresponde, categorías secundarias (DC-16). Los controles de `RJ-05` son decisiones funcionales del equipo y no se presentan como obligaciones legales específicas.

Fuentes de E2: la matriz `docs/legal/legal-matrix.md` (borrador) localizó y leyó, con asistencia de IA y **sin verificación humana**, la Ley 1581 de 2012, el Decreto 1377 de 2013 (compilado en el Decreto 1074 de 2015), la Circular Externa 002 de 2024 de la SIC, la Decisión 486 de la CAN y la Ley 256 de 1996, entre otras. Su aplicación a AI DataGuard sigue siendo interpretación pendiente de revisión jurídica.

## Decisiones abiertas (no resueltas)

| ID | Descripción original | Implicaciones | Estado |
|---|---|---|---|
| **C1** | Los nombres de archivo del plan no coincidían entre `config.yaml` y el Excel. | Decisión del equipo (DC-20): rutas oficiales `docs/project/project-charter.md`, `docs/legal/legal-matrix.md` y `docs/testing/test-plan.md`; equivalencia con el Excel en `design.md`. Falta informar al docente. | **Resuelta por el equipo** |
| **C3** | Selección del stack tecnológico. La guía exige una aplicación funcional (E5) y E4 dice "entorno inicia", pero la restricción vigente prohíbe elegir stack. | Se registra como **aplazada**. Las especificaciones funcionales no dependen de ella y no se bloquean. No se elige tecnología alguna. Hito: decidirla en la tarea 4.4, a más tardar al cierre de E4 (21 nov según el Excel) y antes de E5. La fecha de aprobación docente no está definida. | **Aplazada** |
| **C4** | El Excel pide 3 escenarios de demostración en la ficha E1 (máx. 2 páginas); la guía solo pide "caso demo" en E1 y los 3 escenarios en E8. | Define el contenido de la ficha E1. Hasta saberlo, `design.md` prepara los tres escenarios (`ED-1` a `ED-3`) como borrador. | **Abierta** (consulta docente) |
| **C5** | La guía docente define el proyecto como ayudar a "documentar decisiones y hacer seguimiento a compromisos". Las cinco capacidades no mencionan el seguimiento a compromisos. | Se cubre el registro de la decisión humana dentro de `assessment-reports`, pero **no** el seguimiento de compromisos. Falta confirmar con el docente si es obligatorio. No se agrega capacidad. | **Abierta** (consulta docente) |
| **C7** | (Nueva) No consta si las cinco reglas deben tener fundamento jurídico directo o se admiten reglas funcionales y controles funcionales. | Afecta sobre todo a `RJ-03` y `RJ-05` y al contenido de E2. | **Abierta** (consulta docente) |

Otras observaciones y decisiones, detalladas en `design.md`:

- **C2:** trazabilidad frente a minimización de datos. Se aborda conceptualmente; falta la revisión de E2.
- **C6:** `/opsx-propose` genera todos los artefactos juntos; el Excel los escalona por etapa y responsable.
- **O-01 a O-10:** decidida por el equipo, O-01 (dos perfiles, DC-14; pendiente de aprobación docente de E1). Parciales: O-02 (niveles y lista de sensibilidad ampliada), O-03 (formatos decididos; límite de tamaño pendiente), O-04 (condiciones decididas; origen del catálogo abierto) y O-08. Abiertas: O-05, O-06, O-07, O-09 y O-10.

## Riesgos

- **Cronograma:** E3 y E4 comienzan antes de aprobar E1 y E2, así que un rechazo del alcance puede forzar retrabajo. Mitigación: borrador condicionado y marcadores `RJ`.
- **Alcance frente a plazo:** cinco capacidades y 43 requisitos (37 esenciales) en 14 días de construcción (22 nov - 6 dic) con tres integrantes. Mitigación: entrega por fases A, B y C; falta confirmar las funciones obligatorias para E6.
- **Carga de revisión humana:** toda clasificación pendiente exige al Administrador en su función de revisión, incluso el contenido sin indicadores, y ahora también los datos sensibles y de menores; hay que medir si es excesivo.
- **Corrección jurídica:** riesgo de citar normas mal. Mitigación: ninguna regla se confirma sin fuente verificada por una persona.
- **Falsos negativos:** la ausencia de alertas no equivale a autorización para divulgar.
- **Datos de ejemplo:** deben ser sintéticos y claramente marcados.
- **Catálogo de proveedores desactualizado:** los términos cambian, así que cada dato lleva fuente y fecha de verificación.

## Dependencias

- Aprobación docente de E1 y E2.
- Investigación y validación de fuentes jurídicas (Integrante 2 según el Excel).
- Asignación de responsables para E5-E8 (hoy "Por asignar").
- Respuesta docente sobre C4, C5 y C7.
- Decisión y aprobación de C3 (stack) antes de iniciar E5; no consta fecha de aprobación docente.

## Impact

- **Código:** ninguno. Esta fase no implementa nada.
- **Archivos:** `openspec/changes/initial-mvp/` y `openspec/config.yaml` (ajuste mínimo de terminología y rutas, DC-22). Los borradores `docs/project/project-charter.md` (E1), `docs/legal/legal-matrix.md` (E2) y `docs/testing/test-plan.md` (plan de pruebas v0) existen fuera de este cambio y se mantienen sincronizados con él; **ninguno está aprobado** y la ejecución de las pruebas es de E6.
- **Documentos del docente:** no se modifican (`docs/academic/`).
- **Sistemas externos:** ninguno. Las condiciones de proveedores se tratan como catálogo con fuente y fecha, no como consulta en línea (propuesta, ver O-04).
