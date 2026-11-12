# Spec Delta

## Purpose

Permite consultar las condiciones de tratamiento de información de proveedores de IA generativa mediante un catálogo con fuente y fecha de verificación, sin enviar contenido evaluado a ningún tercero. El origen y los datos del catálogo están **pendientes de decisión** (O-04) y no constituyen una garantía del proveedor.

## ADDED Requirements

### Requirement: Entradas del catálogo con fuente y fecha
El sistema SHALL registrar cada entrada del catálogo con proveedor, servicio o plan, condiciones de tratamiento de información, fuente consultada y fecha de verificación. El conjunto exacto de condiciones es una propuesta pendiente (O-04).

#### Scenario: Entrada completa
- **WHEN** un Administrador registra una entrada con proveedor, condiciones, fuente y fecha
- **THEN** el sistema la guarda y queda disponible para consulta

#### Scenario: Entrada sin fuente
- **WHEN** un Administrador intenta guardar una entrada sin fuente
- **THEN** el sistema rechaza el registro e indica que la fuente es obligatoria

#### Scenario: Entrada sin fecha de verificación
- **WHEN** un Administrador intenta guardar una entrada sin fecha de verificación
- **THEN** el sistema rechaza el registro

### Requirement: Consulta de condiciones por proveedor
El sistema SHALL permitir que cualquier usuario identificado consulte las condiciones registradas de un proveedor, mostrando la fuente y la fecha de verificación de cada dato.

#### Scenario: Proveedor registrado
- **WHEN** un usuario consulta un proveedor registrado
- **THEN** el sistema muestra sus condiciones con fuente y fecha de verificación

#### Scenario: Proveedor no registrado
- **WHEN** un usuario consulta un proveedor que no está en el catálogo
- **THEN** el sistema informa "sin información verificada", no deduce condiciones y sugiere consultar a un Revisor (CP-06)

#### Scenario: Condición no informada por la fuente
- **WHEN** la fuente no informa una condición determinada
- **THEN** el sistema muestra "no informado en la fuente" y no la infiere

### Requirement: Indicación de información posiblemente desactualizada
El sistema SHALL marcar como "posiblemente desactualizada" toda entrada cuya antigüedad desde la fecha de verificación supere el periodo de vigencia configurado. El valor del periodo está pendiente de definición.

#### Scenario: Entrada vencida
- **WHEN** la antigüedad de una entrada supera el periodo de vigencia
- **THEN** el sistema la marca como posiblemente desactualizada (CP-06, RJ-04)

#### Scenario: Entrada en el límite exacto
- **WHEN** la antigüedad de una entrada es igual al periodo de vigencia
- **THEN** el sistema no la marca como desactualizada

#### Scenario: Entrada actualizada
- **WHEN** un Administrador actualiza la fecha de verificación y la fuente de una entrada vencida
- **THEN** el sistema retira la marca de desactualización

### Requirement: Mantenimiento del catálogo por el Administrador
El sistema SHALL permitir que solo un Administrador cree, edite o retire entradas del catálogo, registrando quién, cuándo y qué cambió.

#### Scenario: Edición por un Administrador
- **WHEN** un Administrador edita una entrada
- **THEN** el sistema registra el cambio con persona, fecha y valores anterior y nuevo

#### Scenario: Edición por un Trabajador
- **WHEN** un usuario con perfil Trabajador intenta editar una entrada
- **THEN** el sistema deniega la acción (CP-09)

### Requirement: Consulta sin transmisión del contenido evaluado
El sistema SHALL NOT enviar el contenido evaluado, ni fragmentos derivados de él, al proveedor consultado ni a ningún servicio externo al consultar el catálogo.

#### Scenario: Consulta durante una evaluación
- **WHEN** se consulta un proveedor durante una evaluación de contenido sintético con marcadores únicos
- **THEN** ningún marcador del contenido sale del entorno controlado (CP-08)

### Requirement: Incorporación del proveedor previsto a la evaluación
El sistema SHALL permitir que el usuario indique el proveedor previsto y SHALL incluir sus condiciones, con fuente y fecha, en la evaluación y en la regla correspondiente a `RJ-04`.

#### Scenario: Proveedor con condiciones desfavorables
- **WHEN** el usuario indica un proveedor cuyas condiciones registradas incluyen el uso de datos para mejorar sus modelos y el contenido tiene datos personales
- **THEN** la evaluación devuelve al menos "advertencia" y cita la condición, la fuente y la fecha (CP-06, RJ-04)

#### Scenario: Proveedor sin información verificada
- **WHEN** el usuario indica un proveedor sin información verificada
- **THEN** la evaluación devuelve "requiere revisión humana" (CP-06)

#### Scenario: Sin proveedor indicado
- **WHEN** el usuario no indica proveedor
- **THEN** la evaluación continúa y registra que no se evaluaron condiciones de proveedor

### Requirement: Condiciones presentadas como declaradas por la fuente
El sistema SHALL presentar las condiciones del proveedor como declaradas por la fuente citada y SHALL NOT calificar a un proveedor como "seguro" ni como "cumplidor".

#### Scenario: Visualización de condiciones
- **WHEN** el sistema muestra las condiciones de un proveedor
- **THEN** las identifica como declaradas por la fuente y no usa calificativos de seguridad o cumplimiento

### Requirement: Distinción entre entradas reales y de ejemplo
El sistema SHALL distinguir visiblemente las entradas verificadas de las entradas ficticias de ejemplo. La decisión sobre el uso de datos reales o ficticios está pendiente (O-04).

#### Scenario: Entrada de ejemplo
- **WHEN** una entrada está marcada como ficticia
- **THEN** el sistema la muestra con la etiqueta "ejemplo" y la excluye de cualquier informe presentado como verificado

#### Scenario: Entrada verificada
- **WHEN** una entrada tiene fuente real y fecha de verificación
- **THEN** el sistema la muestra sin la etiqueta "ejemplo"
