# Design

> **Estado: BORRADOR CONDICIONADO. Pendiente de aprobación académica.** E1 y E2 no están aprobadas.
> Diseño **conceptual**: no selecciona frameworks, lenguajes, bases de datos ni otras tecnologías (ver C3). Las motivaciones están en `proposal.md`; los requisitos verificables, en `specs/`.

## Context

- Fuentes revisadas: `openspec/config.yaml`, `docs/academic/` (guía docente, guías de OpenSpec, plan de trabajo en Excel). `docs/project/` y `docs/legal/` están vacíos y `docs/testing/` no existe; no hay contenido de E1 ni E2 del que partir.
- El MVP es una aplicación que se usa de principio a fin, guarda información y genera un informe, apoyando la revisión humana (guía docente).
- La evaluación ocurre en un entorno controlado: el contenido evaluado no se envía a terceros para decidir si es seguro.
- Convenciones usadas en este documento:

| Marca | Significado |
|---|---|
| **DC-xx** | Decisión conceptual **acordada** (viene de `config.yaml`, de la guía docente o de tus instrucciones). |
| **DP-xx** | **Propuesta** pendiente de evaluación por el equipo. |
| **DA-xx** | Decisión que **requiere aprobación docente**. |
| **RA-xx** | **Riesgo o alternativa** todavía abierta. |
| **C-x / O-xx** | Observación o decisión abierta (ver "Decisiones abiertas"). |

## Goals / Non-Goals

**Goals:**
- Describir actores, flujos, clasificación, evaluación de políticas, tratamiento de datos, informes y revisión humana de forma independiente de la tecnología.
- Dejar visible qué está acordado y qué no, de modo que el docente pueda revisarlo.
- Preparar la trazabilidad RJ - requisitos - casos de prueba - escenarios de demostración.

**Non-Goals:**
- Elegir tecnologías, arquitectura de despliegue o modelos de IA concretos.
- Definir el contenido jurídico de las reglas `RJ` (corresponde a E2).
- Resolver C1, C3 y C5 (se registran como abiertas o aplazadas).
- Agregar capacidades o módulos a las cinco acordadas.

## Actores

```
 +-------------+     +----------------+     +-----------------------------+
 | Trabajador  |     | Administrador  |     | Responsable de cumplimiento |
 +-------------+     +----------------+     +-----------------------------+
 | evalúa      |     | políticas      |     | revisa casos ambiguos       |
 | contenido   |     | catálogo       |     | registra decisión           |
 | ve lo propio|     | trazabilidad   |     | consulta trazabilidad       |
 +-------------+     +----------------+     +-----------------------------+
                  \         |         /
                   "Revisor" = Administrador o Responsable de cumplimiento
                   (DP, pendiente O-01: ¿son perfiles distintos?)
```

Matriz de permisos (propuesta DP-06; las celdas "por decidir" dependen de O-01):

| Acción | Trabajador | Administrador | Resp. cumplimiento |
|---|---|---|---|
| Someter contenido a evaluación | Sí | Sí | Sí |
| Ver y exportar evaluaciones propias | Sí | Sí | Sí |
| Ver evaluaciones de otros (metadatos) | No | Sí | Sí |
| Registrar decisión de revisión | No | Sí | Sí |
| Ajustar nivel de clasificación | No | Sí | Sí |
| Gestionar políticas organizacionales | No | Sí | por decidir |
| Gestionar catálogo de proveedores | No | Sí | por decidir |

## Flujo conceptual de información

```
 Trabajador
     | 1. contenido + proveedor previsto (opcional)
     v
 +--------------------------------------------------------------+
 |        ENTORNO CONTROLADO (el contenido no sale de aquí)     |
 |                                                              |
 |  [Ingreso] --> [Análisis] --> [Clasificación]                |
 |                                      |                       |
 |  [Catálogo de proveedores] ----+     v                       |
 |  [Reglas RJ-01..05] -----------+--> [Evaluación de reglas    |
 |  [Políticas de la organiz.] ---+      y políticas]           |
 |                                      |                       |
 |                                      v                       |
 |                                 [Resultado] ---------------------> Revisor
 |                                      |         (si requiere       | decide
 |   descarte del contenido original    |          revisión)         | + justifica
 |                                      v                            |
 |                               [Registro mínimo] <-----------------+
 |                                      |                       |
 |                                      v                       |
 |                                  [Informe]                   |
 +--------------------------------------------------------------+
```

