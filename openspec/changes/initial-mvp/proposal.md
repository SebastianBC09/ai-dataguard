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

- Se crea la especificación inicial del MVP de AI DataGuard en cinco capacidades, con requisitos `SHALL` y escenarios `WHEN/THEN`.
- Se redacta un diseño conceptual que separa decisiones acordadas, propuestas pendientes, decisiones que requieren aprobación docente, y riesgos y alternativas abiertos.
- Se define un plan de tareas alineado con las etapas E1-E8 y con el Excel del plan de trabajo, sin marcar nada futuro como completado.
- Se documentan las cinco reglas jurídicas con identificadores provisionales `RJ-01` a `RJ-05`, **sin** presentarlas como obligaciones confirmadas.
- Se registran las decisiones abiertas C1, C3 y C5 (y otras observaciones) sin resolverlas.
- No se escribe código, no se selecciona stack y no se modifican los documentos del docente.

## Capabilities

### New Capabilities
- `document-analysis`: ingreso y análisis preventivo de documentos y textos, en un entorno controlado y sin transmisión de contenido a terceros.
- `information-classification`: identificación de indicadores de sensibilidad (datos personales e información corporativa confidencial) y asignación de un nivel de clasificación explicable.
- `compliance-policies`: evaluación de reglas jurídicas preliminares (`RJ-01` a `RJ-05`) y de políticas organizacionales, con resultados formulados como alertas que requieren revisión humana.
- `ai-provider-catalog`: consulta de condiciones de tratamiento de información de proveedores de IA generativa, con fuente y fecha de verificación.
- `assessment-reports`: generación de informes, registro mínimo de evaluaciones y decisiones humanas, y trazabilidad.

### Modified Capabilities
<!-- Ninguna. El proyecto no tiene specs existentes (`openspec list --specs` vacío al crear este cambio). -->

## Usuarios

| Perfil | Necesidad | Estado |
|---|---|---|
| Trabajador | Evaluar un texto o documento antes de usarlo con IA generativa y entender el motivo de cada alerta. | Acordado en `config.yaml`. |
| Administrador | Gestionar políticas organizacionales y consultar evaluaciones y trazabilidad. | Acordado en `config.yaml`. |
| Responsable de cumplimiento | Revisar casos ambiguos y registrar la decisión humana. | Acordado en `config.yaml`; **pendiente** definir si es un perfil distinto del Administrador (ver O-01). |

Enfoque inicial: pymes colombianas. Se asume una sola organización por instancia (supuesto, ver O-09).

## Objetivos

1. Detectar y explicar indicadores de datos personales e información corporativa confidencial antes de su divulgación.
2. Evaluar el contenido frente a las cinco reglas jurídicas preliminares y frente a políticas organizacionales, sin emitir certificaciones.
3. Informar las condiciones de tratamiento de los proveedores de IA con fuente y fecha.
4. Registrar de forma mínima evaluaciones y decisiones humanas, sin conservar documentos originales salvo necesidad justificada.
5. Cumplir los mínimos académicos: 5 reglas documentadas, 10 casos de prueba previstos, 3 escenarios de demostración y un recorrido de evaluación de principio a fin con informe exportable.

## Alcance del MVP

- Recorrido de evaluación de principio a fin: ingreso, análisis, clasificación, evaluación de reglas y políticas, consulta de proveedor, informe y registro de la decisión humana.
- Persistencia de la información pertinente, minimizada (ver `design.md`).
- Dos o tres perfiles con permisos diferenciados (sujeto a O-01).
- Datos de ejemplo sintéticos; ningún dato personal real ni contraseñas a la vista.

## Exclusiones

- Selección de stack, lenguajes, frameworks o bases de datos (aplazado, ver C3).
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
| E3 Requisitos y diseño | 12-21 nov | En borrador | `proposal`, `specs/`, `design`. |
| E4 Plan de construcción | 12-21 nov | En borrador | `tasks.md`. |
| E5 Desarrollo | 22 nov - 6 dic | Futuro | Fuera de esta fase. |
| E6 Pruebas y revisión | 7-13 dic | Futuro | Casos previstos, **no ejecutados**. |
| E7 Plan y entrega | 14-18 dic | Futuro | Fuera de esta fase. |
| E8 Sustentación | 19-21 dic | Futuro | Tres escenarios previstos. |

## Tratamiento de las reglas jurídicas (`RJ-01` a `RJ-05`)

Los cinco identificadores son marcadores provisionales. Su contenido sale de E2 y aún no existe ni está aprobado. `design.md` propone un "tema de trabajo" por regla, derivado de la hoja "Puntos de Dolor" del Excel; es una hipótesis para organizar la trazabilidad, no contenido jurídico, y E2 puede reemplazarla. La propuesta distingue cuatro categorías, que se mantienen en los artefactos posteriores:

