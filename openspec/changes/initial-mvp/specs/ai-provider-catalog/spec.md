# Spec Delta

## Purpose

Permite consultar las condiciones de tratamiento de información de proveedores de IA generativa mediante un catálogo con fuente y fecha de verificación, sin enviar contenido evaluado a ningún tercero. Solo el uso para mejorar modelos interviene en el resultado automático; retención, exclusión y ubicación se presentan como información para revisión humana, y el sistema no determina si una transferencia o transmisión internacional es lícita. El origen y los datos del catálogo están **pendientes de decisión** (O-04) y no constituyen una garantía del proveedor. El comportamiento cuando no se selecciona proveedor es el mismo que en `document-analysis` y `compliance-policies` (DOC-07, POL-05).

## ADDED Requirements

### Requirement: PRV-01 Entradas con fuente, fecha y condiciones
[MVP esencial] El sistema SHALL registrar cada entrada con proveedor, servicio o plan, fuente consultada, fecha de verificación, tipo de dato («verificado» o «ejemplo») y cuatro condiciones: uso del contenido para mejorar modelos o entrenarlos (sí, no o no informado), periodo de retención, posibilidad de exclusión (sí, no o no informado) y ubicación del tratamiento. Una entrada sin fuente o sin fecha SHALL rechazarse. El conjunto de condiciones es provisional (O-04).

#### Scenario: Entrada completa
- **WHEN** se registra una entrada con proveedor, las cuatro condiciones, fuente, fecha y tipo de dato
- **THEN** el sistema la guarda y queda disponible para consulta

#### Scenario: Entrada sin fuente
- **WHEN** se intenta guardar una entrada sin fuente
- **THEN** el sistema rechaza el registro e indica que la fuente es obligatoria

#### Scenario: Entrada sin fecha de verificación
- **WHEN** se intenta guardar una entrada sin fecha de verificación
- **THEN** el sistema rechaza el registro

#### Scenario: Entrada de ejemplo
- **WHEN** una entrada tiene el tipo de dato «ejemplo»
- **THEN** el sistema la muestra con la etiqueta «ejemplo» en la consulta y en el informe

### Requirement: PRV-02 Consulta de condiciones declaradas por la fuente
[MVP esencial] El sistema SHALL permitir que cualquier usuario identificado consulte las condiciones de un proveedor, presentándolas como declaradas por la fuente citada con su fecha, sin calificar al proveedor de «seguro» ni «cumplidor» y sin inferir condiciones no informadas.

#### Scenario: Proveedor registrado
- **WHEN** un usuario consulta un proveedor registrado
- **THEN** el sistema muestra sus condiciones con fuente y fecha de verificación

#### Scenario: Proveedor no registrado
- **WHEN** un usuario consulta un proveedor que no está en el catálogo
- **THEN** el sistema informa «sin información verificada» y no deduce condiciones (CP-06)

#### Scenario: Condición no informada
- **WHEN** la fuente no informa una condición
- **THEN** el sistema muestra «no informado en la fuente» y no la infiere

#### Scenario: Calificativos
- **WHEN** el sistema muestra las condiciones de un proveedor
- **THEN** no usa calificativos de seguridad o cumplimiento sobre el proveedor (CP-12)

#### Scenario: Sin determinación de licitud
- **WHEN** la ubicación declarada de un proveedor está fuera de Colombia
- **THEN** el sistema muestra la ubicación como información para revisión humana y no afirma si una transferencia o transmisión internacional es lícita o ilícita (CP-01)

### Requirement: PRV-03 Proveedor previsto opcional
[MVP esencial] El sistema SHALL permitir indicar opcionalmente el proveedor previsto e incorporar a la evaluación sus condiciones, fuente y fecha. El uso para mejorar modelos interviene en `RJ-04` (POL-04); retención, exclusión y ubicación se muestran como «información para revisión humana». Sin proveedor, SHALL registrar «evaluación de proveedor no completada» (POL-05).

#### Scenario: Con proveedor
- **WHEN** el usuario indica un proveedor registrado
- **THEN** la evaluación incluye sus condiciones, fuente y fecha (CP-01)

#### Scenario: Condiciones como información para revisión
- **WHEN** el usuario indica un proveedor registrado
- **THEN** la evaluación muestra la retención, la exclusión y la ubicación rotuladas «información para revisión humana», sin alterar el resultado automático (CP-01)

#### Scenario: Sin proveedor
- **WHEN** el usuario no indica proveedor
- **THEN** el registro dice «evaluación de proveedor no completada» y el informe dice «no evaluado» (CP-07)

#### Scenario: Proveedor no registrado
- **WHEN** el usuario indica un proveedor que no está en el catálogo
- **THEN** la evaluación lo trata como «sin información verificada» y no como «no seleccionado» (CP-06)

### Requirement: PRV-04 Información posiblemente desactualizada
[Complementario] El sistema SHALL marcar como «posiblemente desactualizada» toda entrada cuya antigüedad desde la fecha de verificación supere el periodo de vigencia configurado, y la evaluación SHALL devolver al menos «advertencia» si hay hallazgo relevante. El valor del periodo está pendiente.

#### Scenario: Entrada vencida con hallazgo relevante
- **WHEN** la antigüedad de una entrada supera el periodo y el contenido tiene un hallazgo relevante
- **THEN** la entrada se marca como posiblemente desactualizada y `RJ-04` devuelve al menos «advertencia» citando la fecha (CP-06)

#### Scenario: Entrada en el límite exacto
- **WHEN** la antigüedad de una entrada es igual al periodo de vigencia
- **THEN** el sistema no la marca como desactualizada

#### Scenario: Entrada actualizada
- **WHEN** se actualiza la fecha de verificación y la fuente de una entrada vencida
- **THEN** el sistema retira la marca de desactualización

### Requirement: PRV-05 Mantenimiento del catálogo por el Administrador
[Complementario] El sistema SHALL permitir que solo un Administrador cree, edite o retire entradas, registrando los cambios en el historial (REP-07). El MVP puede operar con entradas precargadas.

#### Scenario: Edición por un Administrador
- **WHEN** un Administrador edita una entrada
- **THEN** el sistema registra persona, fecha y valores anterior y nuevo

#### Scenario: Edición por un Trabajador
- **WHEN** un usuario con perfil Trabajador intenta editar una entrada
- **THEN** el sistema deniega la acción (CP-11)
