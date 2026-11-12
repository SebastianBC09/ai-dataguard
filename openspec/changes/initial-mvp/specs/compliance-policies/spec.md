# Spec Delta

## Purpose

Evalúa cada evaluación frente a tres tipos de elementos claramente distintos: reglas jurídicas preliminares (`RJ-01` a `RJ-04`), políticas organizacionales definidas por el Administrador y controles funcionales transversales (`RJ-05`), que son decisiones del equipo y no se presentan como obligaciones legales específicas. Entrega un resultado de riesgo explicable que requiere revisión humana. Los identificadores `RJ` son **provisionales** hasta que E2 los investigue, valide y apruebe; no son obligaciones jurídicas confirmadas ni certificaciones. Si cada una de las cinco reglas debe tener fundamento jurídico directo es una consulta docente abierta (C7).

## ADDED Requirements

### Requirement: POL-01 Registro de reglas preliminares
[MVP esencial] El sistema SHALL mantener las reglas `RJ-01` a `RJ-05` con identificador, tipo (regla jurídica preliminar o controles funcionales transversales), condición, resultado, fundamento, categoría principal y secundarias, y estado de validación. Una regla sin fuente verificada SHALL figurar como «pendiente de fuente». Hay al menos cinco reglas.

#### Scenario: Regla con fuente verificada
- **WHEN** E2 aprueba una regla con fuente verificada
- **THEN** su estado cambia a «validada» y el fundamento cita la fuente

#### Scenario: Regla sin fuente verificada
- **WHEN** una regla no tiene fuente verificada
- **THEN** el sistema la muestra como «pendiente de fuente» y provisional, no como obligación

#### Scenario: Fundamento mixto
- **WHEN** una regla tiene más de una categoría de fundamento
- **THEN** el sistema muestra una categoría principal y las secundarias, y ninguna interpretación pendiente se presenta como obligación confirmada

#### Scenario: Consulta del registro
- **WHEN** se consulta el registro de reglas
- **THEN** aparecen al menos los identificadores `RJ-01` a `RJ-05`, y `RJ-05` figura con el tipo «controles funcionales transversales»

### Requirement: POL-02 Distinción de tipos y categoría del fundamento
[MVP esencial] El sistema SHALL rotular cada resultado como regla jurídica preliminar (`RJ-01` a `RJ-04`), política organizacional o control funcional transversal (`RJ-05`), y SHALL asignar a cada regla una categoría de fundamento principal y, si corresponde, secundarias: obligación legal con fuente verificada, interpretación pendiente de revisión, política corporativa propuesta o regla funcional.

#### Scenario: Resultado de una política
- **WHEN** una política organizacional produce un resultado
- **THEN** el resultado se rotula «política organizacional» y no se atribuye a ninguna `RJ` (CP-05)

#### Scenario: Resultado de un control funcional
- **WHEN** se muestra el estado de un control de `RJ-05`
- **THEN** se rotula «control funcional transversal» y no como detección sobre el contenido (CP-12)

#### Scenario: Regla sin categoría
- **WHEN** una regla no tiene categoría principal de fundamento asignada
- **THEN** el sistema impide activarla en las evaluaciones

### Requirement: POL-03 Evaluación de RJ-01 y RJ-02
[MVP esencial] El sistema SHALL evaluar `RJ-01` y `RJ-02` con los hallazgos y las marcas: `RJ-01` devuelve «requiere revisión humana» ante indicadores de sensibilidad alta o de menores, «advertencia» ante otros datos personales y «sin alerta» sin ellos; `RJ-02` devuelve «requiere revisión humana» ante «confidencial», «reservado» o «restringido», «advertencia» ante «uso interno» y «sin alerta» sin marcas.

#### Scenario: Datos personales
- **WHEN** el contenido incluye datos personales sintéticos
- **THEN** `RJ-01` devuelve «advertencia» (CP-01, RJ-01)

#### Scenario: Dato sensible o indicio de menores
- **WHEN** el contenido incluye un dato de sensibilidad alta sintético o indicios de datos de menores
- **THEN** `RJ-01` devuelve «requiere revisión humana» con una advertencia reforzada que indica que su tratamiento tiene reglas especiales y que el sistema no verifica autorizaciones; no afirma una prohibición (CP-01, RJ-01)

#### Scenario: Marca reservado
- **WHEN** el contenido incluye la marca «reservado»
- **THEN** `RJ-02` devuelve «requiere revisión humana» (CP-03, RJ-02)

#### Scenario: Marca de uso interno
- **WHEN** el contenido incluye solo la marca «uso interno»
- **THEN** `RJ-02` devuelve «advertencia» (CP-05, RJ-02)