Estados de una evaluación (propuesta):

```
 En análisis --> Completada ------------------------------> (cierre)
      |            (global: sin alerta o advertencia)
      |
      +--------> Pendiente de revisión --> Revisada --> (cierre)
      |            (global: requiere revisión)  ^
      |                                         | corrección = entrada nueva
      +--------> Fallida / Cancelada (contenido descartado, sin informe de contenido)
```

## Decisiones

### Decisiones conceptuales acordadas (DC)

| ID | Decisión | Origen |
|---|---|---|
| DC-01 | Exactamente cinco capacidades: `document-analysis`, `information-classification`, `compliance-policies`, `ai-provider-catalog`, `assessment-reports`. | Instrucción del equipo y `config.yaml` |
| DC-02 | Sin selección de stack y sin implementación en esta fase. | `config.yaml` |
| DC-03 | El contenido evaluado no se transmite a proveedores externos para evaluar su confidencialidad. | `config.yaml` |
| DC-04 | Los resultados son alertas y recomendaciones, no certificaciones; hay revisión humana y explicabilidad. | `config.yaml`, guía docente |
| DC-05 | Minimización: no se conserva el contenido original cuando no es necesario; registro mínimo de evaluaciones y decisiones. | Instrucciones del equipo |
| DC-06 | Se documentan cinco reglas jurídicas (`RJ-01` a `RJ-05`, provisionales), diez casos de prueba y tres escenarios de demostración. | `config.yaml`, guía docente |
| DC-07 | E1 y E2 están pendientes de aprobación docente; este cambio es un borrador condicionado. | `config.yaml` |
| DC-08 | Datos de ejemplo sintéticos; sin pagos; la IA es opcional. | Guía docente |

### Propuestas pendientes de evaluación (DP)

**DP-01. Resultado cualitativo en tres niveles** ("sin alerta", "advertencia", "requiere revisión humana") con un resultado global más restrictivo (O-05).
- *Por qué:* es explicable y evita lenguaje de certificación.
- *Alternativa:* puntaje numérico. Se descarta por ahora porque sugiere una precisión que la fuente jurídica no respalda.

**DP-02. Catálogo de proveedores curado, con fuente y fecha**, en lugar de consulta en línea (O-04).
- *Por qué:* no requiere conexión, no tiene costo y permite citar la fuente.
- *Alternativa:* consulta en línea de los términos. Se pospone: depende de red, los términos cambian y complica la prueba de no transmisión.
- *Riesgo:* información desactualizada; se mitiga con la marca de antigüedad.

**DP-03. Conservación mínima.** El contenido existe solo durante la evaluación; se persisten metadatos y conteos, nunca valores sensibles (O-06).
- *Alternativa:* conservar el original cifrado para auditoría. Se descarta por contradecir DC-05.

**DP-04. Registro que solo agrega.** Decisiones, ajustes y cambios de políticas se corrigen con entradas nuevas.
- *Por qué:* cumple el "historial de cambios: qué, quién, cuándo" de la guía docente.

**DP-05. Análisis determinista como base, con IA solo opcional y dentro del entorno controlado** (O-07).
- *Alternativas:* un servicio externo de IA (se descarta por DC-03); un componente local de IA (queda abierto, sin elegir tecnología).

**DP-06. Perfiles y "Revisor"** (O-01). Matriz de permisos de arriba.

**DP-07. Conflicto entre regla y política:** prevalece el resultado más restrictivo y se listan ambos.

**DP-08. Requisitos transversales dentro de las cinco specs** (O-08): permisos en cada capacidad donde aplican, privacidad y minimización en `document-analysis` y `assessment-reports`, revisión humana en `information-classification`, `compliance-policies` y `assessment-reports`.
- *Alternativa:* una sexta spec transversal. Se descarta por DC-01.

### Decisiones que requieren aprobación docente (DA)

