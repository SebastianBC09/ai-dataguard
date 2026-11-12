# Spec Delta

## Purpose

Genera informes de cada evaluación, conserva un registro mínimo de evaluaciones y decisiones humanas y garantiza la trazabilidad sin guardar el contenido original. El seguimiento de compromisos (C5) **no** está incluido y queda como decisión abierta; el registro de decisiones humanas sí lo está.

## ADDED Requirements

### Requirement: REP-01 Informe por evaluación
[MVP esencial] El sistema SHALL generar por evaluación un informe con: identificador, fecha, usuario y perfil, clasificación de sensibilidad, resultado de riesgo global, hallazgos explicados y enmascarados, resultados por regla jurídica, política y control (con estado de validación), estado de la evaluación del proveedor y sus condiciones (las que no intervienen, como información para revisión humana), versiones aplicadas, recomendaciones de precaución y decisión humana si existe.

#### Scenario: Informe de evaluación completa
- **WHEN** finaliza una evaluación con proveedor seleccionado
- **THEN** el informe contiene todos los elementos indicados (CP-12)

#### Scenario: Evaluación sin proveedor
- **WHEN** la evaluación no tuvo proveedor
- **THEN** el informe dice «evaluación de proveedor no completada» (CP-07)

#### Scenario: Condiciones del proveedor en el informe
- **WHEN** la evaluación tuvo proveedor registrado
- **THEN** el informe muestra retención, exclusión y ubicación como «información para revisión humana» (CP-12)

#### Scenario: Clasificación pendiente
- **WHEN** la clasificación está pendiente de revisión
- **THEN** el informe muestra «pendiente de revisión» y el nivel sugerido si existe, no un nivel asignado (CP-08)

#### Scenario: Evaluación pendiente de revisión
- **WHEN** la evaluación no tiene decisión humana
- **THEN** el informe muestra el estado «pendiente de revisión» y no la presenta como cerrada

### Requirement: REP-02 Aviso de no autorización en resultados e informes
[MVP esencial] El sistema SHALL mostrar en toda pantalla de resultado y en todo informe, incluso sin hallazgos, el aviso de que es apoyo a la revisión humana, no certificación ni asesoría jurídica, y de que la ausencia de alertas no autoriza divulgar. El sistema SHALL NOT emitir recomendaciones de divulgación.

#### Scenario: Resultado sin hallazgos
- **WHEN** la evaluación no produce hallazgos
- **THEN** el resultado y el informe incluyen el aviso y declaran que la detección corporativa se limita a marcas explícitas (CP-02)

#### Scenario: Resultado con hallazgos o parcial
- **WHEN** la evaluación produce hallazgos o es parcial
- **THEN** el resultado y el informe incluyen el mismo aviso (CP-12)

#### Scenario: Ausencia de recomendaciones de divulgación
- **WHEN** se revisan los textos de resultado e informe
- **THEN** no hay frases que recomienden divulgar o indiquen que el contenido «puede enviarse» (CP-12)

### Requirement: REP-03 Informe y registro sin contenido original (control CT-04)
[MVP esencial] El sistema SHALL NOT incluir en el informe ni en el registro el contenido original evaluado ni valores sensibles completos.

#### Scenario: Documento con múltiples datos personales sintéticos
- **WHEN** se genera el informe de un documento con muchos datos personales sintéticos
- **THEN** el informe no contiene ningún valor completo (CP-12)

#### Scenario: Búsqueda del contenido en el registro
- **WHEN** se busca en el registro persistente una frase del documento evaluado
- **THEN** no se encuentra ninguna coincidencia (CP-10)

### Requirement: REP-04 Exportación del informe
[MVP esencial] El sistema SHALL permitir exportar el informe a un formato legible fuera de la aplicación, solo al autor de la evaluación y a los Revisores.

#### Scenario: Exportación por el autor
- **WHEN** el autor exporta el informe de su evaluación
- **THEN** el sistema entrega el archivo (CP-12)

#### Scenario: Exportación por un Revisor
- **WHEN** un Revisor exporta el informe de una evaluación ajena
- **THEN** el sistema entrega el archivo

#### Scenario: Exportación por un usuario ajeno
- **WHEN** un Trabajador intenta exportar el informe de otro Trabajador
- **THEN** el sistema deniega la acción (CP-11)

