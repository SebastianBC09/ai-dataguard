# Design

> **Estado: BORRADOR CONDICIONADO. Pendiente de aprobación académica.** E1 y E2 no están aprobadas.
> Diseño **conceptual**: no selecciona frameworks, lenguajes, bases de datos ni otras tecnologías (ver C3). Las motivaciones están en `proposal.md`; los requisitos verificables, en `specs/`.
> Sincronizado el 12 nov con las decisiones del equipo D1 a D9 y la auditoría I-01 a I-20. Que `openspec validate --strict` pase indica solo estructura correcta; **no** equivale a aprobación académica ni a calidad jurídica.

## Context

- Fuentes revisadas: `openspec/config.yaml`, `docs/academic/` (guía docente, guías de OpenSpec, plan de trabajo en Excel) y los borradores `docs/project/project-charter.md` (E1), `docs/legal/legal-matrix.md` (E2) y `docs/testing/test-plan.md` (plan de pruebas v0). Ninguno está aprobado.
- El MVP es una aplicación que se usa de principio a fin, guarda información y genera un informe, apoyando la revisión humana (guía docente).
- La evaluación ocurre en un entorno controlado: el contenido evaluado no se envía a terceros.
- Convenciones:

| Marca | Significado |
|---|---|
| **DC-xx** | Decisión conceptual **acordada** (viene de `config.yaml`, de la guía docente o de decisiones del equipo). |
| **DP-xx** | **Propuesta** pendiente de evaluación por el equipo. |
| **DA-xx** | Decisión que **requiere aprobación docente**. |
| **RA-xx** | **Riesgo o alternativa** todavía abierta. |
| **C-x / O-xx** | Observación o decisión abierta (ver "Decisiones abiertas"). |
| **EP-xx** | Requisito de **evolución posterior**, fuera de `specs/`. |

## Goals / Non-Goals

**Goals:**
- Describir actores, flujos, clasificación, evaluación, tratamiento de datos, informes y revisión humana sin imponer tecnología.
- Separar con claridad reglas jurídicas, políticas organizacionales y controles funcionales, y clasificación de sensibilidad y resultado de riesgo.
- Dejar visible qué está acordado y qué no, y mantener la trazabilidad RJ - requisitos - pruebas - escenarios.

**Non-Goals:**
- Elegir tecnologías, arquitectura de despliegue o modelos de IA.
- Definir el contenido jurídico de las reglas `RJ` (corresponde a E2).
- Resolver C3, C4, C5 o C7.
- Agregar capacidades o módulos a las cinco acordadas.

## Modelo conceptual

### Tres tipos de elementos de evaluación

| Tipo | Quién lo define | Qué evalúa | Ejemplos | Resultado |
|---|---|---|---|---|
| **Regla jurídica preliminar** | E2 (provisional) | El contenido, el proveedor o el contexto | `RJ-01` datos personales, `RJ-02` información corporativa reservada, `RJ-03` existencia de políticas aplicables, `RJ-04` condiciones del proveedor | «sin alerta», «advertencia», «requiere revisión humana» o «no evaluada» |
| **Política organizacional** | El Administrador de la organización | Condiciones sobre nivel, categoría o proveedor | «Interna a un proveedor externo requiere revisión» | Resultado recomendado por la política, rotulado «política organizacional» |
| **Control funcional transversal** (`RJ-05`) | El sistema (reglas funcionales) | El propio comportamiento del sistema, **no** el contenido | CT-01 sin transmisión externa, CT-02 descarte del original, CT-03 enmascarado, CT-04 registro sin contenido, CT-05 revisión humana ante ambigüedad | «aplicado» o «no aplicado» |

Notas:
- `RJ-03` evalúa si hay una política aplicable; las políticas en sí no son reglas `RJ`. Que `RJ-03` y `RJ-05` tengan o no fundamento jurídico directo es la consulta **C7**.
- **Terminología (DC-21):** se usa «controles funcionales transversales». Son decisiones del equipo y **no** se presentan como obligaciones legales específicas. La sigla «CT» se mantiene por estabilidad de identificadores.
- **CT-05 (DC-17):** «aplicado» cuando una evaluación con resultado «requiere revisión humana», con clasificación pendiente o con un control «no aplicado» queda «pendiente de revisión» y no emite ninguna recomendación de divulgación. «No aplicado» si no queda pendiente.
- **CT-06** (historial que no se sobrescribe) se mantiene diferenciado: no se registra por evaluación y se verifica en `REP-07`.
- Los controles son una autodeclaración del sistema; su evidencia se corrobora con pruebas independientes (`CP-09`, `CP-10`, `CP-12`). Ver RA-04.

### Clasificación de sensibilidad y resultado de riesgo

| Aspecto | Clasificación de sensibilidad | Resultado de riesgo |
|---|---|---|
| Describe | El contenido | El uso del contenido con un proveedor, políticas y reglas |
| Depende de | Solo del contenido (hallazgos, marcas, resolución humana) | Clasificación, proveedor, políticas, reglas y controles |
| Valores | Pública < Interna < Confidencial < Restringida, o «pendiente de revisión» | «sin alerta» < «advertencia» < «requiere revisión humana» |
| Spec | `information-classification` | `compliance-policies` |

Ejemplos (todos con datos sintéticos, resultados esperados a verificar en E6):