| ID | Qué se necesita |
|---|---|
| DA-01 | Aprobar E1 (selección y delimitación) y E2 (análisis jurídico y reglas). |
| DA-02 | **C5:** confirmar si "documentar decisiones y seguimiento a compromisos" obliga a cubrir el seguimiento de compromisos. |
| DA-03 | **C4:** confirmar si los tres escenarios de demostración deben ir en la ficha E1 (máx. 2 páginas) o solo en E8. |
| DA-04 | Confirmar el alcance frente al plazo de construcción y qué funciones son "obligatorias" para E6. |
| DA-05 | **C3:** confirmar el momento y el criterio para registrar la decisión del stack. |

## Tratamiento de datos

| Dato | ¿Se persiste? | Nota |
|---|---|---|
| Contenido original (texto o archivo) | **No** | Solo existe durante la evaluación; se descarta al finalizar, cancelar o fallar. Excepción pendiente (O-06). |
| Valores sensibles detectados completos | **No** | Solo fragmentos enmascarados en pantalla e informe. |
| Tipos, cantidad y ubicación aproximada de hallazgos | Sí | Necesarios para explicar y auditar. |
| Nivel, resultado global, reglas y versiones | Sí | Trazabilidad. |
| Usuario y perfil que evalúa | Sí | Es dato personal de trabajadores; usar el mínimo necesario. Revisión pendiente (C2, `RJ-05`). |
| Proveedor consultado, fuente y fecha | Sí | Contexto de la evaluación. |
| Decisión humana, justificación, autor, fecha | Sí | Revisión humana. |
| Políticas y catálogo (con historial) | Sí | Configuración de la organización. |
| Exportaciones de informes | Sí (evento) | Persona y fecha, sin contenido. |

**C2 (tensión trazabilidad - minimización):** el registro es necesario para la trazabilidad, pero cada dato persistido debe justificarse. Se resuelve conceptualmente guardando metadatos y no contenido; el periodo de retención queda abierto (O-06).

## Clasificación

- Categorías funcionales provisionales: datos personales de identificación y contacto, datos personales financieros, indicadores de sensibilidad alta, información corporativa confidencial, credenciales o secretos técnicos. **No** equivalen todavía a categorías legales; esa equivalencia es una tarea de E2.
- Niveles provisionales (O-02): "Sin indicadores detectados" < "Interno" < "Confidencial" < "Restringido". El nivel de una evaluación es el más alto entre sus hallazgos.
- Certeza baja o conflicto: se mantiene el nivel como si el hallazgo fuese cierto y se exige revisión humana.
- "Sin indicadores detectados" no significa información pública ni autorización para divulgar.

## Evaluación de reglas y políticas

- Entradas de la evaluación: nivel, hallazgos, proveedor previsto y sus condiciones, reglas `RJ` activas y políticas activas.
- Resultado por regla o política: "sin alerta", "advertencia" o "requiere revisión humana". Resultado global: el más restrictivo.
- Cuando falta información para decidir, el resultado es "requiere revisión humana", no "sin alerta".
- Sin políticas activas: se evalúa solo con las reglas `RJ` y se avisa; no se interpreta como permiso.
- Categorías del fundamento de cada regla: obligación legal respaldada por fuente verificada / interpretación pendiente de revisión jurídica / política corporativa propuesta / regla funcional de AI DataGuard.

### Reglas jurídicas provisionales

Los identificadores son marcadores. La columna "tema de trabajo" es una **hipótesis** derivada de la hoja "Puntos de Dolor" del Excel, **no contenido jurídico**; E2 puede reemplazarla. No se cita ninguna ley ni artículo como fundamento.

| ID | Tema de trabajo (hipótesis) | Categoría de fundamento | Fuente | Estado |
|---|---|---|---|---|
| RJ-01 | Datos personales enviados a herramientas de IA externas | por definir en E2 | pendiente | Provisional |
| RJ-02 | Información corporativa reservada o confidencial | por definir en E2 | pendiente | Provisional |
| RJ-03 | Políticas y reglas internas de la organización | por definir en E2 | pendiente | Provisional |
| RJ-04 | Condiciones de tratamiento de los proveedores de IA | por definir en E2 | pendiente | Provisional |
| RJ-05 | Minimización, retención, trazabilidad y revisión humana | por definir en E2 | pendiente | Provisional |

