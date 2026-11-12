# Spec Delta

## Purpose

Permite al usuario someter un texto o documento a un análisis preventivo, en un entorno controlado y sin transmitir su contenido a terceros, antes de usarlo con herramientas de IA generativa. Es una especificación **provisional**, pendiente de aprobación docente (E1 y E2).

## ADDED Requirements

### Requirement: Identificación del usuario antes del análisis
El sistema SHALL requerir que el usuario esté identificado con un perfil vigente (Trabajador, Administrador o Responsable de cumplimiento) antes de permitirle someter contenido a análisis. El mecanismo de identificación queda aplazado (C3).

#### Scenario: Usuario identificado envía contenido
- **WHEN** un usuario identificado con perfil Trabajador somete un texto
- **THEN** el sistema inicia el análisis y le asigna un identificador de evaluación

#### Scenario: Usuario no identificado
- **WHEN** una persona no identificada intenta someter contenido
- **THEN** el sistema rechaza la solicitud sin procesar ni conservar el contenido

#### Scenario: Perfil desactivado
- **WHEN** un usuario cuyo perfil fue desactivado intenta someter contenido
- **THEN** el sistema deniega el acceso e informa que debe contactar al Administrador

### Requirement: Ingreso de texto directo
El sistema SHALL permitir ingresar texto directamente para su análisis, rechazando entradas vacías y entradas que superen el límite máximo de tamaño. El valor del límite está pendiente de definición en E3 (O-03).

#### Scenario: Texto válido
- **WHEN** el usuario ingresa un texto no vacío dentro del límite de tamaño
- **THEN** el sistema acepta el texto e inicia el análisis

#### Scenario: Texto vacío
- **WHEN** el usuario envía un texto vacío o compuesto solo por espacios
- **THEN** el sistema rechaza la entrada e indica que no hay contenido para analizar

#### Scenario: Texto en el límite exacto
- **WHEN** el tamaño del texto es igual al límite máximo configurado
- **THEN** el sistema acepta el texto y lo analiza completo

#### Scenario: Texto que excede el límite
- **WHEN** el tamaño del texto supera en una unidad el límite máximo configurado
- **THEN** el sistema rechaza la entrada, informa el límite y no realiza un análisis parcial silencioso

### Requirement: Ingreso de documentos en formatos soportados
El sistema SHALL permitir someter documentos solo en los formatos declarados como soportados y SHALL mostrar esa lista antes del envío. La lista de formatos del MVP está pendiente (O-03).

#### Scenario: Formato soportado
- **WHEN** el usuario somete un documento en un formato de la lista soportada
- **THEN** el sistema inicia el análisis del documento

#### Scenario: Formato no soportado
- **WHEN** el usuario somete un documento en un formato fuera de la lista
- **THEN** el sistema rechaza el documento, muestra los formatos soportados y no conserva el archivo

#### Scenario: Documento corrupto o protegido
- **WHEN** el usuario somete un documento que no puede abrirse por estar dañado o protegido
- **THEN** el sistema rechaza el documento indicando el motivo y no conserva el archivo

### Requirement: Análisis sin transmisión externa del contenido
El sistema SHALL completar el análisis sin enviar el contenido evaluado, ni fragmentos derivados de él, a servicios o proveedores externos.

#### Scenario: Análisis sin conexión externa
- **WHEN** se ejecuta un análisis en un entorno sin acceso a servicios externos
- **THEN** el análisis se completa y entrega resultados (CP-08)

#### Scenario: Verificación de salida de datos
- **WHEN** se analiza contenido sintético con marcadores únicos y se observa toda comunicación saliente
- **THEN** ningún marcador del contenido aparece fuera del entorno controlado (CP-08)

#### Scenario: Componente opcional basado en IA
- **WHEN** el análisis utiliza un componente basado en IA
- **THEN** dicho componente opera dentro del entorno controlado y no depende de servicios externos (O-07)

### Requirement: Hallazgos con explicación
El sistema SHALL producir, por cada análisis, una lista de hallazgos que incluya para cada uno el tipo de indicador, su ubicación aproximada, un grado de certeza (alto, medio o bajo) y un motivo comprensible.