| Contenido | Proveedor | Políticas | Clasificación | Riesgo global | Estado |
|---|---|---|---|---|---|
| Datos personales, certeza alta | «usa el contenido para mejorar modelos = sí» | activas | Confidencial | requiere revisión humana | pendiente de revisión |
| Datos personales, certeza alta | no seleccionado | cualquiera | Confidencial | requiere revisión humana (`RJ-04` «no evaluada») | pendiente de revisión |
| Dato de sensibilidad alta o indicio de menores | informado | cualquiera | Restringida (sensibilidad alta) o al menos Confidencial (menores) | requiere revisión humana (`RJ-01`, advertencia reforzada) | pendiente de revisión |
| Sin hallazgos ni marcas | informado | activas, sin coincidencia | pendiente de revisión (no Pública) | sin alerta | pendiente de revisión (por la clasificación) |
| Sin hallazgos ni marcas | no seleccionado | ninguna | pendiente de revisión | advertencia (`RJ-03` y `RJ-04` «no evaluadas») | pendiente de revisión |
| Marca «uso interno» | no seleccionado | ninguna | Interna | advertencia | completada |
| Marca «reservado» | no seleccionado | ninguna | Restringida | requiere revisión humana (`RJ-02`) | pendiente de revisión |

### Proveedor no seleccionado (comportamiento único)

Lo describen igual `DOC-07`, `POL-05` y `PRV-03`:
1. La detección y la clasificación continúan.
2. Se registra «evaluación de proveedor no completada»; `RJ-04` queda «no evaluada».
3. Se informan los hallazgos. Con hallazgos relevantes, el resultado es «requiere revisión humana» antes de cualquier recomendación de divulgación.
4. Sin hallazgos relevantes, el resultado global es al menos «advertencia», nunca «sin alerta».
5. «Sin proveedor» no equivale a «proveedor seguro»; el texto dice «no evaluado».

El mismo principio aplica a `RJ-03` sin políticas activas (`POL-11`).

### Condiciones del proveedor (DC-15)

Se registran cuatro condiciones, con fuente y fecha. Solo una interviene en el resultado automático:

| Condición | Interviene en el resultado | Cómo se presenta |
|---|---|---|
| Uso del contenido para mejorar modelos (entrenamiento) | Sí, en `RJ-04` (`POL-04`) | Resultado de la regla |
| Retención | No | «información para revisión humana» |
| Posibilidad de exclusión | No | «información para revisión humana» |
| Ubicación del tratamiento | No | «información para revisión humana» |

El sistema **no determina** si una transferencia o transmisión internacional es lícita, ni asigna al proveedor una figura jurídica (encargado, responsable o tercero): eso es interpretación pendiente (`legal-matrix.md`, sección 3.2). El catálogo registra lo que el proveedor declara. El «uso para mejorar modelos» es el único indicio de finalidad que usa la regla.

### Términos con criterio verificable (provisionales)

| Término | Criterio |
|---|---|
| Hallazgo relevante | El de una categoría que corresponde a Confidencial o Restringida, con cualquier certeza. |
| Certeza alta / media / baja | Alta: formato del tipo más etiqueta de contexto. Media: formato sin contexto. Baja: coincidencia parcial o compatible con más de un tipo. |
| Ubicación | Número de línea o de párrafo. |
| Máscara | Máximo los dos últimos caracteres visibles; valores de 4 caracteres o menos, ocultos por completo. |
| Marcas explícitas | Expresiones completas «uso interno», «confidencial», «reservado», «restringido», sin distinguir mayúsculas. «Uso interno» da Interna; «confidencial», Confidencial; «reservado» y «restringido», Restringida. Una palabra aislada como «interno» no es marca. |
| Sensibilidad alta (DC-18) | Los datos sensibles del art. 5 de la Ley 1581: origen racial o étnico, orientación política, convicciones religiosas o filosóficas, pertenencia a sindicatos, organizaciones sociales o de derechos humanos o partidos, salud, vida sexual y biométricos. Es una lista funcional; su equivalencia legal se valida en E2. |
| Indicios de menores (DC-18) | Mención textual explícita de un niño, niña, adolescente o menor de edad. El sistema no verifica la edad ni la autorización. |
| Criterio de «Interna» | Solo la marca «uso interno» sin hallazgos de nivel superior, o asignación humana con justificación. |
| «Pública» | Nunca automática; solo por asignación humana con justificación. |
| Clasificación pendiente | Sin hallazgos ni marcas, análisis parcial, certeza baja o hallazgos en contradicción. |
| Información corporativa | Se detecta solo con marcas explícitas; el informe declara esa limitación. |
| Entorno controlado | El recorrido completo se realiza con las conexiones externas bloqueadas. |
| Revisor | El Administrador en su función de revisión de cumplimiento (DC-14). |
| Volver a someter | «Reevaluar» significa volver a someter el mismo contenido; el original no se conserva (`DOC-08`). |

## Actores y permisos (DC-14)

Para el MVP hay **dos perfiles**: Trabajador y Administrador. La revisión de cumplimiento es una responsabilidad del Administrador, que en esa función se denomina «Revisor». No hay un tercer perfil.

```
 +-------------+        +----------------------------------+
 | Trabajador  |        | Administrador                    |
 +-------------+        +----------------------------------+
 | evalúa      |        | políticas y catálogo             |
 | ve lo propio|        | trazabilidad                     |
 |             |        | función de revisión de           |
 |             |        | cumplimiento ("Revisor"):        |
 |             |        | resuelve casos pendientes y      |
 |             |        | registra la decisión             |
 +-------------+        +----------------------------------+
```

| Acción | Trabajador | Administrador |
|---|---|---|
| Someter contenido a evaluación | Sí | Sí |
| Ver y exportar evaluaciones propias | Sí | Sí |
| Ver y exportar evaluaciones de otros | No | Sí |
| Asignar o ajustar clasificación, registrar decisión (Revisor) | No | Sí |
| Gestionar políticas organizacionales | No | Sí |
| Mantener catálogo de proveedores | No | Sí |