Observaciones: el Excel enumera siete puntos de dolor y solo hay cinco reglas, así que "clasificación incorrecta o falsos negativos" se trata como limitación funcional (categoría "regla funcional") y no como regla jurídica, salvo que E2 decida otra cosa (RA-01). Fuentes candidatas, sin leer ni validar, en `proposal.md`.

## Revisión humana

- Cuando el resultado global es "requiere revisión humana", la evaluación queda "pendiente de revisión" hasta que un Revisor registre decisión ("proceder", "proceder con ajustes" o "no proceder") con justificación.
- Un Revisor puede ajustar el nivel con justificación, conservando el original.
- Las correcciones se agregan como entradas nuevas.
- El sistema recomienda; la persona decide. La decisión humana no se presenta como certificación.

## Informes

- Un informe por evaluación: identificación, nivel, hallazgos explicados y enmascarados, resultados por regla y política con su estado de validación, proveedor con fuente y fecha, versiones aplicadas, recomendaciones y decisión humana.
- Siempre con la advertencia de apoyo a la revisión humana y de que la ausencia de alertas no autoriza divulgar.
- Exportable a un formato legible fuera de la aplicación; cada exportación queda registrada.

## Trazabilidad

### Casos de prueba previstos (ninguno ejecutado)

Estado de todos: **previsto, no ejecutado**. Su ejecución es de E6 y los resultados, incluidos los esperados, se detallarán en el plan de pruebas (nombre de archivo pendiente por C1). Mínimo exigido: 10.

| ID | Objetivo | Tipo | Capacidades | RJ |
|---|---|---|---|---|
| CP-01 | Detección de datos personales sintéticos, clasificación y advertencia | Positivo | 1, 2, 3 | RJ-01 |
| CP-02 | Texto sin indicadores: "sin indicadores detectados" con advertencia de no autorización | Negativo / falso negativo | 1, 2, 3, 5 | - |
| CP-03 | Información corporativa reservada: nivel "Confidencial" o superior y revisión humana | Positivo | 1, 2, 3 | RJ-02 |
| CP-04 | Evaluación en una organización sin políticas configuradas | Límite | 3 | RJ-03 |
| CP-05 | Conflicto entre regla y política: prevalece el resultado más restrictivo | Positivo | 3 | RJ-03 |
| CP-06 | Proveedor con información vencida o sin información verificada | Negativo / límite | 4, 3 | RJ-04 |
| CP-07 | Caso ambiguo: certeza baja o análisis parcial exige decisión humana justificada | Límite | 1, 2, 5 | RJ-05 |
| CP-08 | Sin transmisión externa y sin retención del original | Privacidad | 1, 4, 5 | RJ-05 |
| CP-09 | Permisos por perfil | Negativo | 2, 3, 4, 5 | - |
| CP-10 | Informe coherente, enmascarado, con advertencia y con historial que no se sobrescribe | Positivo | 5 | RJ-05 |

Cobertura prevista: las cinco capacidades y las cinco reglas aparecen al menos una vez. Algunos escenarios de las specs (por ejemplo, entrada vacía o formato no soportado) no están mapeados a un CP y podrán añadirse como pruebas adicionales en E6.

### Escenarios de demostración (borrador, pendiente de DA-03)

| ID | Escenario | Capacidades | Perfiles | Pruebas relacionadas |
|---|---|---|---|---|
| ED-1 | Un Trabajador evalúa un texto sintético con datos personales y quiere usar un proveedor externo; recibe advertencia y explicación | 1, 2, 3, 4, 5 | Trabajador | CP-01, CP-06 |
| ED-2 | Un Trabajador evalúa un documento sintético con información corporativa reservada y queda pendiente de revisión; un Revisor decide con justificación | 1, 2, 3, 5 | Trabajador, Revisor | CP-03, CP-07 |
| ED-3 | Un Administrador configura una política, consulta la trazabilidad y exporta un informe | 3, 4, 5 | Administrador | CP-05, CP-09, CP-10 |

Nota: ninguno de los escenarios o pruebas está ejecutado ni el MVP implementado.

### Etapas académicas