#### Scenario: Contenido sin indicadores
- **WHEN** el contenido no tiene hallazgos ni marcas
- **THEN** `RJ-01` y `RJ-02` devuelven «sin alerta» con el aviso de que no equivale a autorización (CP-02)

### Requirement: POL-04 Evaluación de las condiciones del proveedor (RJ-04)
[MVP esencial] Con proveedor seleccionado, el sistema SHALL evaluar `RJ-04` solo con las condiciones del catálogo: «requiere revisión humana» si el proveedor no tiene información verificada, o si hay hallazgo relevante y el uso para mejorar modelos es «sí» o «no informado»; «advertencia» si hay hallazgo relevante con otras condiciones; «sin alerta» sin hallazgos relevantes.

#### Scenario: Proveedor que usa el contenido para mejorar modelos
- **WHEN** el contenido tiene un hallazgo relevante y el proveedor declara el uso para mejorar modelos como «sí»
- **THEN** `RJ-04` devuelve «requiere revisión humana» y cita la condición, la fuente y la fecha (CP-01, RJ-04)

#### Scenario: Condición no informada
- **WHEN** el contenido tiene un hallazgo relevante y la fuente no informa el uso para mejorar modelos
- **THEN** `RJ-04` devuelve «requiere revisión humana» e indica «no informado en la fuente»

#### Scenario: Condiciones favorables con hallazgo relevante
- **WHEN** el contenido tiene un hallazgo relevante y el proveedor declara el uso para mejorar modelos como «no»
- **THEN** `RJ-04` devuelve «advertencia»

#### Scenario: Sin hallazgos relevantes
- **WHEN** el contenido no tiene hallazgos relevantes y las condiciones del proveedor están informadas
- **THEN** `RJ-04` devuelve «sin alerta»

#### Scenario: Proveedor sin información verificada
- **WHEN** el usuario selecciona un proveedor sin entrada verificada en el catálogo
- **THEN** `RJ-04` devuelve «requiere revisión humana» (CP-06)

#### Scenario: Condiciones que no intervienen
- **WHEN** dos entradas del catálogo difieren solo en retención, exclusión o ubicación
- **THEN** `RJ-04` devuelve el mismo resultado y esas condiciones se muestran como «información para revisión humana» (CP-01)

### Requirement: POL-05 Proveedor no seleccionado
[MVP esencial] Si no se selecciona proveedor, el sistema SHALL continuar la detección y la clasificación, registrar «evaluación de proveedor no completada», marcar `RJ-04` como «no evaluada», informar los hallazgos y exigir revisión humana antes de cualquier recomendación de divulgación cuando existan hallazgos relevantes. «Sin proveedor» no equivale a «proveedor seguro».

#### Scenario: Sin proveedor y con datos personales
- **WHEN** el contenido tiene datos personales sintéticos y no se selecciona proveedor
- **THEN** el sistema muestra los hallazgos, marca `RJ-04` como «no evaluada» y el resultado global es «requiere revisión humana» (CP-07)

#### Scenario: Sin proveedor y sin hallazgos relevantes
- **WHEN** el contenido no tiene hallazgos relevantes y no se selecciona proveedor
- **THEN** `RJ-04` queda «no evaluada» y el resultado global es al menos «advertencia», nunca «sin alerta»

#### Scenario: Vocabulario del resultado
- **WHEN** se muestra una evaluación sin proveedor
- **THEN** el texto dice «no evaluado» y no usa «seguro», «aprobado» ni «autorizado» (CP-07)

### Requirement: POL-06 Resultado global más restrictivo
[MVP esencial] El sistema SHALL calcular el resultado global como el más restrictivo entre reglas, políticas y controles («sin alerta» < «advertencia» < «requiere revisión humana»), SHALL NOT devolver «sin alerta» si alguna regla aplicable quedó «no evaluada» y SHALL listar todos los resultados cuando difieran.

#### Scenario: Un resultado requiere revisión
- **WHEN** al menos una regla, política o control devuelve «requiere revisión humana»
- **THEN** el resultado global es «requiere revisión humana»

#### Scenario: Regla y política en conflicto
- **WHEN** `RJ-02` devuelve «advertencia» y una política devuelve «requiere revisión humana»
- **THEN** el resultado global es «requiere revisión humana» y se listan ambos resultados con su rótulo (CP-05)

#### Scenario: Regla no evaluada
- **WHEN** todas las demás reglas devuelven «sin alerta» y una está «no evaluada»
- **THEN** el resultado global es «advertencia»

### Requirement: POL-07 RJ-05 como regla transversal de controles funcionales
[MVP esencial] El sistema SHALL tratar `RJ-05` como regla transversal de controles funcionales, no de detección de contenido ni obligación legal específica: CT-01 sin transmisión externa, CT-02 descarte del original, CT-03 enmascarado, CT-04 registro sin contenido original y CT-05 revisión humana ante ambigüedad. Por evaluación SHALL registrar cada control como «aplicado» o «no aplicado»; uno «no aplicado» exige revisión humana.

