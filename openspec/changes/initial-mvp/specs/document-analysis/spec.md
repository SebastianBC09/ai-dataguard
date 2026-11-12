# Spec Delta

## Purpose

Permite al usuario someter un texto o documento a un análisis preventivo, en un entorno controlado y sin transmitir su contenido a terceros, antes de usarlo con herramientas de IA generativa. Especificación **provisional**, pendiente de aprobación docente (E1 y E2). Cada requisito tiene un identificador estable y una clase: [MVP esencial] o [Complementario]; la clase [Evolución posterior] se documenta fuera de las specs, en `design.md`.

## ADDED Requirements

### Requirement: DOC-01 Identificación y perfil del usuario
[MVP esencial] El sistema SHALL requerir que el usuario esté identificado con un perfil (Trabajador o Administrador) antes de someter contenido a análisis. El mecanismo de identificación y el alta de usuarios quedan fuera de este cambio (C3, O-10).

#### Scenario: Usuario identificado envía contenido
- **WHEN** un usuario identificado con perfil Trabajador somete un texto
- **THEN** el sistema inicia el análisis y registra el usuario y el perfil en la evaluación (CP-01)

#### Scenario: Usuario no identificado
- **WHEN** una persona no identificada intenta someter contenido
- **THEN** el sistema rechaza la solicitud sin procesar ni conservar el contenido (CP-11)

### Requirement: DOC-02 Ingreso de texto directo
[MVP esencial] El sistema SHALL permitir ingresar texto directamente para su análisis, rechazando entradas vacías y las que superen el límite máximo de tamaño. Es la entrada esencial del MVP. El valor del límite está pendiente (O-03).

#### Scenario: Texto válido
- **WHEN** el usuario ingresa un texto no vacío dentro del límite de tamaño
- **THEN** el sistema acepta el texto e inicia el análisis (CP-01)

#### Scenario: Texto vacío
- **WHEN** el usuario envía un texto vacío o compuesto solo por espacios
- **THEN** el sistema rechaza la entrada e indica que no hay contenido para analizar

#### Scenario: Texto en el límite exacto
- **WHEN** el tamaño del texto es igual al límite máximo configurado
- **THEN** el sistema acepta el texto y lo analiza completo

#### Scenario: Texto que excede el límite
- **WHEN** el tamaño del texto supera en una unidad el límite máximo configurado
- **THEN** el sistema rechaza la entrada, informa el límite y no realiza un análisis parcial silencioso

### Requirement: DOC-03 Ingreso de documentos PDF con texto extraíble
[Complementario] El sistema SHALL permitir someter documentos PDF con texto extraíble, mostrando antes del envío que ese es el único formato de documento soportado. No se admiten otros formatos en el MVP (O-03). El texto directo (DOC-02) sigue siendo la entrada esencial.

#### Scenario: PDF con texto extraíble
- **WHEN** el usuario somete un PDF cuyo texto puede extraerse
- **THEN** el sistema inicia el análisis del texto del documento

#### Scenario: Formato no soportado
- **WHEN** el usuario somete un documento en un formato distinto de PDF
- **THEN** el sistema rechaza el documento, informa que solo admite PDF con texto extraíble y no conserva el archivo

#### Scenario: PDF sin texto extraíble
- **WHEN** el usuario somete un PDF del que no puede extraerse texto
- **THEN** el sistema rechaza el documento indicando el motivo y no conserva el archivo

#### Scenario: Documento corrupto o protegido
- **WHEN** el usuario somete un PDF que no puede abrirse por estar dañado o protegido
- **THEN** el sistema rechaza el documento indicando el motivo y no conserva el archivo

### Requirement: DOC-04 Análisis sin transmisión externa (control CT-01)
[MVP esencial] El sistema SHALL completar el análisis y la consulta del catálogo sin enviar el contenido, ni fragmentos derivados, a servicios externos. «Entorno controlado» significa que el recorrido completo se realiza con las conexiones externas bloqueadas.

#### Scenario: Recorrido con conexiones externas bloqueadas
- **WHEN** se ejecuta una evaluación completa con todas las conexiones externas bloqueadas
- **THEN** la evaluación finaliza y entrega clasificación, resultado e informe (CP-09)

#### Scenario: Verificación con marcadores únicos
- **WHEN** se evalúa contenido sintético con marcadores únicos y se observa toda comunicación saliente
- **THEN** ningún marcador aparece fuera del entorno controlado (CP-09)

#### Scenario: Consulta del catálogo durante la evaluación
- **WHEN** se consulta un proveedor durante una evaluación
- **THEN** la consulta no envía el contenido ni fragmentos derivados a ningún servicio (CP-09)

#### Scenario: Función que intenta una conexión externa
- **WHEN** durante una evaluación alguna función intenta contactar un servicio externo
- **THEN** la conexión se bloquea, no sale contenido ni fragmentos y el control CT-01 queda «no aplicado» si algo saliera (CP-09)

#### Scenario: Componente opcional basado en IA
- **WHEN** el análisis utiliza un componente basado en IA
- **THEN** dicho componente opera dentro del entorno controlado y sin servicios externos (O-07)

### Requirement: DOC-05 Hallazgos con explicación y criterios de certeza
[MVP esencial] El sistema SHALL listar por cada hallazgo su tipo, su ubicación (número de línea o de párrafo), su certeza y su motivo. Certeza alta: el valor cumple el formato del tipo y tiene una etiqueta de contexto; media: cumple el formato sin contexto; baja: coincide solo parcialmente o es compatible con más de un tipo.