1. **Obligación legal respaldada por fuente verificada:** ninguna confirmada todavía.
2. **Interpretación pendiente de revisión jurídica.**
3. **Política corporativa propuesta.**
4. **Regla funcional propia de AI DataGuard.**

Fuentes candidatas para E2. Su contenido **no ha sido leído ni validado por el equipo**; se verificó únicamente que existen, sin artículos ni interpretaciones:

- Ley Estatutaria 1581 de 2012 y Ley Estatutaria 1266 de 2008 (protección de datos personales).
- Circular Externa 002 de 2024 de la Superintendencia de Industria y Comercio, sobre tratamiento de datos personales en sistemas de IA.
- Normativa sobre información reservada o secretos empresariales: **fuente por identificar**.

## Decisiones abiertas (no resueltas)

| ID | Descripción original | Implicaciones | Estado |
|---|---|---|---|
| **C1** | Los nombres de archivo del plan no coinciden. Config: `docs/project/project-charter.md`, `docs/legal/legal-matrix.md`, `docs/testing/test-plan.md`. Excel: `ficha-e1.md`, `matriz-reglas.md`, `fuentes.md`, `casos-prueba.md`. Ambos archivos tienen la misma marca de modificación (12 nov 11:58). | Hasta resolverla, los artefactos citan ambas variantes. Afecta enlaces de trazabilidad en tareas y pruebas. | **Abierta** |
| **C3** | Selección del stack tecnológico. La guía exige una aplicación funcional (E5) y E4 dice "entorno inicia", pero la restricción vigente prohíbe elegir stack. | Se registra como **aplazada**. Las especificaciones funcionales no dependen de ella y no se bloquean. No se elige tecnología alguna. | **Aplazada** |
| **C5** | La guía docente define el proyecto como ayudar a "documentar decisiones y hacer seguimiento a compromisos". Las cinco capacidades no mencionan el seguimiento a compromisos. | Se cubre el registro de la decisión humana dentro de `assessment-reports`, pero **no** el seguimiento de compromisos. Falta confirmar con el docente si es obligatorio. No se agrega capacidad. | **Abierta** (consulta docente) |

Observaciones adicionales (no solicitadas expresamente como C):

- **C2:** trazabilidad frente a minimización de datos. Se aborda conceptualmente en `design.md`, queda por validar.
- **C4:** el Excel pide 3 escenarios en la ficha E1 (máx. 2 páginas); la guía solo pide "caso demo" en E1.
- **C6:** `/opsx-propose` genera todos los artefactos juntos; el Excel los escalona por etapa y responsable.
- **O-01 a O-09:** decisiones nuevas detalladas en `design.md` (perfiles, taxonomía de clasificación, formatos de entrada, origen del catálogo de proveedores, escala de resultados, datos persistidos, uso de IA opcional, ubicación de requisitos transversales, alcance de organizaciones).

## Riesgos

- **Cronograma:** E3 y E4 comienzan antes de aprobar E1 y E2, así que un rechazo del alcance puede forzar retrabajo. Mitigación: borrador condicionado y marcadores `RJ`.
- **Alcance frente a plazo:** cinco capacidades en 14 días de construcción (22 nov - 6 dic) con tres integrantes. Pendiente de priorizar funciones obligatorias para E6.
- **Corrección jurídica:** riesgo de citar normas mal. Mitigación: ninguna regla se confirma sin fuente verificada por una persona.
- **Falsos negativos:** la ausencia de alertas no equivale a autorización para divulgar.
- **Datos de ejemplo:** deben ser sintéticos y claramente marcados.
- **Catálogo de proveedores desactualizado:** los términos cambian, así que cada dato lleva fuente y fecha de verificación.

## Dependencias

- Aprobación docente de E1 y E2.
- Investigación y validación de fuentes jurídicas (Integrante 2 según el Excel).
- Asignación de responsables para E5-E8 (hoy "Por asignar").
- Respuesta docente sobre C5 y sobre la ubicación de los 3 escenarios (C4).

## Impact

- **Código:** ninguno. Esta fase no implementa nada.
- **Archivos:** solo `openspec/changes/initial-mvp/`. Los documentos `docs/project/`, `docs/legal/` y `docs/testing/` son entregables de E1, E2 y E6; **no** se crean en este cambio.
- **Documentos del docente:** no se modifican (`docs/academic/`).
- **Sistemas externos:** ninguno. Las condiciones de proveedores se tratan como catálogo con fuente y fecha, no como consulta en línea (propuesta, ver O-04).