### Requirement: REP-05 Registro mínimo de evaluaciones
[MVP esencial] El sistema SHALL persistir por evaluación únicamente: identificador, fecha, usuario, clasificación, resultado global, tipos, cantidad y ubicación de hallazgos, resultados por regla y estado de los controles, versiones de reglas y políticas, proveedor y estado de su evaluación, estado y decisión humana. La lista definitiva está pendiente (O-06).

#### Scenario: Evaluación registrada
- **WHEN** finaliza una evaluación
- **THEN** el registro contiene esos datos y ningún valor sensible detectado (CP-10)

#### Scenario: Evaluación sin proveedor
- **WHEN** la evaluación no tuvo proveedor
- **THEN** el registro contiene «evaluación de proveedor no completada» y `RJ-04` como «no evaluada» (CP-07)

#### Scenario: Evaluación con fallo
- **WHEN** una evaluación falla
- **THEN** se registra el fallo sin contenido del documento

#### Scenario: Cambio posterior de una política
- **WHEN** un Administrador modifica una política después de una evaluación
- **THEN** la evaluación anterior conserva la versión que se aplicó entonces

### Requirement: REP-06 Decisión humana ante revisión (control CT-05)
[MVP esencial] El sistema SHALL mantener la evaluación «pendiente de revisión» mientras el resultado global sea «requiere revisión humana», la clasificación esté pendiente o un control esté «no aplicado», hasta que un Revisor registre una decisión (proceder, proceder con ajustes o no proceder) con justificación, persona y fecha.

#### Scenario: Caso que requiere revisión
- **WHEN** el resultado global es «requiere revisión humana»
- **THEN** el estado es «pendiente de revisión» hasta que se registre una decisión (CP-08)

#### Scenario: Sin recomendación mientras está pendiente
- **WHEN** la evaluación está «pendiente de revisión»
- **THEN** ni el resultado ni el informe contienen una recomendación de divulgación (CP-08)

#### Scenario: Decisión justificada
- **WHEN** un Revisor elige una decisión e ingresa justificación
- **THEN** el sistema la registra con persona y fecha y el estado cambia a «revisada» (CP-08)

#### Scenario: Decisión sin justificación
- **WHEN** un Revisor intenta registrar una decisión sin justificación
- **THEN** el sistema rechaza el registro

#### Scenario: Decisión por un Trabajador
- **WHEN** un Trabajador intenta registrar una decisión de revisión
- **THEN** el sistema deniega la acción (CP-11)

### Requirement: REP-07 Historial que no se sobrescribe (control CT-06)
[MVP esencial] El sistema SHALL conservar el historial de decisiones, ajustes de clasificación y cambios de políticas y del catálogo añadiendo entradas nuevas con qué cambió, quién y cuándo, sin sobrescribir ni borrar las anteriores mediante funciones normales.

#### Scenario: Corrección de una decisión
- **WHEN** un Revisor corrige una decisión anterior
- **THEN** el sistema añade una entrada nueva y conserva la original con su fecha y autor (CP-13)

#### Scenario: Cambio de política
- **WHEN** un Administrador activa o desactiva una política
- **THEN** el historial registra qué cambió, quién y cuándo (CP-05)

#### Scenario: Intento de eliminar una entrada
- **WHEN** cualquier usuario intenta eliminar una entrada del historial desde la aplicación
- **THEN** el sistema no ofrece esa acción o la rechaza (CP-13)

### Requirement: REP-08 Consulta de trazabilidad según perfil
[MVP esencial] El sistema SHALL permitir que el Administrador liste todas las evaluaciones y las filtre por estado, y que un Trabajador consulte solo las propias.

#### Scenario: Filtro por estado
- **WHEN** un Administrador filtra por el estado «pendiente de revisión»
- **THEN** el sistema muestra solo las evaluaciones en ese estado (CP-08)

#### Scenario: Consulta por un Trabajador
- **WHEN** un Trabajador consulta el registro
- **THEN** solo ve sus propias evaluaciones (CP-11)

#### Scenario: Consulta sin resultados
- **WHEN** ninguna evaluación coincide con el filtro
- **THEN** el sistema informa que no hay resultados

### Requirement: REP-09 Registro de exportaciones
[Complementario] El sistema SHALL registrar cada exportación de informe con persona y fecha, sin contenido del informe.

#### Scenario: Exportación registrada
- **WHEN** un usuario exporta un informe
- **THEN** el historial añade una entrada con persona y fecha de la exportación

#### Scenario: Exportación denegada
- **WHEN** se deniega una exportación por permisos
- **THEN** el historial no registra una exportación exitosa