#### Scenario: Valor con etiqueta de contexto
- **WHEN** el texto incluye un correo sintético precedido de la etiqueta «correo:»
- **THEN** el hallazgo indica tipo, línea, certeza alta y motivo (CP-01)

#### Scenario: Valor sin etiqueta de contexto
- **WHEN** el mismo correo sintético aparece sin etiqueta
- **THEN** el hallazgo tiene certeza media

#### Scenario: Valor compatible con varios tipos
- **WHEN** el texto incluye una secuencia numérica sintética que puede ser un documento de identidad o un teléfono
- **THEN** el hallazgo tiene certeza baja y cita ambos tipos posibles (CP-08)

#### Scenario: Contenido sin indicadores
- **WHEN** el análisis no detecta ningún indicador
- **THEN** el sistema devuelve una lista vacía y el resultado de detección «sin indicadores detectados» (CP-02)

### Requirement: DOC-06 Valores enmascarados (control CT-03)
[MVP esencial] El sistema SHALL mostrar los valores asociados a hallazgos con máscara: como máximo los dos últimos caracteres visibles. Los valores de cuatro caracteres o menos SHALL ocultarse por completo.

#### Scenario: Valor largo
- **WHEN** un hallazgo corresponde a un valor de diez caracteres
- **THEN** el sistema muestra solo los dos últimos y oculta los demás (CP-12)

#### Scenario: Valor de cuatro caracteres
- **WHEN** el valor detectado tiene cuatro caracteres
- **THEN** el sistema lo oculta por completo

#### Scenario: Valor de cinco caracteres
- **WHEN** el valor detectado tiene cinco caracteres
- **THEN** el sistema muestra solo los dos últimos y oculta los otros tres

### Requirement: DOC-07 Análisis independiente del proveedor
[MVP esencial] El sistema SHALL ejecutar la detección y la clasificación sin exigir un proveedor de IA seleccionado e informar los hallazgos. La falta de proveedor se trata según POL-05 y PRV-03, con el mismo comportamiento en las tres capacidades.

#### Scenario: Sin proveedor y con datos personales
- **WHEN** el usuario somete contenido con datos personales sintéticos sin seleccionar proveedor
- **THEN** el sistema muestra los hallazgos y la clasificación, e indica «evaluación de proveedor no completada» (CP-07)

#### Scenario: Sin proveedor y sin hallazgos
- **WHEN** el usuario somete contenido sin indicadores y sin proveedor
- **THEN** el análisis finaliza y registra «evaluación de proveedor no completada»

#### Scenario: Con proveedor seleccionado
- **WHEN** el mismo contenido se evalúa con un proveedor seleccionado
- **THEN** los hallazgos son los mismos que sin proveedor (CP-01)

### Requirement: DOC-08 Descarte del contenido original (control CT-02)
[MVP esencial] El sistema SHALL descartar el contenido original (texto o archivo) cuando la evaluación finalice, se cancele o falle, salvo necesidad justificada y aprobada (O-06), y SHALL marcar el control como «no aplicado» y exigir revisión humana si el descarte no se logra.

#### Scenario: Evaluación finalizada
- **WHEN** el análisis termina y se registra la evaluación
- **THEN** el contenido original no puede recuperarse desde el registro ni desde el informe (CP-10)

#### Scenario: Evaluación cancelada o fallida
- **WHEN** el usuario cancela la evaluación o el análisis falla
- **THEN** el sistema descarta el contenido y registra el error sin incluir el contenido (CP-10)

#### Scenario: Descarte no logrado
- **WHEN** el sistema no puede confirmar el descarte del contenido original
- **THEN** el control CT-02 queda «no aplicado» y la evaluación requiere revisión humana (CP-10)

### Requirement: DOC-09 Análisis parcial exige revisión humana
[Complementario] El sistema SHALL marcar el análisis como parcial cuando alguna parte del contenido no pueda analizarse, y la clasificación SHALL quedar «pendiente de revisión» (CLA-05).

#### Scenario: Sección no analizable
- **WHEN** un documento contiene una sección ilegible o no soportada
- **THEN** el sistema marca el análisis como parcial e indica la parte omitida

#### Scenario: Documento completamente analizable
- **WHEN** todo el contenido puede analizarse
- **THEN** el sistema no marca el análisis como parcial

#### Scenario: Contenido totalmente ilegible
- **WHEN** ninguna parte del contenido puede analizarse
- **THEN** el sistema no declara «sin indicadores detectados» y deja la clasificación pendiente de revisión

### Requirement: DOC-10 Consistencia del análisis y la clasificación
[Complementario] El sistema SHALL producir los mismos hallazgos y la misma clasificación cuando se evalúa el mismo contenido con la misma versión de reglas y configuración.

#### Scenario: Repetición de la evaluación
- **WHEN** el mismo contenido se evalúa dos veces con la misma configuración
- **THEN** ambas evaluaciones muestran los mismos hallazgos y la misma clasificación

#### Scenario: Cambio de configuración
- **WHEN** cambia la versión de reglas o configuración entre dos evaluaciones del mismo contenido
- **THEN** cada evaluación registra la versión utilizada para explicar la diferencia
