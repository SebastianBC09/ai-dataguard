# Spec Delta

## Purpose

Identifica indicadores de sensibilidad en el contenido y le asigna una clasificación de sensibilidad (Pública, Interna, Confidencial o Restringida) o la registra como pendiente de revisión. La clasificación describe el contenido; el resultado de riesgo, definido en `compliance-policies`, describe su uso con un proveedor, políticas y reglas. Categorías, marcas y criterios son **provisionales** (O-02) y no constituyen una calificación legal.

## ADDED Requirements

### Requirement: CLA-01 Categorías funcionales de indicadores
[MVP esencial] El sistema SHALL reconocer estas categorías: datos personales de identificación y contacto; datos personales financieros; sensibilidad alta (origen racial o étnico, orientación política, convicciones religiosas o filosóficas, pertenencia a sindicatos, organizaciones sociales o de derechos humanos, salud, vida sexual, biométricos); indicios textuales de datos de menores; información corporativa confidencial con marcas explícitas; y credenciales o secretos técnicos.

#### Scenario: Contenido con cada categoría
- **WHEN** se evalúa contenido sintético con un indicador de cada categoría
- **THEN** el sistema genera un hallazgo asociado a cada una (CP-01)

#### Scenario: Indicios de datos de menores
- **WHEN** el texto menciona expresamente a un niño, niña, adolescente o menor de edad junto con datos personales sintéticos
- **THEN** el sistema genera un hallazgo de la categoría de indicios de datos de menores, sin verificar la edad ni la autorización (CP-01)

#### Scenario: Dato sensible de la lista ampliada
- **WHEN** el texto incluye una afiliación sindical ficticia
- **THEN** el sistema genera un hallazgo de sensibilidad alta (CP-01)

#### Scenario: Información corporativa sin marca explícita
- **WHEN** el contenido describe información corporativa sin ninguna marca explícita
- **THEN** el sistema no genera hallazgo corporativo y el informe declara que esa detección se limita a marcas explícitas (CP-02)

#### Scenario: Indicador fuera de las categorías
- **WHEN** el contenido incluye información sensible de un tipo no contemplado
- **THEN** el sistema no genera hallazgo y la clasificación queda pendiente de revisión si no hay otros indicadores (CP-02)

### Requirement: CLA-02 Marcas explícitas de confidencialidad
[MVP esencial] El sistema SHALL reconocer las expresiones completas «uso interno», «confidencial», «reservado» y «restringido», sin distinguir mayúsculas, con esta correspondencia: «uso interno» da Interna; «confidencial» da Confidencial; «reservado» y «restringido» dan Restringida. La lista es provisional.

#### Scenario: Marca en mayúsculas y en minúsculas
- **WHEN** el contenido incluye «CONFIDENCIAL» en un caso y «confidencial» en otro
- **THEN** ambos generan el mismo hallazgo de nivel Confidencial

#### Scenario: Marca de uso interno
- **WHEN** el contenido incluye «USO INTERNO» y ningún otro indicador
- **THEN** el sistema genera un hallazgo de nivel Interna

#### Scenario: Palabra aislada
- **WHEN** el contenido incluye la palabra «interno» dentro de otra expresión, como «control interno»
- **THEN** el sistema no la reconoce como marca

#### Scenario: Marcas en conflicto
- **WHEN** el contenido incluye «confidencial» y «reservado»
- **THEN** el hallazgo determinante es el de mayor nivel, Restringida (CP-03)

### Requirement: CLA-03 Niveles de clasificación y estado
[MVP esencial] El sistema SHALL registrar una clasificación con uno de los niveles ordenados Pública < Interna < Confidencial < Restringida, o con el estado «pendiente de revisión» (con nivel sugerido cuando exista). El nivel es el más alto entre sus hallazgos. Un «hallazgo relevante» es el de una categoría que corresponde a Confidencial o Restringida.

#### Scenario: Hallazgos de distinto nivel
- **WHEN** la evaluación tiene hallazgos de niveles distintos
- **THEN** el nivel asignado es el más alto (CP-01)

#### Scenario: Clasificación pendiente con nivel sugerido
- **WHEN** la clasificación queda pendiente de revisión y existen hallazgos
- **THEN** el sistema muestra «pendiente de revisión» y el nivel sugerido más alto (CP-08)

#### Scenario: Clasificación pendiente sin hallazgos
- **WHEN** la clasificación queda pendiente y no hay hallazgos
- **THEN** el sistema muestra «pendiente de revisión» sin nivel sugerido (CP-02)

### Requirement: CLA-04 Criterios de asignación automática
[MVP esencial] El sistema SHALL asignar automáticamente: Restringida ante sensibilidad alta, credenciales o marcas «reservado» o «restringido»; Confidencial ante datos personales de identificación, contacto o financieros, indicios de datos de menores o marca «confidencial»; Interna solo ante marca «uso interno» sin hallazgos de nivel superior.

