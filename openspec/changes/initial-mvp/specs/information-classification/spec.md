# Spec Delta

## Purpose

Identifica indicadores de sensibilidad en el contenido analizado y le asigna un nivel de clasificación explicable. Las categorías y niveles son **provisionales** (O-02) y su equivalencia jurídica queda pendiente de E2; no constituyen una calificación legal.

## ADDED Requirements

### Requirement: Categorías funcionales de indicadores
El sistema SHALL reconocer como mínimo estas categorías: datos personales de identificación y contacto, datos personales financieros, indicadores de sensibilidad alta, información corporativa confidencial, y credenciales o secretos técnicos. La equivalencia jurídica de cada categoría está pendiente de E2.

#### Scenario: Contenido con cada categoría
- **WHEN** se analiza contenido sintético que incluye un indicador de cada categoría
- **THEN** el sistema genera un hallazgo asociado a cada una (CP-01, CP-03)

#### Scenario: Indicador fuera de las categorías soportadas
- **WHEN** el contenido incluye información sensible de un tipo no contemplado
- **THEN** el sistema no genera hallazgo y mantiene la advertencia de que la ausencia de alertas no es autorización

### Requirement: Marcas explícitas de confidencialidad
El sistema SHALL tratar como indicador las marcas explícitas de confidencialidad que aparezcan en el contenido, sin distinguir mayúsculas de minúsculas.

#### Scenario: Marca en mayúsculas
- **WHEN** el contenido incluye la marca "CONFIDENCIAL"
- **THEN** el sistema genera un hallazgo de información corporativa confidencial

#### Scenario: Marca en minúsculas
- **WHEN** el contenido incluye la misma marca en minúsculas
- **THEN** el sistema genera el mismo hallazgo

### Requirement: Niveles de clasificación provisionales
El sistema SHALL asignar a cada evaluación uno de estos niveles, ordenados de menor a mayor: "Sin indicadores detectados", "Interno", "Confidencial" y "Restringido". Los nombres son provisionales (O-02).

#### Scenario: Sin hallazgos
- **WHEN** la evaluación no tiene hallazgos y no es parcial
- **THEN** el nivel asignado es "Sin indicadores detectados" (CP-02)

#### Scenario: Hallazgos de distinto nivel
- **WHEN** la evaluación tiene hallazgos que corresponden a distintos niveles
- **THEN** el nivel asignado es el más alto de ellos

### Requirement: Regla provisional de asignación de nivel
El sistema SHALL asignar al menos el nivel "Confidencial" ante datos personales de identificación, contacto o financieros, o información corporativa confidencial, y el nivel "Restringido" ante indicadores de sensibilidad alta o credenciales.

#### Scenario: Datos de contacto
- **WHEN** el contenido incluye datos personales de contacto sintéticos
- **THEN** el nivel asignado es al menos "Confidencial" (CP-01)

#### Scenario: Credencial sintética
- **WHEN** el contenido incluye una credencial sintética
- **THEN** el nivel asignado es "Restringido"

#### Scenario: Información corporativa confidencial
- **WHEN** el contenido incluye información corporativa confidencial sintética
- **THEN** el nivel asignado es al menos "Confidencial" (CP-03)

### Requirement: Explicación de la clasificación
El sistema SHALL presentar el nivel asignado junto con los hallazgos que lo determinan y el motivo de cada uno.

#### Scenario: Nivel Restringido
- **WHEN** el nivel asignado es "Restringido"
- **THEN** el resultado muestra el hallazgo determinante y su motivo

#### Scenario: Consulta del porqué
- **WHEN** el usuario consulta por qué se asignó un nivel
- **THEN** el sistema lista los hallazgos y el criterio aplicado

### Requirement: Certeza baja exige revisión humana
El sistema SHALL marcar la evaluación como "requiere revisión humana" cuando exista un hallazgo de certeza baja o hallazgos en conflicto, y no SHALL reducir el nivel por esa incertidumbre.

#### Scenario: Hallazgo de certeza baja
- **WHEN** un hallazgo tiene certeza baja
- **THEN** la evaluación se marca "requiere revisión humana" y el nivel considera la categoría como si se confirmara (CP-07)

#### Scenario: Hallazgos en conflicto
- **WHEN** dos hallazgos sugieren niveles distintos para el mismo fragmento
- **THEN** el sistema asigna el nivel más alto y exige revisión humana

#### Scenario: Único hallazgo de certeza baja
- **WHEN** el único hallazgo tiene certeza baja
- **THEN** el sistema no asigna "Sin indicadores detectados"

### Requirement: Ajuste humano del nivel con justificación
El sistema SHALL permitir que un Revisor (Administrador o Responsable de cumplimiento, ver O-01) ajuste el nivel asignado solo con una justificación, conservando el nivel original y el ajustado.

#### Scenario: Ajuste justificado
- **WHEN** un Revisor ajusta el nivel e ingresa una justificación
- **THEN** el sistema registra ambos niveles, la justificación, la persona y la fecha

#### Scenario: Ajuste sin justificación
- **WHEN** un Revisor intenta ajustar el nivel sin justificación
- **THEN** el sistema rechaza el ajuste

#### Scenario: Ajuste por un Trabajador
- **WHEN** un usuario con perfil Trabajador intenta ajustar el nivel
- **THEN** el sistema deniega la acción (CP-09)

### Requirement: Sin indicadores no equivale a información pública o segura
El sistema SHALL NOT presentar el nivel "Sin indicadores detectados" con términos como "público", "seguro", "aprobado" o "autorizado".

#### Scenario: Resultado sin indicadores
- **WHEN** el nivel asignado es "Sin indicadores detectados"
- **THEN** el resultado no usa esos términos y muestra la advertencia de ausencia de alertas (CP-02)

### Requirement: Consistencia de la clasificación
El sistema SHALL asignar el mismo nivel ante los mismos hallazgos y la misma versión de reglas de clasificación.

#### Scenario: Mismos hallazgos
- **WHEN** dos evaluaciones tienen los mismos hallazgos y la misma versión de reglas
- **THEN** ambas reciben el mismo nivel