Las altas, bajas y asignación de perfiles quedan fuera de este cambio (O-10). Pendiente de aprobación docente de E1, donde figura esta decisión.

## Flujo conceptual de información

```
 Trabajador
     | 1. contenido + proveedor previsto (opcional)
     v
 +-----------------------------------------------------------------------+
 |        ENTORNO CONTROLADO (conexiones externas bloqueadas)            |
 |                                                                       |
 |  [Ingreso] --> [Análisis: hallazgos] --> [Clasificación de            |
 |                                           sensibilidad]               |
 |                                                  |                    |
 |  [Catálogo] -------------------+                 v                    |
 |  [Reglas RJ-01..04] -----------+--> [Resultado de riesgo]             |
 |  [Políticas de la organiz.] ---+       (por regla, política, control) |
 |  [Controles CT-01..05 (RJ-05)] +                 |                    |
 |                                                  v                    |
 |   descarte del contenido original        [Resultado] -------------------> Administrador
 |                                                  |      (si requiere   | (Revisor)
 |                                                  v       revisión)      | resuelve y
 |                                          [Registro mínimo] <------------+ decide
 |                                                  |                    |  y justifica
 |                                                  v                    |
 |                                              [Informe]                |
 +-----------------------------------------------------------------------+
```

Estados de una evaluación:

```
 En análisis --> Completada      (clasificación asignada, riesgo sin alerta o advertencia,
      |                           controles aplicados)
      |
      +--------> Pendiente de revisión --> Revisada
      |            (riesgo «requiere revisión humana», clasificación
      |             pendiente o control «no aplicado»)
      |             correcciones posteriores = entradas nuevas del historial
      |
      +--------> Cancelada / Fallida (contenido descartado, sin contenido en el registro)
```

## Decisiones

### Decisiones conceptuales acordadas (DC)

| ID | Decisión | Origen |
|---|---|---|
| DC-01 | Exactamente cinco capacidades: `document-analysis`, `information-classification`, `compliance-policies`, `ai-provider-catalog`, `assessment-reports`. | Equipo y `config.yaml` |
| DC-02 | Sin selección de stack y sin implementación en esta fase. | `config.yaml` |
| DC-03 | El contenido evaluado no se transmite a proveedores externos para evaluar su confidencialidad. | `config.yaml` |
| DC-04 | Los resultados son alertas y recomendaciones de precaución, no certificaciones; hay revisión humana y explicabilidad. | `config.yaml`, guía docente |
| DC-05 | Minimización: no se conserva el contenido original cuando no es necesario; registro mínimo de evaluaciones y decisiones. | Equipo |
| DC-06 | Se documentan cinco reglas jurídicas (`RJ-01` a `RJ-05`, provisionales), diez casos de prueba como mínimo y tres escenarios de demostración. | `config.yaml`, guía docente |
| DC-07 | E1 y E2 están pendientes de aprobación docente; este cambio es un borrador condicionado. | `config.yaml` |
| DC-08 | Datos de ejemplo sintéticos, sin pagos, IA opcional. | Guía docente |
| DC-09 | Cuatro niveles: Pública, Interna, Confidencial y Restringida. «Pública» nunca es automática. La falta de información suficiente se registra como clasificación «pendiente de revisión». | Equipo, 12 nov |
| DC-10 | Con proveedor no seleccionado continúan la detección y la clasificación, se registra que la evaluación del proveedor no se completó y, con hallazgos relevantes, se exige revisión humana antes de recomendar divulgar. «Sin proveedor» no es «proveedor seguro». | Equipo, 12 nov |
| DC-11 | `RJ-05` es una regla transversal de controles, no de detección de contenido. Se distinguen reglas jurídicas, políticas organizacionales y controles. `RJ-01` a `RJ-05` siguen provisionales. | Equipo, 12 nov |
| DC-12 | La clasificación de sensibilidad es distinta del resultado de riesgo. | Equipo, 12 nov |
| DC-13 | Los requisitos se clasifican en MVP esencial, complementario o evolución posterior; se fusionan duplicados; se prioriza el flujo de principio a fin. | Equipo, 12 nov |
| DC-14 | **Perfiles (D1):** dos perfiles, Trabajador y Administrador. La revisión de cumplimiento es una responsabilidad del Administrador. Se conservan la revisión humana y sus evidencias. | Equipo, 12 nov (pendiente de aprobación de E1) |
| DC-15 | **Proveedores (D2):** se registran entrenamiento, retención, exclusión y ubicación; solo el uso para mejorar modelos interviene en el resultado; el resto es información para revisión humana. No se determina la licitud de una transferencia o transmisión internacional. | Equipo, 12 nov |
| DC-16 | **Fundamentos (D3):** cada regla tiene una categoría de fundamento principal y, si corresponde, secundarias. Se conservan las interpretaciones pendientes y C7. | Equipo, 12 nov |
| DC-17 | **CT-05 (D4):** definido como en la sección "Modelo conceptual"; sin recomendación de divulgación mientras la revisión necesaria no se resuelva; CT-06 diferenciado. | Equipo, 12 nov |
| DC-18 | **Datos sensibles (D5):** la lista de sensibilidad alta cubre las categorías del art. 5 de la Ley 1581; se consideran indicios de datos de menores; `RJ-01` da «requiere revisión humana» con advertencia reforzada, sin afirmar una prohibición absoluta ni que el sistema verifique autorizaciones. | Equipo, 12 nov |
| DC-19 | **Formatos (D6):** texto directo como entrada esencial; PDF con texto extraíble como funcionalidad complementaria; sin otros formatos. | Equipo, 12 nov |
| DC-20 | **Rutas (D7):** son oficiales `docs/project/project-charter.md`, `docs/legal/legal-matrix.md` y `docs/testing/test-plan.md`; su equivalencia con el Excel está en "Discrepancias con el Excel y la guía". | Equipo, 12 nov |
| DC-21 | **Terminología (D8):** «controles funcionales transversales» para `RJ-05`, sin presentarlos como obligaciones legales específicas. | Equipo, 12 nov |
| DC-22 | **Configuración (D9):** ajustes mínimos en `openspec/config.yaml` para reflejar la terminología y las rutas, sin cambiar capacidades ni estructura. | Equipo, 12 nov |