| Etapa | Artefacto relacionado |
|---|---|
| E1 | Ficha de proyecto (ruta pendiente, C1). Pendiente de aprobación. |
| E2 | Matriz de 5 reglas y fuentes. Pendiente de aprobación. |
| E3 | `proposal.md`, `specs/`, `design.md` de este cambio. |
| E4 | `tasks.md` de este cambio y el Excel. |
| E5-E8 | Futuros; ver `tasks.md`. |

## Decisiones abiertas

| ID | Tema | Estado | Detalle |
|---|---|---|---|
| **C1** | Nombres de archivo de `docs/` (config frente a Excel) | **Abierta** | Config: `project-charter.md`, `legal-matrix.md`, `test-plan.md`. Excel: `ficha-e1.md`, `matriz-reglas.md`, `fuentes.md`, `casos-prueba.md`. No se elige ninguno; los artefactos citan ambos. |
| **C3** | Selección del stack tecnológico | **Aplazada** | No se selecciona ninguna tecnología. Las specs son independientes de la implementación y no se bloquean. Propuesta (DA-05): registrar la decisión en E4, antes de comenzar E5, con criterios derivados de la guía docente (web, computador o celular; sin pagos; IA opcional; entorno controlado; persistencia; informe exportable). |
| **C5** | "Seguimiento a compromisos" | **Abierta** (consulta docente) | La guía define el proyecto como ayudar a "documentar decisiones y hacer seguimiento a compromisos". Se cubre el registro de decisiones en `assessment-reports`; el seguimiento de compromisos **no** está especificado y no se agrega capacidad. |
| C2 | Trazabilidad frente a minimización | Abierta | Ver "Tratamiento de datos". |
| C4 | Ubicación de los tres escenarios (E1 frente a E8) | Abierta (DA-03) | Excel pide 3 escenarios en E1; la guía solo pide "caso demo". |
| C6 | Propose genera todos los artefactos juntos; el Excel los escalona | Abierta | Tratado como borrador por responsable y etapa. |
| O-01 | Perfiles: ¿Administrador y Responsable de cumplimiento son distintos? ¿Quién es "Revisor"? | Abierta | DP-06. |
| O-02 | Taxonomía de clasificación | Abierta | Niveles provisionales. |
| O-03 | Formatos de entrada y límite de tamaño | Abierta | Mínimo: texto directo. |
| O-04 | Origen y contenido del catálogo de proveedores; reales o ficticios | Abierta | DP-02. |
| O-05 | Escala de resultados | Abierta | DP-01. |
| O-06 | Datos persistidos, retención y excepción de conservación del original | Abierta | DP-03. |
| O-07 | Uso de IA opcional dentro del entorno controlado | Abierta | DP-05. |
| O-08 | Ubicación de los requisitos transversales | Abierta | DP-08. |
| O-09 | Alcance de organizaciones: una por instancia (supuesto) | Abierta | Pymes. |

## Risks / Trade-offs

- **Reglas provisionales leídas como obligaciones** → toda regla sin fuente verificada se muestra "provisional" y "pendiente de fuente" (`compliance-policies`).
- **Falsos negativos** (RA-01) → advertencia obligatoria, certeza baja exige revisión, "sin indicadores detectados" no significa seguro.
- **Cronograma que adelanta E3 y E4 a E1 y E2** → borrador condicionado; posible retrabajo si el docente cambia el alcance.
- **Alcance frente al plazo** (RA-02): cinco capacidades en 14 días de construcción con tres integrantes. → pedir priorización (DA-04).
- **Catálogo desactualizado** → fuente, fecha y marca de antigüedad.
- **Datos de ejemplo parecidos a datos reales** → marcar y revisar el conjunto sintético.
- **Datos de trabajadores en el registro** → identificar lo mínimo necesario y revisar con E2.
- **Trade-off:** resultados cualitativos son menos precisos pero más explicables que un puntaje (DP-01).

## Open Questions

Pueden responderse después sin cambiar las specs ni el desglose de tareas:

- Valor del límite de tamaño de entrada (O-03).
- Periodo de vigencia de entradas del catálogo.
- Periodo de retención del registro (O-06).
- Redacción final de las advertencias y de los mensajes de rechazo.