#### Scenario: Contenido con datos personales sintéticos
- **WHEN** se analiza un texto que contiene datos personales sintéticos
- **THEN** el sistema lista un hallazgo por cada dato con tipo, ubicación, certeza y motivo (CP-01, RJ-01)

#### Scenario: Contenido con varios tipos de indicadores
- **WHEN** el contenido incluye indicadores de más de un tipo
- **THEN** el sistema presenta hallazgos separados por tipo

#### Scenario: Contenido sin indicadores
- **WHEN** el análisis no detecta ningún indicador
- **THEN** el sistema devuelve una lista vacía y el resultado "sin indicadores detectados" (CP-02)

### Requirement: Fragmentos enmascarados por defecto
El sistema SHALL mostrar los fragmentos asociados a los hallazgos parcialmente enmascarados, de modo que el valor completo no sea legible en pantallas ni en informes.

#### Scenario: Valor identificador detectado
- **WHEN** un hallazgo corresponde a un identificador personal
- **THEN** el sistema muestra solo una parte del valor y enmascara el resto

#### Scenario: Valor demasiado corto para enmascarar parcialmente
- **WHEN** el valor detectado es demasiado corto para mostrar una parte sin revelarlo
- **THEN** el sistema oculta el valor por completo

### Requirement: Análisis parcial exige revisión humana
El sistema SHALL marcar el análisis como parcial y como "requiere revisión humana" cuando alguna parte del contenido no pueda analizarse, y no SHALL emitir "sin indicadores detectados" en ese caso.

#### Scenario: Sección no analizable
- **WHEN** un documento contiene una sección ilegible o no soportada
- **THEN** el sistema marca el análisis como parcial, indica la parte omitida y exige revisión humana (CP-07)

#### Scenario: Documento completamente analizable
- **WHEN** todo el contenido del documento puede analizarse
- **THEN** el sistema no marca el análisis como parcial

#### Scenario: Contenido totalmente ilegible
- **WHEN** ninguna parte del contenido puede analizarse
- **THEN** el sistema no declara "sin indicadores detectados" y exige revisión humana

### Requirement: Ausencia de alertas no equivale a autorización
El sistema SHALL acompañar todo resultado de análisis, incluso el que no tenga hallazgos, con la advertencia de que la ausencia de alertas no autoriza la divulgación ni certifica cumplimiento.

#### Scenario: Resultado sin hallazgos
- **WHEN** el análisis no produce hallazgos
- **THEN** el resultado incluye la advertencia de que no equivale a autorización (CP-02)

#### Scenario: Resultado con hallazgos
- **WHEN** el análisis produce hallazgos
- **THEN** el resultado incluye la misma advertencia

#### Scenario: Resultado parcial
- **WHEN** el análisis es parcial
- **THEN** el resultado incluye la advertencia junto con la indicación de que es parcial

### Requirement: Descarte del contenido original
El sistema SHALL no conservar el contenido original (texto o archivo) cuando la evaluación finalice, se cancele o falle, salvo necesidad justificada y aprobada. La excepción está pendiente de decisión (O-06).

#### Scenario: Evaluación finalizada
- **WHEN** el análisis termina y se registra la evaluación
- **THEN** el contenido original no puede recuperarse desde el registro persistente ni desde el informe (CP-08)

#### Scenario: Evaluación cancelada
- **WHEN** el usuario cancela la evaluación antes de que termine
- **THEN** el sistema descarta el contenido recibido

#### Scenario: Fallo durante el análisis
- **WHEN** el análisis falla a mitad del proceso
- **THEN** el sistema descarta el contenido y registra el error sin incluir el contenido

### Requirement: Consistencia del análisis
El sistema SHALL producir los mismos hallazgos cuando se analiza el mismo contenido con la misma versión de reglas y configuración.

#### Scenario: Repetición del mismo análisis
- **WHEN** el mismo contenido se analiza dos veces con la misma configuración
- **THEN** ambas evaluaciones muestran los mismos hallazgos

#### Scenario: Cambio de configuración
- **WHEN** cambia la versión de reglas o configuración entre dos análisis del mismo contenido
- **THEN** cada evaluación registra la versión utilizada para explicar cualquier diferencia