### Propuestas pendientes de evaluación (DP)

- **DP-01. Resultado cualitativo en tres niveles** más «no evaluada» (O-05). *Alternativa:* puntaje numérico, descartado por sugerir precisión que la fuente jurídica no respalda.
- **DP-02. Catálogo curado con fuente y fecha**, en lugar de consulta en línea (O-04). *Alternativa:* consulta en línea, pospuesta por depender de red y complicar la prueba de no transmisión.
- **DP-03. Conservación mínima**: solo metadatos y conteos (O-06). *Alternativa:* conservar el original cifrado, descartada por DC-05.
- **DP-04. Registro que solo agrega**, para cumplir "qué cambió, quién y cuándo" de la guía.
- **DP-05. Análisis determinista como base, IA solo opcional y dentro del entorno controlado** (O-07). *Alternativa:* servicio externo de IA, descartado por DC-03.
- **DP-07. Conflicto regla/política**: prevalece el más restrictivo y se listan ambos (`POL-06`).
- **DP-08. Requisitos transversales dentro de las cinco specs** (O-08). *Alternativa:* una sexta spec, descartada por DC-01.
- **DP-09. Criterios provisionales** de la tabla "Términos con criterio verificable" (marcas, máscara, certeza, listas de sensibilidad y menores, condiciones del proveedor) (O-02, O-04).
- **DP-10. Orden de entrega** de los requisitos esenciales en fases (ver abajo).

(DP-06, sobre los perfiles, quedó superada por DC-14.)

### Decisiones que requieren aprobación docente (DA)

| ID | Qué se necesita |
|---|---|
| DA-01 | Aprobar E1 y E2. No consta en los documentos una fecha de aprobación. Incluye la decisión de dos perfiles (DC-14). |
| DA-02 | **C5:** confirmar si "documentar decisiones y seguimiento a compromisos" obliga a cubrir el seguimiento de compromisos. |
| DA-03 | **C4:** confirmar si los tres escenarios de demostración van en la ficha E1 o solo en E8. |
| DA-04 | Confirmar el alcance frente al plazo y qué funciones son "obligatorias" para E6 (la clasificación de este documento es propuesta). |
| DA-05 | **C3:** confirmar el criterio y el momento para registrar la decisión del stack. |
| DA-06 | **C7:** consultar si las cinco reglas deben tener fundamento jurídico directo o se admiten reglas funcionales y controles (`RJ-03`, `RJ-05`). |

## Tratamiento de datos

| Dato | ¿Se persiste? | Nota |
|---|---|---|
| Contenido original (texto o archivo) | **No** | Solo existe durante la evaluación (CT-02). Excepción pendiente (O-06). |
| Valores sensibles detectados completos | **No** | Solo fragmentos enmascarados (CT-03, CT-04). |
| Tipos, cantidad y ubicación de hallazgos | Sí | Explicar y auditar. |
| Clasificación, resultado global, resultados por regla, estado de controles | Sí | Trazabilidad. |
| Estado de la evaluación del proveedor | Sí | Incluye «evaluación de proveedor no completada». |
| Usuario y perfil que evalúa | Sí | Es dato personal de trabajadores; usar el mínimo necesario. Revisión pendiente (C2, E2). |
| Proveedor consultado, fuente y fecha | Sí | Contexto de la evaluación. |
| Decisión humana, justificación, autor, fecha | Sí | Revisión humana. |
| Políticas y catálogo con historial | Sí | Configuración de la organización. |
| Exportaciones de informes | Sí (complementario) | Persona y fecha, sin contenido. |

**C2 (trazabilidad frente a minimización):** se resuelve conceptualmente guardando metadatos y no contenido; el periodo de retención queda abierto y pasa a evolución posterior (EP-01).

## Catálogo de requisitos: clase y justificación

Criterios: **MVP esencial** = necesario para el recorrido de principio a fin o exigido por una restricción de `config.yaml` o por la guía docente; **Complementario** = mejora el producto y se puede quitar sin romper el recorrido; **Evolución posterior** = especulativo o dependiente de decisiones abiertas, fuera de `specs/`. Es una **propuesta** pendiente del equipo y del docente (DA-04). En total: **43 requisitos en specs (37 esenciales, 6 complementarios)** y 6 de evolución posterior.