#### Scenario: Evaluación con controles aplicados
- **WHEN** una evaluación finaliza con normalidad
- **THEN** CT-01 a CT-05 figuran como «aplicado» en el informe (CP-12)

#### Scenario: Control no aplicado
- **WHEN** el descarte del contenido original no se logra
- **THEN** CT-02 figura como «no aplicado» y el resultado global es «requiere revisión humana» (CP-10)

#### Scenario: CT-05 aplicado
- **WHEN** el resultado global es «requiere revisión humana», la clasificación está pendiente o un control está «no aplicado»
- **THEN** la evaluación queda «pendiente de revisión», CT-05 figura «aplicado» y no se emite ninguna recomendación de divulgación (CP-08)

#### Scenario: CT-05 no aplicado
- **WHEN** una evaluación en esas condiciones no queda «pendiente de revisión»
- **THEN** CT-05 figura «no aplicado» y se exige revisión humana

#### Scenario: CT-06 diferenciado
- **WHEN** se muestra el estado de los controles de una evaluación
- **THEN** CT-06 (historial que no se sobrescribe) no se registra por evaluación y se verifica mediante `REP-07` (CP-13)

#### Scenario: Independencia del contenido
- **WHEN** se evalúa un contenido sin hallazgos
- **THEN** el estado de los controles se muestra igualmente y no depende de los hallazgos (CP-02)

### Requirement: POL-08 Explicabilidad de cada resultado
[MVP esencial] El sistema SHALL mostrar, para cada resultado, su identificador y tipo, la condición que se cumplió, los hallazgos o datos que lo activaron y el estado de validación de su fundamento.

#### Scenario: Regla provisional
- **WHEN** una regla provisional produce una advertencia
- **THEN** el resultado muestra la condición, los hallazgos y la marca «regla provisional» (CP-01)

#### Scenario: Política organizacional
- **WHEN** una política produce un resultado
- **THEN** el resultado identifica la política y el dato que la activó (CP-05)

#### Scenario: Resultado sin alerta
- **WHEN** una regla devuelve «sin alerta»
- **THEN** el resultado muestra la condición evaluada e indica que ningún hallazgo la activó (CP-02)

### Requirement: POL-09 Prohibición de lenguaje de certificación
[MVP esencial] El sistema SHALL NOT usar términos que sugieran certificación o dictamen, como «cumple», «no cumple», «legal», «ilegal», «autorizado» o «aprobado», en los resultados de reglas, políticas y controles.

#### Scenario: Revisión de los textos del resultado
- **WHEN** se revisan todos los textos que muestra una evaluación
- **THEN** no aparece ninguno de los términos prohibidos asociados al resultado (CP-12)

#### Scenario: Control aplicado
- **WHEN** se muestra el estado de un control funcional
- **THEN** se usa «aplicado» o «no aplicado» y no «cumple» ni «no cumple»

### Requirement: POL-10 Gestión de políticas organizacionales
[MVP esencial] El sistema SHALL permitir que un Administrador cree, active y desactive políticas con nombre, condición (nivel de clasificación, categoría de hallazgo o proveedor) y resultado recomendado. Los cambios se registran en el historial (REP-07).

#### Scenario: Creación y activación
- **WHEN** un Administrador crea una política completa y la activa
- **THEN** la política se aplica a las evaluaciones posteriores (CP-05)

#### Scenario: Política incompleta
- **WHEN** un Administrador intenta activar una política sin condición o sin resultado
- **THEN** el sistema rechaza la activación e indica el campo faltante

#### Scenario: Intento de un Trabajador
- **WHEN** un usuario con perfil Trabajador intenta crear o activar una política
- **THEN** el sistema deniega la acción (CP-11)

#### Scenario: Desactivación
- **WHEN** un Administrador desactiva una política
- **THEN** deja de aplicarse a las evaluaciones posteriores y las anteriores conservan la versión aplicada

### Requirement: POL-11 Evaluación sin políticas activas (RJ-03)
[MVP esencial] Sin políticas activas, el sistema SHALL marcar `RJ-03` como «no evaluada», informar «no hay políticas organizacionales activas» y recomendar al Administrador definirlas, sin tratar la ausencia como permiso.

#### Scenario: Organización sin políticas
- **WHEN** no hay políticas organizacionales activas
- **THEN** el sistema marca `RJ-03` como «no evaluada», muestra el aviso y el resultado global no es «sin alerta» (CP-04, RJ-03)

#### Scenario: Primera política activada
- **WHEN** un Administrador activa una política y se vuelve a someter el mismo contenido
- **THEN** `RJ-03` se evalúa y el aviso desaparece (CP-05)
