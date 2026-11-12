# Spec Delta

## Purpose

Genera informes de cada evaluación, conserva un registro mínimo de evaluaciones y decisiones humanas, y garantiza la trazabilidad sin guardar el contenido original. El seguimiento de compromisos (C5) **no** está incluido y queda como decisión abierta.

## ADDED Requirements

### Requirement: Informe por evaluación
El sistema SHALL generar un informe por evaluación que incluya identificador, fecha, usuario y perfil, nivel de clasificación, hallazgos explicados, resultados por regla y política con su estado de validación, proveedor consultado, versiones aplicadas, recomendaciones y decisión humana si existe.

#### Scenario: Informe de evaluación completa
- **WHEN** finaliza una evaluación
- **THEN** el sistema genera un informe con todos los elementos indicados (CP-10)

#### Scenario: Evaluación sin proveedor
- **WHEN** la evaluación no tuvo proveedor indicado
- **THEN** el informe indica "no se evaluaron condiciones de proveedor"

#### Scenario: Evaluación pendiente de revisión
- **WHEN** la evaluación no tiene decisión humana
- **THEN** el informe muestra el estado "pendiente de revisión" y no la presenta como cerrada

### Requirement: Advertencia obligatoria en todo informe
El sistema SHALL incluir en cada informe la advertencia de que es un apoyo a la revisión humana, que no constituye certificación ni asesoría jurídica, y que la ausencia de alertas no autoriza divulgar información.

#### Scenario: Informe con alertas
- **WHEN** se genera un informe con alertas
- **THEN** incluye la advertencia (CP-10)

#### Scenario: Informe sin alertas
- **WHEN** se genera un informe sin alertas
- **THEN** incluye la misma advertencia

### Requirement: Informe sin contenido original
El sistema SHALL NOT incluir en el informe ni en el registro el contenido original evaluado; los fragmentos mostrados SHALL estar enmascarados.

#### Scenario: Documento con múltiples datos personales sintéticos
- **WHEN** se genera el informe de un documento con muchos datos personales sintéticos
- **THEN** el informe no contiene ningún valor completo y muestra solo fragmentos enmascarados (CP-10)

#### Scenario: Búsqueda del contenido en el registro
- **WHEN** se busca en el registro persistente una frase del documento evaluado
- **THEN** no se encuentra ninguna coincidencia (CP-08)

### Requirement: Exportación del informe
El sistema SHALL permitir exportar el informe a un formato legible sin acceso a la aplicación, solo a su autor y a los Revisores, y SHALL registrar cada exportación.

#### Scenario: Exportación por el autor
- **WHEN** el autor de la evaluación exporta su informe
- **THEN** el sistema entrega el archivo y registra persona y fecha de la exportación (CP-10)

#### Scenario: Exportación por un usuario ajeno
- **WHEN** un Trabajador intenta exportar el informe de otro Trabajador
- **THEN** el sistema deniega la acción (CP-09)

### Requirement: Registro mínimo de evaluaciones
El sistema SHALL persistir por evaluación únicamente: identificador, fecha, usuario, nivel, resultado global, tipos y cantidad de hallazgos con ubicación aproximada, reglas y versiones, proveedor, estado y decisión humana. La lista definitiva está pendiente (O-06).

#### Scenario: Evaluación registrada
- **WHEN** finaliza una evaluación
- **THEN** el registro contiene esos datos y ningún valor sensible detectado

#### Scenario: Evaluación con fallo
- **WHEN** una evaluación falla
- **THEN** se registra el fallo sin contenido del documento

### Requirement: Decisión humana obligatoria ante revisión
El sistema SHALL mantener la evaluación en estado "pendiente de revisión" hasta que un Revisor registre una decisión cuando el resultado global sea "requiere revisión humana".

#### Scenario: Caso que requiere revisión
- **WHEN** el resultado global es "requiere revisión humana"
- **THEN** el estado es "pendiente de revisión" hasta que se registre una decisión (CP-07)

#### Scenario: Registro de decisión
- **WHEN** un Revisor registra una decisión
- **THEN** el estado cambia a "revisada"

### Requirement: Contenido de la decisión humana
El sistema SHALL exigir que cada decisión humana se elija entre "proceder", "proceder con ajustes" y "no proceder", e incluya una justificación, la persona y la fecha. Estas opciones son una propuesta pendiente.

#### Scenario: Decisión justificada
- **WHEN** un Revisor elige una decisión e ingresa justificación
- **THEN** el sistema la registra con persona y fecha (CP-07)

#### Scenario: Decisión sin justificación
- **WHEN** un Revisor intenta registrar una decisión sin justificación
- **THEN** el sistema rechaza el registro

#### Scenario: Decisión por un Trabajador
- **WHEN** un Trabajador intenta registrar una decisión de revisión
- **THEN** el sistema deniega la acción (CP-09)

### Requirement: Historial que no se sobrescribe
El sistema SHALL conservar el historial de decisiones, ajustes y cambios de políticas añadiendo nuevas entradas, sin sobrescribir ni borrar las anteriores mediante funciones normales.

#### Scenario: Corrección de una decisión
- **WHEN** un Revisor corrige una decisión anterior
- **THEN** el sistema añade una entrada nueva y conserva la original con su fecha y autor

#### Scenario: Intento de eliminar una entrada
- **WHEN** cualquier usuario intenta eliminar una entrada del historial desde la aplicación
- **THEN** el sistema no ofrece esa acción o la rechaza (CP-10)

### Requirement: Consulta de la trazabilidad según perfil
El sistema SHALL permitir que Administrador y Responsable de cumplimiento consulten evaluaciones por fecha, usuario, nivel, resultado y estado, y que un Trabajador consulte solo las propias.

#### Scenario: Consulta por un Administrador
- **WHEN** un Administrador filtra las evaluaciones por nivel y estado
- **THEN** el sistema muestra solo las que coinciden con ambos filtros

#### Scenario: Consulta por un Trabajador
- **WHEN** un Trabajador consulta el registro
- **THEN** solo ve sus propias evaluaciones (CP-09)

#### Scenario: Consulta sin resultados
- **WHEN** ningún registro coincide con los filtros
- **THEN** el sistema informa que no hay resultados

### Requirement: Retención configurable del registro
El sistema SHALL permitir configurar un periodo de retención del registro de evaluaciones y SHALL señalar los registros que lo superen. El valor y el tratamiento posterior están pendientes de decisión (O-06) y de revisión jurídica.

#### Scenario: Registro vencido
- **WHEN** la antigüedad de un registro supera el periodo configurado
- **THEN** el sistema lo señala como vencido para su revisión

#### Scenario: Registro en el límite exacto
- **WHEN** la antigüedad de un registro es igual al periodo configurado
- **THEN** el sistema no lo señala como vencido

### Requirement: Datos de ejemplo sintéticos
El sistema SHALL operar en la demostración y en las pruebas con datos de ejemplo sintéticos, sin datos personales reales ni contraseñas visibles.

#### Scenario: Conjunto de datos de demostración
- **WHEN** se revisa el conjunto de datos de ejemplo
- **THEN** todo dato personal está marcado como sintético y no corresponde a una persona real