| ID | Requisito | Clase | Justificación |
|---|---|---|---|
| DOC-01 | Identificación y perfil del usuario | Esencial | Permisos (E5) y "quién" para la trazabilidad; dos perfiles; el mecanismo queda fuera. |
| DOC-02 | Ingreso de texto directo | Esencial | Entrada esencial del MVP (DC-19). |
| DOC-03 | Ingreso de documentos PDF con texto extraíble | Complementario | Único formato de documento (DC-19); el texto cubre el recorrido. |
| DOC-04 | Análisis sin transmisión externa (CT-01) | Esencial | Restricción central. Fusiona la consulta del catálogo sin transmisión. |
| DOC-05 | Hallazgos con explicación y certeza | Esencial | Explicabilidad. |
| DOC-06 | Valores enmascarados (CT-03) | Esencial | Minimización. |
| DOC-07 | Análisis independiente del proveedor | Esencial | Mantiene el flujo si falta proveedor. |
| DOC-08 | Descarte del original (CT-02) | Esencial | Minimización. |
| DOC-09 | Análisis parcial | Complementario | Solo cobra sentido con documentos. |
| DOC-10 | Consistencia | Complementario | Propiedad no funcional; fusiona dos requisitos duplicados. |
| CLA-01 | Categorías (sensibilidad ampliada e indicios de menores) | Esencial | Base de la clasificación (DC-18). |
| CLA-02 | Marcas explícitas | Esencial | Único mecanismo verificable de información corporativa. |
| CLA-03 | Niveles y estado | Esencial | Cuatro niveles más estado pendiente (DC-09). |
| CLA-04 | Criterios de asignación | Esencial | Define cuándo aplica cada nivel, incluida «Interna». |
| CLA-05 | Clasificación pendiente (CT-05) | Esencial | Evita Pública automática. |
| CLA-06 | Resolución humana | Esencial | Resuelve lo pendiente; reutiliza el antiguo ajuste de nivel. |
| CLA-07 | Explicación | Esencial | Explicabilidad. |
| CLA-08 | Sensibilidad independiente del riesgo | Esencial | DC-12; verificable por escenarios. |
| POL-01 | Registro de reglas (categoría principal y secundarias) | Esencial | Mínimo académico de cinco reglas. |
| POL-02 | Tipos y categoría del fundamento | Esencial | Diferenciación pedida (DC-11, DC-16). |
| POL-03 | `RJ-01` y `RJ-02` | Esencial | Núcleo de la evaluación de contenido; incluye la advertencia reforzada (DC-18). |
| POL-04 | `RJ-04` condiciones del proveedor | Esencial | Escenarios verificables; solo el uso para mejorar modelos interviene (DC-15). |
| POL-05 | Proveedor no seleccionado | Esencial | DC-10. |
| POL-06 | Resultado global más restrictivo | Esencial | Fusiona el conflicto regla-política. |
| POL-07 | `RJ-05` controles funcionales | Esencial | Evidencia de privacidad; define CT-05 y diferencia CT-06 (DC-17). |
| POL-08 | Explicabilidad de resultados | Esencial | Restricción del proyecto. |
| POL-09 | Sin lenguaje de certificación | Esencial | Restricción explícita. |
| POL-10 | Gestión de políticas | Esencial | Mínimo: crear, activar y desactivar; ED-3. |
| POL-11 | Sin políticas (`RJ-03`) | Esencial | Punto de dolor del plan; costo bajo. |
| PRV-01 | Entradas con fuente, fecha y condiciones | Esencial | Base del catálogo; incluye entradas de ejemplo. |
| PRV-02 | Consulta de condiciones declaradas | Esencial | Evita calificar proveedores. |
| PRV-03 | Proveedor previsto opcional | Esencial | Une catálogo, evaluación y `RJ-04`; muestra las condiciones informativas (DC-15). |
| PRV-04 | Información desactualizada | Complementario | Mitiga un riesgo, no imprescindible. |
| PRV-05 | Mantenimiento por Administrador | Complementario | El catálogo puede precargarse. |
| REP-01 | Informe por evaluación | Esencial | Informe exportado exigido. |
| REP-02 | Aviso de no autorización | Esencial | Fusiona cuatro avisos duplicados. |
| REP-03 | Sin contenido original (CT-04) | Esencial | Minimización. |
| REP-04 | Exportación | Esencial | Guía docente. |
| REP-05 | Registro mínimo | Esencial | Persistencia exigida. |
| REP-06 | Decisión humana (CT-05) | Esencial | Fusiona dos requisitos; documentar decisiones. |
| REP-07 | Historial que no se sobrescribe (CT-06) | Esencial | Historial de cambios de la guía. |
| REP-08 | Consulta de trazabilidad | Esencial | Listado y filtro por estado; ED-3. |
| REP-09 | Registro de exportaciones | Complementario | Auditoría adicional. |

**Evolución posterior (fuera de `specs/`, sin `SHALL`):**

| ID | Tema | Motivo |
|---|---|---|
| EP-01 | Retención configurable del registro | Depende de una decisión jurídica abierta (O-06). |
| EP-02 | Formatos de documento adicionales al PDF | DC-19: no se añaden formatos. |
| EP-03 | Términos reservados definidos por la organización | Ampliaría la detección corporativa más allá de las marcas. |
| EP-04 | Filtros adicionales de trazabilidad (fecha, usuario, nivel) | El filtro por estado basta para el MVP. |
| EP-05 | Gestión de usuarios y perfiles | Fuera de las cinco capacidades (O-10). |
| EP-06 | Seguimiento a compromisos | Solo si el docente lo exige (C5); no se agrega capacidad. |

**Reubicado:** los datos de ejemplo sintéticos dejan de ser requisito del sistema y pasan a restricción del proyecto, cubierta por la tarea 5.5.

### Orden de entrega dentro de los esenciales (DP-10)

Todos son obligatorios; el orden prioriza el flujo de principio a fin.

| Fase | Requisitos | Objetivo |
|---|---|---|
| A. Flujo mínimo | DOC-01, DOC-02, DOC-05, DOC-07, CLA-01 a CLA-05, POL-03 a POL-06, PRV-01 a PRV-03, REP-01, REP-05, REP-06 | Evaluar de principio a fin con informe y decisión. |
| B. Salvaguardas y gobierno | DOC-04, DOC-06, DOC-08, CLA-06 a CLA-08, POL-01, POL-02, POL-07 a POL-11, REP-02 a REP-04, REP-07, REP-08 | Privacidad, minimización, explicabilidad y permisos. |
| C. Complementarios | DOC-03, DOC-09, DOC-10, PRV-04, PRV-05, REP-09 | Solo si el plazo lo permite. |

