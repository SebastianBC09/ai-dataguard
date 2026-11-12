# Spec Delta

## Purpose

Evalúa el resultado de la clasificación frente a reglas jurídicas preliminares (`RJ-01` a `RJ-05`) y políticas organizacionales, y entrega alertas explicables que requieren revisión humana. Las reglas `RJ` son **provisionales** hasta que E2 las investigue, valide y apruebe; no son obligaciones jurídicas confirmadas ni certificaciones.

## ADDED Requirements

### Requirement: Registro de reglas jurídicas preliminares
El sistema SHALL mantener cada regla `RJ-01` a `RJ-05` con identificador, condición, resultado asociado, fundamento, categoría y estado de validación. Una regla sin fuente verificada SHALL figurar como "pendiente de fuente".

#### Scenario: Regla con fuente verificada
- **WHEN** E2 aprueba una regla con fuente verificada
- **THEN** su estado cambia a "validada" y el fundamento cita la fuente

#### Scenario: Regla sin fuente verificada
- **WHEN** una regla no tiene fuente verificada
- **THEN** el sistema la muestra como "pendiente de fuente" y como provisional, no como obligación

#### Scenario: Cantidad de reglas
- **WHEN** se consulta el registro de reglas
- **THEN** aparecen exactamente cinco reglas con los identificadores `RJ-01` a `RJ-05`

### Requirement: Categoría del fundamento de cada regla
El sistema SHALL clasificar el fundamento de cada regla en una de estas categorías: obligación legal respaldada por fuente verificada, interpretación pendiente de revisión jurídica, política corporativa propuesta, o regla funcional de AI DataGuard.

#### Scenario: Regla funcional propia
- **WHEN** una regla expresa un comportamiento propio del sistema y no una norma
- **THEN** su categoría es "regla funcional de AI DataGuard"

#### Scenario: Interpretación pendiente
- **WHEN** una regla depende de una interpretación normativa no revisada
- **THEN** su categoría es "interpretación pendiente de revisión jurídica"

#### Scenario: Categoría ausente
- **WHEN** una regla no tiene categoría asignada
- **THEN** el sistema impide activarla en las evaluaciones

### Requirement: Evaluación contra las reglas activas
El sistema SHALL evaluar cada resultado de clasificación contra todas las reglas activas y devolver, por regla, uno de estos resultados: "sin alerta", "advertencia" o "requiere revisión humana".

#### Scenario: Datos personales hacia IA externa
- **WHEN** la evaluación contiene datos personales y el usuario indica un proveedor externo de IA
- **THEN** la regla correspondiente a `RJ-01` devuelve al menos "advertencia" (CP-01, RJ-01)

#### Scenario: Información corporativa reservada
- **WHEN** la evaluación contiene información corporativa confidencial
- **THEN** la regla correspondiente a `RJ-02` devuelve "requiere revisión humana" (CP-03, RJ-02)

#### Scenario: Ningún indicador
- **WHEN** la evaluación no tiene hallazgos
- **THEN** todas las reglas devuelven "sin alerta" con la advertencia de que no equivale a autorización (CP-02)

#### Scenario: Información insuficiente para decidir
- **WHEN** una regla necesita un dato que no está disponible, como el proveedor previsto
- **THEN** la regla devuelve "requiere revisión humana" e indica el dato faltante

### Requirement: Resultado global más restrictivo
El sistema SHALL calcular el resultado global de la evaluación como el más restrictivo entre los resultados de todas las reglas y políticas aplicadas, en el orden "sin alerta", "advertencia", "requiere revisión humana".

#### Scenario: Un resultado requiere revisión
- **WHEN** al menos una regla o política devuelve "requiere revisión humana"
- **THEN** el resultado global es "requiere revisión humana"

#### Scenario: Solo advertencias
- **WHEN** ninguna devuelve "requiere revisión humana" y alguna devuelve "advertencia"
- **THEN** el resultado global es "advertencia"

### Requirement: Explicabilidad de cada resultado
El sistema SHALL mostrar, para cada resultado de regla o política, su identificador, la condición que se cumplió, los hallazgos que la activaron y el estado de validación de su fundamento.

#### Scenario: Resultado de regla provisional
- **WHEN** una regla provisional produce una advertencia
- **THEN** el resultado muestra la condición, los hallazgos y la marca "regla provisional"

#### Scenario: Resultado de política organizacional
- **WHEN** una política organizacional produce un resultado
- **THEN** el resultado identifica la política y el hallazgo que la activó

### Requirement: Prohibición de lenguaje de certificación
El sistema SHALL NOT usar términos que sugieran certificación o dictamen, como "cumple", "no cumple", "legal", "ilegal", "autorizado" o "aprobado", en los resultados de las reglas, y SHALL incluir la aclaración de que es un apoyo a la revisión humana.

#### Scenario: Revisión de textos del resultado
- **WHEN** se revisan todos los textos que muestra la evaluación
- **THEN** no aparece ninguno de los términos prohibidos asociados al resultado legal

#### Scenario: Aclaración presente
- **WHEN** el sistema muestra un resultado de reglas
- **THEN** incluye la aclaración de que no es certificación ni asesoría jurídica

### Requirement: Gestión de políticas organizacionales
El sistema SHALL permitir que un Administrador cree, edite, active y desactive políticas organizacionales, registrando cada cambio con quién, cuándo y qué cambió.

#### Scenario: Creación de política
- **WHEN** un Administrador crea una política con nombre, condición y resultado recomendado
- **THEN** el sistema la guarda y la deja disponible para activarla

#### Scenario: Edición registrada
- **WHEN** un Administrador edita una política activa
- **THEN** el sistema registra el cambio con la persona, la fecha y los valores anterior y nuevo

#### Scenario: Intento de un Trabajador
- **WHEN** un usuario con perfil Trabajador intenta crear o editar una política
- **THEN** el sistema deniega la acción (CP-09)

#### Scenario: Política incompleta
- **WHEN** un Administrador intenta activar una política sin condición o sin resultado recomendado
- **THEN** el sistema rechaza la activación e indica el campo faltante

### Requirement: Evaluación sin políticas configuradas
El sistema SHALL completar la evaluación con las reglas `RJ` cuando la organización no tenga políticas activas, informar esa situación y no tratarla como permiso.

#### Scenario: Organización sin políticas
- **WHEN** no existen políticas organizacionales activas
- **THEN** la evaluación usa solo las reglas, informa "no hay políticas configuradas" y recomienda al Administrador definirlas (CP-04, RJ-03)

### Requirement: Conflicto entre regla y política
El sistema SHALL mostrar el resultado más restrictivo cuando una regla y una política produzcan resultados distintos, y SHALL listar ambos. Esta resolución es una propuesta pendiente de aprobación.

#### Scenario: Resultados distintos
- **WHEN** una regla devuelve "advertencia" y una política devuelve "requiere revisión humana"
- **THEN** el sistema muestra "requiere revisión humana" y lista ambos resultados (CP-05, RJ-03)

### Requirement: Registro de versiones aplicadas
El sistema SHALL registrar en cada evaluación la versión de las reglas y de las políticas aplicadas.

#### Scenario: Evaluación registrada
- **WHEN** finaliza una evaluación
- **THEN** el registro incluye la versión de cada regla y política utilizada

#### Scenario: Cambio posterior de una política
- **WHEN** un Administrador modifica una política después de una evaluación
- **THEN** la evaluación anterior conserva la versión que se aplicó entonces