#### Scenario: Datos de contacto
- **WHEN** el contenido incluye un correo sintético con certeza media o alta
- **THEN** el nivel asignado es Confidencial (CP-01)

#### Scenario: Credencial sintética
- **WHEN** el contenido incluye una credencial sintética
- **THEN** el nivel asignado es Restringida (CP-01)

#### Scenario: Indicios de datos de menores
- **WHEN** el contenido incluye indicios de datos de menores y ningún indicador de nivel superior
- **THEN** el nivel asignado es al menos Confidencial (CP-01)

#### Scenario: Marca reservado
- **WHEN** el contenido incluye la marca «reservado»
- **THEN** el nivel asignado es Restringida (CP-03)

#### Scenario: Uso interno con un dato de nivel superior
- **WHEN** el contenido incluye «uso interno» y un correo sintético
- **THEN** el nivel asignado es Confidencial y no Interna (CP-03)

### Requirement: CLA-05 Clasificación pendiente por información insuficiente (control CT-05)
[MVP esencial] El sistema SHALL registrar la clasificación como «pendiente de revisión» y SHALL NOT asignar «Pública» cuando no haya hallazgos ni marcas, el análisis sea parcial, algún hallazgo tenga certeza baja o los hallazgos se contradigan.

#### Scenario: Sin hallazgos ni marcas
- **WHEN** el contenido no tiene hallazgos ni marcas
- **THEN** la clasificación es «pendiente de revisión» y no Pública (CP-02)

#### Scenario: Texto que se declara público
- **WHEN** el contenido incluye la frase «documento público» y ningún otro indicador
- **THEN** la clasificación sigue pendiente de revisión

#### Scenario: Hallazgo de certeza baja
- **WHEN** un hallazgo tiene certeza baja
- **THEN** la clasificación es «pendiente de revisión» con nivel sugerido (CP-08)

#### Scenario: Hallazgos en contradicción
- **WHEN** dos hallazgos sugieren tipos distintos para el mismo fragmento
- **THEN** la clasificación es «pendiente de revisión» con el nivel sugerido más alto

### Requirement: CLA-06 Resolución humana de la clasificación
[MVP esencial] El sistema SHALL permitir que un Revisor (el Administrador en su función de revisión de cumplimiento) asigne o ajuste el nivel solo con una justificación. «Pública» SHALL asignarse únicamente así. Se conservan el nivel automático o sugerido y el humano.

#### Scenario: Asignar Pública con justificación
- **WHEN** un Revisor asigna Pública a una clasificación pendiente e ingresa justificación
- **THEN** el sistema registra ambos niveles, la justificación, la persona y la fecha (CP-08)

#### Scenario: Ajuste sin justificación
- **WHEN** un Revisor intenta asignar o ajustar el nivel sin justificación
- **THEN** el sistema rechaza el cambio

#### Scenario: Ajuste por un Trabajador
- **WHEN** un usuario con perfil Trabajador intenta asignar o ajustar el nivel
- **THEN** el sistema deniega la acción (CP-11)

#### Scenario: Reducción del nivel automático
- **WHEN** un Revisor baja una clasificación de Confidencial a Interna con justificación
- **THEN** el sistema acepta el cambio, conserva el nivel automático y lo registra en el historial (CP-08)

### Requirement: CLA-07 Explicación de la clasificación
[MVP esencial] El sistema SHALL presentar la clasificación junto con los hallazgos y marcas que la determinan y el motivo de cada uno.

#### Scenario: Nivel Restringida
- **WHEN** el nivel asignado es Restringida
- **THEN** el resultado muestra el hallazgo o la marca determinante y su motivo (CP-03)

#### Scenario: Clasificación pendiente
- **WHEN** la clasificación está pendiente de revisión
- **THEN** el resultado indica cuál de los motivos de CLA-05 la originó (CP-08)

#### Scenario: Pendiente sin hallazgos
- **WHEN** la clasificación está pendiente porque no hay hallazgos ni marcas
- **THEN** el resultado indica ese motivo y no inventa hallazgos determinantes (CP-02)

### Requirement: CLA-08 Clasificación independiente del resultado de riesgo
[MVP esencial] El sistema SHALL calcular la clasificación solo a partir del contenido, y cambiar el proveedor, las políticas o las reglas SHALL NOT modificarla. La clasificación y el resultado de riesgo SHALL mostrarse como campos separados.

#### Scenario: Mismo contenido con dos proveedores
- **WHEN** el mismo contenido se evalúa con dos proveedores de condiciones distintas
- **THEN** la clasificación es la misma y el resultado de riesgo puede diferir (CP-01, CP-07)

#### Scenario: Activación de una política
- **WHEN** un Administrador activa una política y se vuelve a someter el mismo contenido
- **THEN** la clasificación no cambia aunque cambie el resultado de riesgo (CP-05)

#### Scenario: Presentación separada
- **WHEN** se muestra el resultado de una evaluación
- **THEN** la clasificación de sensibilidad y el resultado de riesgo aparecen como campos distintos (CP-12)