## Trazabilidad

### Reglas, capacidades, requisitos, pruebas y escenarios

| Regla | Tipo | Capacidades | Requisitos | Pruebas | Escenario |
|---|---|---|---|---|---|
| `RJ-01` | Regla jurídica preliminar | 1, 2, 3 | DOC-05, CLA-01, CLA-04, POL-03 | CP-01, CP-02, CP-12 | ED-1 |
| `RJ-02` | Regla jurídica preliminar | 1, 2, 3 | CLA-02, CLA-04, POL-03, POL-06 | CP-02, CP-03, CP-05 | ED-2, ED-3 |
| `RJ-03` | Evalúa políticas | 3 | POL-06, POL-10, POL-11 | CP-05 (mínimo), CP-04 (adicional) | ED-3 |
| `RJ-04` | Regla jurídica preliminar | 3, 4 | POL-04, POL-05, PRV-02, PRV-03 | CP-01, CP-07, CP-12 (mínimos), CP-06 (adicional) | ED-1, ED-2 |
| `RJ-05` | Controles funcionales | 1, 3, 5 | POL-07, DOC-04, DOC-06, DOC-08, REP-03, REP-07 | CP-02, CP-08, CP-09, CP-10, CP-12 (mínimos), CP-13 (adicional) | ED-1, ED-2, ED-3 |

### Casos de prueba previstos (ninguno ejecutado)

Todos están **previstos, no ejecutados**. La ejecución y las evidencias son de E6. Son 13: **10 mínimos** (los exigidos) y 3 adicionales. Procedimientos, datos y resultados esperados: `docs/testing/test-plan.md`.

| ID | Objetivo | Tipo | Prioridad | Requisitos principales | Capacidades |
|---|---|---|---|---|---|
| CP-01 | Datos personales sintéticos con proveedor que usa el contenido para mejorar modelos: hallazgos, Confidencial, `RJ-01` y `RJ-04`; sensibles y menores con advertencia reforzada | Positivo | Mínimo | DOC-05, CLA-01, CLA-04, POL-03, POL-04, PRV-03 | 1, 2, 3, 4 |
| CP-02 | Contenido sin indicadores: clasificación pendiente (no Pública), aviso y controles visibles | Negativo / falso negativo | Mínimo | DOC-05, CLA-05, POL-07, REP-02 | 1, 2, 3, 5 |
| CP-03 | Marcas de confidencialidad: «reservado» da Restringida y `RJ-02` requiere revisión | Positivo | Mínimo | DOC-05, CLA-02, CLA-04, POL-03 | 1, 2, 3 |
| CP-04 | Evaluación sin políticas: `RJ-03` «no evaluada» y aviso | Límite | Adicional | POL-11 | 3 |
| CP-05 | Política más restrictiva que la regla: prevalece y se listan ambos | Positivo | Mínimo | CLA-08, POL-06, POL-10, REP-07 | 2, 3, 5 |
| CP-06 | Proveedor sin información verificada o desactualizado | Negativo / límite | Adicional | POL-04, PRV-02, PRV-04 | 3, 4 |
| CP-07 | Sin proveedor con datos personales: continúa, `RJ-04` «no evaluada», requiere revisión | Positivo / límite | Mínimo | DOC-07, CLA-08, POL-05, PRV-03, REP-05 | 1, 2, 3, 4, 5 |
| CP-08 | Caso ambiguo (certeza baja): clasificación pendiente, resolución humana y decisión (CT-05) | Límite | Mínimo | DOC-05, CLA-05, CLA-06, REP-06 | 1, 2, 5 |
| CP-09 | Sin transmisión externa: recorrido con conexiones bloqueadas (CT-01) | Privacidad | Mínimo | DOC-04, PRV-03 | 1, 4 |
| CP-10 | Descarte y minimización: sin contenido en el registro tras evaluar; descarte fallido marca CT-02 (CT-02, CT-04) | Privacidad | Mínimo | DOC-08, POL-07, REP-03, REP-05 | 1, 3, 5 |
| CP-11 | Permisos por perfil | Negativo | Mínimo | DOC-01, CLA-06, POL-10, PRV-05, REP-04, REP-06, REP-08 | 1, 2, 3, 4, 5 |
| CP-12 | Informe coherente: campos separados, enmascarado, aviso, controles, condiciones informativas, sin lenguaje de certificación (CT-03) | Positivo | Mínimo | DOC-06, CLA-08, POL-07, POL-09, PRV-02, REP-01, REP-02 | 1, 2, 3, 4, 5 |
| CP-13 | Historial que no se sobrescribe: corrección de decisión (CT-06) | Positivo / negativo | Adicional | REP-07 | 5 |

Las capacidades de cada caso se derivan de los requisitos listados.

### Escenarios de demostración (borrador, pendiente de DA-03)

| ID | Escenario | Capacidades que usa | Perfiles | Pruebas |
|---|---|---|---|---|
| ED-1 | **Privacidad y proveedor.** Un Trabajador evalúa un texto sintético con datos personales y selecciona un proveedor que usa el contenido para mejorar modelos. Se muestran hallazgos enmascarados, Confidencial, `RJ-01` y `RJ-04`, y la retención, la exclusión y la ubicación como información para revisión humana. **Evidencia de privacidad y minimización:** (a) el recorrido se ejecuta con las conexiones externas bloqueadas; (b) el informe muestra CT-01 a CT-05 «aplicado»; (c) la revisión del registro persistido (o de su exportación) muestra que no contiene el texto evaluado ni valores completos. | 1, 2, 3, 4, 5 | Trabajador | CP-01, CP-09, CP-10, CP-12 |
| ED-2 | **Revisión humana y proveedor no seleccionado.** Un Trabajador evalúa un texto sintético que representa un documento, con la marca «reservado», sin elegir proveedor: Restringida, `RJ-02` requiere revisión, `RJ-04` «no evaluada». El Administrador, en su función de Revisor, resuelve el caso con justificación. | 1, 2, 3, 5 y 4 solo en el caso «no seleccionado» | Trabajador, Administrador | CP-03, CP-07, CP-08 |
| ED-3 | **Administración de políticas.** Un Administrador evalúa un texto sintético con la marca «uso interno», sin políticas activas (`RJ-03` «no evaluada»). Crea y activa una política que exige revisión para Interna, vuelve a someter el mismo contenido (prevalece la política), filtra por «pendiente de revisión» y exporta el informe. No selecciona proveedor. | 1, 2, 3, 5 | Administrador | CP-04, CP-05, CP-12 |

Nota: ni los escenarios ni las pruebas están ejecutados, ni el MVP implementado. La guía fija 15 minutos de demostración; los tres escenarios deben ensayarse (tarea 8.1).

### Requisitos sin prueba asociada

| Requisito | Clase | Cómo se verifica |
|---|---|---|
| PRV-01, POL-01 | Esencial | Verificaciones documentales `VD-01` y `VD-02` del plan de pruebas (tarea 6.2). |
| DOC-02 (escenarios de borde) | Esencial | `VD-03`, cuando se defina el límite de tamaño (O-03). |
| DOC-03, DOC-09, DOC-10, REP-09 | Complementario | Se prevén pruebas solo si se implementan. |

### Etapas académicas

| Etapa | Artefacto relacionado |
|---|---|
| E1 | Ficha de proyecto: `docs/project/project-charter.md`. Pendiente de aprobación. |
| E2 | Matriz de 5 reglas y fuentes: `docs/legal/legal-matrix.md`. Pendiente de aprobación. |
| E3 | `proposal.md`, `specs/`, `design.md` y plan de pruebas v0 (`docs/testing/test-plan.md`). |
| E4 | `tasks.md`, hito C3 y plan de pruebas v1. |
| E5-E8 | Futuros; ver `tasks.md`. |

## Discrepancias con el Excel y la guía

El Excel y los documentos del docente **no se modifican**. Las discrepancias se documentan aquí y en `tasks.md`.

**Equivalencia de rutas (DC-20):**

| Ruta oficial (equipo y `config.yaml`) | En el Excel | Observación |
|---|---|---|
| `docs/project/project-charter.md` | `docs/project/ficha-e1.md` | Ficha de E1 |
| `docs/legal/legal-matrix.md` | `docs/legal/matriz-reglas.md` | Matriz de E2 |
| Sección 2 de `legal-matrix.md` | `docs/legal/fuentes.md` | Las fuentes se incluyen en la matriz; no hay archivo separado |
| `docs/testing/test-plan.md` | `docs/testing/casos-prueba.md` | Plan v0 y v1 en E3 y E4; ejecución en E6 |
| (sin ruta oficial) | `docs/user-guide/` | Por definir en E7; no figura en `config.yaml` |

| # | Discrepancia | Tratamiento |
|---|---|---|
| 1 | Nombres de archivo distintos entre `config.yaml` y el Excel (C1). | **Resuelta por el equipo (DC-20):** rutas oficiales de `config.yaml`; equivalencia arriba; informar al docente. |
| 2 | El Excel pide 3 escenarios en la ficha E1; la guía solo pide "caso demo" (C4). | Abierta (DA-03). |
| 3 | La tarea 4.1 del Excel (12-15 nov) termina antes que 3.2 (hasta el 17) y 3.3 (hasta el 21), de las que depende. | `tasks.md` divide: 4.1 es el borrador v0 y 4.3 la revisión final. |
| 4 | El Excel (6.1) "diseña y ejecuta" los casos en E6; la guía incluye "criterios de prueba" en E3. | El plan de pruebas se redacta en E3 (v0) y E4 (v1); E6 solo ejecuta. |
| 5 | E3 y E4 empiezan el 12 nov, antes de aprobar E1 y E2; la guía las define como puertas de cierre. | Borrador condicionado. |
| 6 | Títulos de etapa distintos entre Excel y guía. | Informativa. |
| 7 | La guía dice "entorno inicia" en E4; el Excel no tiene ninguna tarea para ello ni para la decisión del stack. | Tarea 4.4 (hito C3). |
| 8 | El Excel no desglosa E5 por capacidad. | `tasks.md` añade ítems adicionales sin cambiar el alcance. |
| 9 | Siete puntos de dolor frente a cinco reglas. | Tarea 2.4. |
| 10 | Fechas en fin de semana (22 nov, 13 dic, 19 dic). | Por confirmar con el equipo. |
| 11 | En el Excel, 4.2 (12 nov) termina antes que 4.1 (hasta el 15 nov), y 2.2 y 5.2 empiezan antes de que terminen 2.1 y 5.1. | `tasks.md` lo anota como inicio parcial; no se modifica el Excel. |

## Estado de la auditoría de sincronización (I-01 a I-20)

"Resuelto en artefactos" significa que el texto se corrigió; **no** significa aprobado ni verificado por el equipo o el docente.

| ID | Estado |
|---|---|
| I-01 Perfiles | Resuelto en artefactos (DC-14); pendiente de aprobación de E1 |
| I-02 Condiciones del proveedor | Resuelto en artefactos (DC-15); aplicación jurídica pendiente (C7, E2) |
| I-03 Categorías de fundamento | Resuelto en artefactos (DC-16); C7 abierta |
| I-04 CT-05 y CT-06 | Resuelto en artefactos (DC-17) |
| I-05 Datos sensibles y menores | Resuelto en artefactos (DC-18); equivalencia legal pendiente de E2 |
| I-06 Formatos y «documento» | Resuelto en artefactos (DC-19); límite de tamaño pendiente (O-03) |
| I-07 «Reevaluar» | Resuelto en artefactos |
| I-08 Evidencia del registro | Resuelto en artefactos; método pendiente de C3 |
| I-09 Escenarios sin pasos en el plan | Resuelto en el plan de pruebas |
| I-10 a I-12 Capacidades, reglas y terminología | Resueltos en artefactos |
| I-13 Textos desfasados | Resuelto en artefactos |
| I-14 Rutas (C1) | Resuelto por el equipo (DC-20) |
| I-15, I-16 Dependencias y referencias de tareas | Resueltos en `tasks.md` |
| I-17 Días de construcción | Resuelto (14) |
| I-18 `config.yaml` | Resuelto con ajustes mínimos (DC-22) |
| I-19 Versionado | Pendiente: sin commit, por indicación del equipo |
| I-20 Extensión de la ficha E1 | Pendiente de medir en el formato final |

## Decisiones abiertas

| ID | Tema | Estado | Detalle |
|---|---|---|---|
| C1 | Nombres de archivo de `docs/` | **Resuelta por el equipo** | DC-20. Informar al docente. |
| C2 | Trazabilidad frente a minimización | Abierta (parcial) | Resuelta conceptualmente; falta la revisión de E2. |
| **C3** | Selección del stack tecnológico | **Aplazada** | No se selecciona. Las specs no dependen de ella. Hito: registrar la decisión en la tarea 4.4, a más tardar al cierre de E4 (21 nov según el Excel) y antes de iniciar E5 (22 nov). La fecha de aprobación docente **no está definida**; si se retrasa, E5 no inicia. |
| **C4** | Ubicación de los tres escenarios (E1 frente a E8) | **Abierta** | DA-03. |
| **C5** | Seguimiento a compromisos | **Abierta** (consulta docente) | Se cubre el registro de decisiones; el seguimiento no está especificado (EP-06). |
| C6 | Propose genera todos los artefactos juntos; el Excel los escalona | Abierta | Borrador por responsable y etapa. |
| **C7** | ¿Las cinco reglas deben tener fundamento jurídico directo? | **Abierta** (consulta docente) | Afecta sobre todo a `RJ-03` y `RJ-05` (DA-06). |
| O-01 | Perfiles | **Decidida por el equipo** (DC-14) | Pendiente de aprobación docente de E1. |
| O-02 | Taxonomía de clasificación | Parcial | Niveles acordados (DC-09); lista de sensibilidad ampliada (DC-18); marcas y criterios siguen siendo propuesta (DP-09). |
| O-03 | Formatos de entrada y límite de tamaño | Parcial | Formatos decididos (DC-19); límite de tamaño pendiente. |
| O-04 | Origen del catálogo y conjunto de condiciones | Parcial | Condiciones decididas (DC-15); origen del catálogo abierto (DP-02). |
| O-05 | Escala de resultados | Abierta | DP-01. |
| O-06 | Datos persistidos, retención y excepción de conservación del original | Abierta | Retención pasa a EP-01. |
| O-07 | IA opcional dentro del entorno controlado | Abierta | DP-05. |
| O-08 | Ubicación de requisitos transversales | Parcial | `RJ-05` se especifica en `POL-07`; el reparto de permisos queda como en la sección de actores. |
| O-09 | Una organización por instancia (supuesto) | Abierta | Pymes. |
| O-10 | Gestión de usuarios y perfiles (altas, bajas, asignación) | **Abierta** | Fuera de las cinco capacidades (EP-05). |

## Risks / Trade-offs

- **Reglas provisionales leídas como obligaciones** → toda regla sin fuente verificada se muestra «provisional» y «pendiente de fuente»; las categorías secundarias no se presentan como obligación.
- **Falsos negativos** (RA-01) → clasificación pendiente en lugar de Pública, aviso obligatorio y declaración de que la detección corporativa se limita a marcas.
- **Carga de revisión humana** (RA-03): toda clasificación pendiente exige al Administrador, incluso contenido sin indicadores, y ahora también los datos sensibles y de menores. → medir en E6; si es excesivo, replantear con el docente.
- **Autodeclaración de controles** (RA-04): CT-01 a CT-05 los reporta el propio sistema. → se corroboran con pruebas independientes (`CP-09`, `CP-10`, `CP-12`).
- **Alcance frente al plazo** (RA-02): 43 requisitos para 14 días de construcción con tres integrantes. → fases A, B y C, y priorización (tarea 4.5).
- **Cronograma que adelanta E3 y E4 a E1 y E2** → borrador condicionado; posible retrabajo.
- **Catálogo desactualizado** → fuente, fecha y marca de antigüedad (PRV-04, complementario).
- **Datos de ejemplo parecidos a datos reales** → marcar y revisar el conjunto sintético (tarea 5.5).
- **Datos de trabajadores en el registro** → mínimo necesario y revisión con E2.
- **Trade-off:** resultados cualitativos son menos precisos pero más explicables que un puntaje (DP-01).

## Open Questions

Pueden responderse después sin cambiar las specs ni el desglose de tareas:

- Valor del límite de tamaño de entrada (O-03).
- Periodo de vigencia de entradas del catálogo.
- Redacción final de las advertencias, incluida la advertencia reforzada, y de los mensajes de rechazo.
