# Plan de pruebas preliminar: AI DataGuard (MVP)

**Etapa:** plan de pruebas v0 (E3, tarea 3.4), previo a la ejecución de E6 · Contexto Legal de la Ingeniería · UNINPAHU
**Fecha de elaboración:** 12 de noviembre de 2026
**Estado: BORRADOR PRELIMINAR, PENDIENTE DE REVISIÓN DEL EQUIPO Y DE APROBACIÓN DOCENTE.** Este documento es un **plan**, no un informe de pruebas. **Ninguna prueba ha sido ejecutada**: no existen resultados, evidencias ni defectos reales. E1 y E2 no están aprobadas; el MVP no está implementado.

*Convención:* **[Docente]** = requisito expreso de la guía docente; **[Equipo]** = propuesta del equipo. Las pruebas conservan los identificadores `CP-01` a `CP-13`, de `design.md`.

## 1. Objetivo y alcance

**Objetivo.** Definir cómo se comprobará, durante E6, que el MVP cumple los requisitos de las cinco capacidades (`document-analysis`, `information-classification`, `compliance-policies`, `ai-provider-catalog`, `assessment-reports`) y las salvaguardas de privacidad y minimización, con procedimientos que los integrantes puedan ejecutar y documentar.

**Mínimos del docente** [Docente]: al menos 10 pruebas con evidencias, defectos registrados, revisión de las 5 reglas y 3 escenarios de demostración. Aquí hay **13 casos previstos**: 10 mínimos y 3 adicionales.

**Dentro del alcance:**
- Los 43 requisitos de las specs, con prioridad en los 37 esenciales (los complementarios solo si se implementan).
- El recorrido de evaluación de principio a fin con datos sintéticos.
- Los tres escenarios de demostración (`ED-1` a `ED-3`).

**Fuera del alcance:**
- La corrección jurídica de las reglas `RJ-01` a `RJ-05`. Las pruebas verifican que el sistema se comporte como las specs describen, no que esa regla sea jurídicamente válida; eso corresponde a E2.
- Rendimiento y carga: las specs no definen requisitos medibles.
- Usabilidad y accesibilidad: no están especificadas.
- Pruebas de intrusión o seguridad avanzada.
- Cualquier tecnología concreta: el plan no depende del stack (C3).

## 2. Estrategia de validación

Las pruebas son manuales y se ejecutan sobre el MVP con datos sintéticos. No se exige infraestructura compleja.

| Tipo | Qué se valida | Casos | Cómo |
|---|---|---|---|
| **Funcional** | Detección, clasificación, evaluación de reglas, catálogo, informe | CP-01, 02, 03, 04, 05, 06, 07, 08, 12 | Procedimientos guiados con resultados observables |
| **Seguridad** | Permisos por perfil; no salida del contenido | CP-11, CP-09 | Intentos de acciones no permitidas; ejecución con conexiones externas bloqueadas |
| **Privacidad y minimización** | No transmisión, descarte del original, enmascarado, informe sin contenido | CP-09, CP-10, CP-12 | Ejecución sin red; revisión del registro persistido; revisión de valores mostrados |
| **Trazabilidad y revisión humana** | Estado de la evaluación, decisión justificada, historial que no se sobrescribe | CP-05, CP-07, CP-08, CP-13 | Revisión de estados, filtros y entradas del historial |
| **Explicabilidad** | Motivo de cada hallazgo, clasificación y resultado | CP-01, CP-02, CP-03, CP-12 | Comprobación de los campos explicativos |

**Principios** [Equipo]:
- **Una verificación principal por caso**, con pasos adicionales solo si usan los mismos datos. Los antiguos casos que agrupaban demasiado se dividieron.
- **Resultado esperado derivado de las specs.** No se modifica un resultado esperado para que coincida con lo observado (sección 9).
- **Requisitos no funcionales sin caso propio:** consistencia (`DOC-10`) y rendimiento no tienen prueba; la consistencia puede comprobarse repitiendo `CP-01`, solo si se implementa.

## 3. Condiciones y criterios de entrada y salida

**Entrada.** Todas deben cumplirse antes de iniciar E6:

| # | Condición | Origen |
|---|---|---|
| E-1 | Recorrido principal de E5 funcionando con datos nuevos | [Docente] |
| E-2 | E1 y E2 aprobadas por el docente, o los casos que dependen de las reglas marcados «provisional» | [Equipo] |
| E-3 | Decisión del stack (C3) registrada y aprobada | [Equipo] |
| E-4 | Plan de pruebas v1 cerrado (tarea 4.7), con resultados esperados fijados | [Equipo] |
| E-5 | Datos sintéticos de la sección 6 preparados y revisados por una segunda persona | [Equipo] |
| E-6 | Posibilidad de ejecutar la aplicación con las conexiones externas bloqueadas | [Equipo] |
| E-7 | Usuarios de prueba creados (sección 6) | [Equipo] |
| E-8 | Responsables de ejecución y revisión asignados (tarea 4.6) | [Equipo] |

**Salida:**

| # | Condición | Origen |
|---|---|---|
| S-1 | Los 10 casos mínimos ejecutados, cada uno con evidencia real | [Docente] |
| S-2 | Funciones obligatorias aprobadas; defectos listados | [Docente] |
| S-3 | Cada `RJ` aprobada en E2 relacionada con requisitos y pruebas (tarea 6.2) | [Docente] |
| S-4 | Ningún defecto de severidad crítica abierto en los casos de privacidad y seguridad (`CP-09`, `CP-10`, `CP-11`) | [Equipo] |
| S-5 | Casos fallidos o bloqueados registrados, sin alterar los resultados esperados | [Equipo] |

Los 3 casos adicionales (`CP-04`, `CP-06`, `CP-13`) no son requisito de salida y se ejecutan si el plazo lo permite.

## 4. Casos de prueba previstos

**Estado de los trece casos: PREVISTO, NO EJECUTADO.** La columna «Resultado real» no existe en este plan; se registra en el acta de ejecución (sección 8).

**Notación.** US-T1 y US-T2: usuarios con perfil Trabajador. US-ADM: usuario con perfil Administrador, que actúa como Revisor (E1: dos perfiles). Datos `DS-xx`, proveedores `PF-x`, políticas `PO-xx`: sección 6. «Esperado» incluye la referencia al requisito entre paréntesis. **Todos los resultados esperados son provisionales** hasta E2 y hasta resolver las dependencias de cada caso (sección 11).

### CP-01. Datos personales con proveedor que usa el contenido para mejorar modelos

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional y explicabilidad · Mínimo |
| Capacidades | 1, 2, 3, 4 |
| Requisitos | DOC-01, DOC-02, DOC-05, DOC-07, CLA-01, CLA-03, CLA-04, CLA-08, POL-03, POL-04, POL-08, PRV-03 |
| Reglas | `RJ-01`, `RJ-04` (provisionales) |
| Dependencias abiertas | O-02 (criterios), O-04 (condiciones del proveedor), O-05, E2 |
| Datos y precondiciones | DS-01, DS-01b y DS-07; PF-A en el catálogo; US-T1 identificado |
| Procedimiento | 1. US-T1 somete DS-01 y selecciona PF-A. 2. Observar la lista de hallazgos, la clasificación y el resultado por regla. 3. Observar el estado de la evaluación. 4. Repetir con DS-01b y PF-A. 5. Someter DS-07 sin proveedor y listar los hallazgos por categoría, el nivel asignado y el resultado de `RJ-01`. 6. Con PF-A, revisar cómo se muestran la retención, la exclusión y la ubicación. |
| Esperado | 1. El correo y el documento con etiqueta aparecen con tipo, línea, certeza **alta** y motivo (DOC-05). 2. Con DS-01b, el correo tiene certeza **media** (DOC-05). 3. Clasificación **Confidencial** (CLA-04, CLA-03). 4. `RJ-01` «advertencia» (POL-03). 5. `RJ-04` «requiere revisión humana», citando la condición, la fuente y la fecha de PF-A (POL-04, PRV-03). 6. Resultado global «requiere revisión humana»; estado «pendiente de revisión». 7. Las reglas provisionales muestran la marca «regla provisional» (POL-08). 8. La evaluación registra usuario y perfil (DOC-01). 9. Los hallazgos son los mismos que en `CP-07` y la clasificación es la misma (DOC-07, CLA-08). 10. Con DS-07 hay un hallazgo por cada categoría de DS-07 (CLA-01); la credencial y el dato de sensibilidad alta dan Restringida y el indicio de menores da al menos Confidencial (CLA-04). 11. Con DS-07, `RJ-01` devuelve «requiere revisión humana» con una advertencia reforzada que indica que el tratamiento de esos datos tiene reglas especiales y que el sistema no verifica autorizaciones, sin afirmar una prohibición (POL-03). 12. Con PF-A, la retención, la exclusión y la ubicación aparecen rotuladas «información para revisión humana», no alteran el resultado de `RJ-04` y el sistema no dice si una transferencia o transmisión es lícita (PRV-03, POL-04). |
| Evidencia | Capturas de hallazgos, clasificación, resultados y estado; acta de ejecución. |
| Estado | **No ejecutado** |

### CP-02. Contenido sin indicadores

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional · Mínimo · Negativo / falso negativo |
| Capacidades | 1, 2, 3, 5 |
| Requisitos | DOC-05, CLA-01, CLA-03, CLA-05, CLA-07, POL-03, POL-07, POL-08, REP-02 |
| Reglas | `RJ-01`, `RJ-02`, `RJ-05` |
| Dependencias abiertas | O-02, O-05, E2 |
| Datos y precondiciones | DS-02, DS-02b y DS-02c; PF-B; política PO-01 activa que no coincide con el contenido; US-T1 |
| Procedimiento | 1. US-T1 somete DS-02 con PF-B. 2. Observar hallazgos, clasificación, resultado por regla, estado, avisos y estado de los controles. 3. Repetir con DS-02b. 4. US-ADM (Revisor) asigna «Pública» a la clasificación pendiente de DS-02, primero sin justificación y luego con justificación. 5. Someter DS-02c con PF-B y revisar el informe. |
| Esperado | 1. Lista de hallazgos vacía y resultado de detección «sin indicadores detectados» (DOC-05). 2. Clasificación «pendiente de revisión», **sin nivel sugerido y no Pública** (CLA-05, CLA-03). Con DS-02b también (la frase «documento público» no basta). 3. `RJ-01`, `RJ-02` y `RJ-04` «sin alerta»; `RJ-03` evaluada; resultado global «sin alerta» (POL-03, POL-06). 4. Estado «pendiente de revisión» por la clasificación (REP-06). 5. Aviso de que la ausencia de alertas no autoriza divulgar y declaración de que la detección corporativa se limita a marcas (REP-02, CLA-01). 6. El resultado indica el motivo de la clasificación pendiente (CLA-07). 7. Controles CT-01 a CT-05 visibles, independientemente de los hallazgos (POL-07). 8. Ningún texto usa «público», «seguro», «aprobado» ni «autorizado» asociado al nivel. 9. La asignación sin justificación se rechaza; con justificación se registra el nivel humano y el automático (CLA-06). 10. Con DS-02c no hay hallazgo corporativo y el informe declara que esa detección se limita a marcas explícitas (CLA-01, REP-02). |
| Evidencia | Capturas de resultado, avisos y clasificación; acta. |
| Estado | **No ejecutado** |

### CP-03. Marca «reservado»

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional · Mínimo |
| Capacidades | 1, 2, 3 |
| Requisitos | DOC-05, CLA-02, CLA-04, CLA-07, POL-03 |
| Reglas | `RJ-02` |
| Dependencias abiertas | O-02 (lista de marcas), E2 |
| Datos y precondiciones | DS-03, DS-03b, DS-03c y DS-04b; PF-B; US-T1 |
| Procedimiento | 1. US-T1 somete DS-03 con PF-B. 2. Observar clasificación, `RJ-02` y la explicación. 3. Repetir con DS-03b (marcas en conflicto). 4. Con DS-03c, comprobar cada variante: mayúsculas, minúsculas y la expresión «control interno». 5. Con DS-04b (marca «uso interno» más un correo), observar el nivel. |
| Esperado | 1. Clasificación **Restringida** (CLA-04). 2. `RJ-02` «requiere revisión humana» (POL-03). 3. La explicación muestra la marca determinante y su motivo (CLA-07). 4. Con DS-03b, el hallazgo determinante es el de mayor nivel, Restringida (CLA-02). 5. «CONFIDENCIAL» y «confidencial» producen el mismo hallazgo de nivel Confidencial (CLA-02). 6. «control interno» **no** se reconoce como marca (CLA-02). 7. Resultado global «requiere revisión humana»; estado «pendiente de revisión». 8. Con DS-04b el nivel es Confidencial y no Interna (CLA-04). |
| Evidencia | Capturas de clasificación y explicación; acta. |
| Estado | **No ejecutado** |

### CP-04. Evaluación sin políticas activas (adicional)

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional · Adicional · Límite |
| Capacidades | 3 |
| Requisitos | POL-11 |
| Reglas | `RJ-03` |
| Dependencias abiertas | C7 (naturaleza de `RJ-03`), E2 |
| Datos y precondiciones | DS-04; PF-B; **sin ninguna política activa**; US-T1 |
| Procedimiento | 1. US-T1 somete DS-04 con PF-B. 2. Observar `RJ-03`, los avisos y el resultado global. |
| Esperado | 1. `RJ-03` «no evaluada». 2. Aviso «no hay políticas organizacionales activas» y recomendación al Administrador de definirlas (POL-11). 3. El resultado global no es «sin alerta» (POL-11, POL-06). |
| Evidencia | Captura del aviso y del resultado; acta. |
| Estado | **No ejecutado** |

### CP-05. Política más restrictiva que la regla

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional y trazabilidad · Mínimo |
| Capacidades | 2, 3, 5 |
| Requisitos | CLA-08, POL-02, POL-03, POL-06, POL-08, POL-10, POL-11, REP-05, REP-07 |
| Reglas | `RJ-02`, `RJ-03` |
| Dependencias abiertas | O-01 (quién gestiona políticas), C7, E2 |
| Datos y precondiciones | DS-04; PF-B; PO-01 y PO-02; US-ADM y US-T1; sin políticas activas al inicio |
| Procedimiento | 1. US-T1 evalúa DS-04 con PF-B (referencia). 2. US-ADM intenta activar PO-02 (incompleta). 3. US-ADM crea y activa PO-01. 4. US-T1 vuelve a someter DS-04. 5. US-ADM desactiva PO-01 y se vuelve a someter DS-04. 6. Consultar el historial y la evaluación hecha con PO-01 activa. |
| Esperado | 1. Base: `RJ-02` «advertencia» (marca «uso interno») y clasificación Interna (POL-03). 2. PO-02 se rechaza e indica el campo faltante (POL-10). 3. Tras activar PO-01, `RJ-03` se evalúa y el aviso desaparece (POL-11). 4. El resultado de la política se rotula «política organizacional» y no se atribuye a ninguna `RJ` (POL-02). 5. Resultado global «requiere revisión humana», con ambos resultados listados (POL-06). 6. La clasificación sigue siendo Interna (CLA-08). 7. El resultado identifica la política y el dato que la activó (POL-08). 8. Con PO-01 desactivada deja de aplicarse. 9. El historial registra activación y desactivación con qué, quién y cuándo (REP-07). 10. La evaluación hecha con PO-01 activa conserva la versión de la política que se aplicó entonces (REP-05). |
| Evidencia | Capturas de los resultados antes y después; captura del historial; acta. |
| Estado | **No ejecutado** |

### CP-06. Proveedor sin información verificada o desactualizado (adicional)

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional · Adicional · Negativo / límite |
| Capacidades | 4, 3 |
| Requisitos | POL-04, PRV-02, PRV-03, PRV-04 (complementario) |
| Reglas | `RJ-04` |
| Dependencias abiertas | O-04; PRV-04 solo si se implementa; valor del periodo de vigencia |
| Datos y precondiciones | DS-01; PF-C, PF-D y PF-V; periodo de vigencia configurado con valor N |
| Procedimiento | 1. Consultar PF-D en el catálogo. 2. Evaluar DS-01 con PF-D. 3. Evaluar DS-01 con PF-C. 4. Si PRV-04 existe: evaluar DS-01 con PF-V con antigüedad N+1, con antigüedad N, y tras actualizar su fecha. |
| Esperado | 1. La consulta de PF-D muestra «sin información verificada» y no deduce condiciones (PRV-02). 2. `RJ-04` «requiere revisión humana»; PF-D se trata como «sin información verificada» y no como «no seleccionado» (POL-04, PRV-03). 3. Con PF-C: «requiere revisión humana» e indica «no informado en la fuente» (POL-04, PRV-02). 4. PRV-04: con N+1 se marca «posiblemente desactualizada» y `RJ-04` al menos «advertencia» citando la fecha; con N no se marca; tras actualizar se retira la marca. |
| Evidencia | Capturas; acta. |
| Estado | **No ejecutado** |

### CP-07. Sin proveedor con datos personales

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional y trazabilidad · Mínimo · Positivo / límite |
| Capacidades | 1, 2, 3, 4, 5 |
| Requisitos | DOC-07, CLA-08, POL-05, PRV-03, REP-01, REP-05 |
| Reglas | `RJ-04` |
| Dependencias abiertas | O-05, O-06 (datos del registro), E2 |
| Datos y precondiciones | DS-01 y DS-02; US-T1 |
| Procedimiento | 1. US-T1 somete DS-01 **sin** seleccionar proveedor. 2. Observar hallazgos, clasificación, `RJ-04`, resultado global, estado y texto. 3. Consultar el registro y exportar el informe. 4. Repetir con DS-02 sin proveedor. |
| Esperado | 1. Los hallazgos y la clasificación coinciden con los de `CP-01` (DOC-07, CLA-08). 2. Se registra «evaluación de proveedor no completada»; `RJ-04` queda «no evaluada» (POL-05, PRV-03). 3. Resultado global «requiere revisión humana»; estado «pendiente de revisión». 4. El texto dice «no evaluado» y no usa «seguro», «aprobado» ni «autorizado». 5. El informe y el registro contienen «evaluación de proveedor no completada» (REP-01, REP-05). 6. Con DS-02, `RJ-04` queda «no evaluada» y el resultado global es **al menos «advertencia», nunca «sin alerta»** (POL-05). |
| Evidencia | Capturas del resultado, del registro y del informe exportado; acta. |
| Estado | **No ejecutado** |

### CP-08. Caso ambiguo con resolución humana

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional, trazabilidad y revisión humana · Mínimo · Límite |
| Capacidades | 1, 2, 5 |
| Requisitos | DOC-05, CLA-03, CLA-05, CLA-06, CLA-07, REP-01, REP-06, REP-08 |
| Reglas | `RJ-05` (control CT-05) |
| Dependencias abiertas | O-01 (quién es Revisor), O-02, O-05 |
| Datos y precondiciones | DS-05; PF-B; US-T1 y US-ADM; la evaluación de `CP-01` para el paso 7 |
| Procedimiento | 1. US-T1 somete DS-05 con PF-B. 2. Observar el hallazgo, la clasificación y el estado. 3. US-ADM filtra por «pendiente de revisión». 4. US-ADM intenta asignar un nivel sin justificación; luego con justificación. 5. US-ADM registra una decisión «proceder con ajustes», primero sin justificación y luego con justificación. 6. Consultar el estado final y el informe. 7. Con la evaluación de `CP-01` (Confidencial automática), US-ADM baja el nivel a Interna con justificación. |
| Esperado | 1. El hallazgo tiene certeza **baja** y cita ambos tipos posibles (DOC-05). 2. Clasificación «pendiente de revisión» con nivel sugerido; el resultado indica el motivo (CLA-05, CLA-03, CLA-07). 3. Estado «pendiente de revisión»; el informe muestra el nivel sugerido, no un nivel asignado (REP-01). 4. El filtro lista la evaluación (REP-08). 5. Sin justificación se rechaza; con justificación se registra el nivel humano y el automático (CLA-06). 6. La decisión sin justificación se rechaza; con justificación queda con persona y fecha y el estado pasa a «revisada» (REP-06). 7. La reducción se acepta con justificación, conserva el nivel automático y queda en el historial (CLA-06). |
| Evidencia | Capturas de cada paso; informe antes y después; acta. |
| Estado | **No ejecutado** |

### CP-09. Sin transmisión externa (control CT-01)

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Privacidad y seguridad · Mínimo |
| Capacidades | 1, 4 |
| Requisitos | DOC-04, PRV-03 |
| Reglas | `RJ-05` (CT-01) |
| Dependencias abiertas | O-07 (IA opcional); C3 (cómo se bloquean las conexiones) |
| Datos y precondiciones | DS-06; PF-A; aplicación en un equipo con **todas las conexiones externas bloqueadas** (por ejemplo, red desactivada) |
| Procedimiento | 1. Bloquear las conexiones externas del equipo y anotar cómo. 2. US-T1 somete DS-06 con PF-A y completa la evaluación. 3. Consultar el catálogo durante la evaluación. 4. Si el equipo dispone de una herramienta sencilla de observación de comunicaciones, repetir con la red activa y buscar el marcador único; si no, anotar la limitación. 5. Anotar el estado de CT-01 en el informe. 6. Revisar el registro de errores de la aplicación y del equipo para detectar intentos de conexión saliente durante la evaluación. |
| Esperado | 1. La evaluación finaliza y entrega clasificación, resultado e informe sin conexiones externas (DOC-04). 2. La consulta del catálogo funciona sin salida de datos (DOC-04). 3. Si hubo observación con red activa: el marcador no aparece fuera del entorno (DOC-04). 4. CT-01 figura como «aplicado». 5. No hay intentos de conexión saliente registrados durante la evaluación; si los hay, se registra un defecto (DOC-04). |
| Evidencia | Descripción del método de bloqueo; capturas de la evaluación finalizada; registro de observación si se hizo; acta. |
| Estado | **No ejecutado** |

### CP-10. Descarte y minimización (CT-02, CT-04)

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Privacidad · Mínimo · Negativo / límite |
| Capacidades | 1, 3, 5 |
| Requisitos | DOC-08, POL-07, REP-03, REP-05 |
| Reglas | `RJ-05` (CT-02, CT-04) |
| Dependencias abiertas | O-06 (datos persistidos y excepción de conservación) |
| Datos y precondiciones | DS-06 (incluye la frase de verificación); US-T1 |
| Procedimiento | 1. Evaluar DS-06 hasta el final. 2. Revisar el registro persistido (o su exportación) y comprobar que no contiene la frase de verificación ni un valor sensible completo; lo hacen los integrantes con los medios que ofrezca el stack y no es una función del MVP. 3. Revisar el informe exportado. 4. Iniciar una evaluación y cancelarla antes de que termine. 5. Provocar un fallo del análisis, solo si es factible sin infraestructura compleja. 6. Provocar un fallo del descarte, solo si es factible. |
| Esperado | 1. No hay coincidencias de la frase ni del valor completo en el registro ni en el informe (REP-03, DOC-08). 2. El registro contiene solo los datos de la lista de REP-05. 3. CT-02 y CT-04 figuran «aplicados» (POL-07). 4. Tras cancelar, el contenido se descarta (DOC-08). 5. Tras un fallo, se registra el error sin contenido (DOC-08). 6. Con descarte no logrado, CT-02 queda «no aplicado» y el resultado global es «requiere revisión humana» (DOC-08, POL-07). |
| Evidencia | Capturas de la revisión del registro sin la frase ni valores completos; informe; acta. |
| Nota | Los pasos 5 y 6 se omiten y se registran como «no ejecutable» con su justificación si la inducción de fallos exige infraestructura compleja. En ese caso, esos escenarios de DOC-08 y POL-07 quedan sin verificar. |
| Estado | **No ejecutado** |

### CP-11. Permisos por perfil

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Seguridad · Mínimo · Negativo |
| Capacidades | 1, 2, 3, 4, 5 |
| Requisitos | DOC-01, CLA-06, POL-10, PRV-05 (complementario), REP-04, REP-06, REP-08 |
| Reglas | Ninguna |
| Dependencias abiertas | O-01 (perfiles), O-10 (gestión de usuarios) |
| Datos y precondiciones | US-T1, US-T2 y US-ADM con una evaluación de cada Trabajador |
| Procedimiento | 1. Sin identificarse, intentar someter contenido. 2. Con US-T1: intentar asignar nivel, registrar decisión, crear y activar política y editar el catálogo. 3. US-T1 intenta exportar el informe de US-T2 y consultar el registro. 4. US-ADM exporta el informe de US-T1. |
| Esperado | 1. La solicitud sin identificar se rechaza sin procesar ni conservar el contenido (DOC-01). 2. Cada acción del paso 2 se deniega sin cambiar el estado (CLA-06, REP-06, POL-10, PRV-05). 3. La exportación ajena se deniega y el registro de US-T1 muestra solo sus evaluaciones (REP-04, REP-08). 4. US-ADM exporta con éxito (REP-04). |
| Evidencia | Capturas de cada denegación; acta. |
| Estado | **No ejecutado** |

### CP-12. Informe coherente

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Funcional, privacidad y explicabilidad · Mínimo |
| Capacidades | 1, 2, 3, 4, 5 |
| Requisitos | CLA-08, POL-02, POL-07, POL-09, PRV-02, REP-01, REP-02, REP-03, REP-04, DOC-06 |
| Reglas | `RJ-05` (CT-03), también `RJ-01` y `RJ-04` por su contenido |
| Dependencias abiertas | O-05, E2 |
| Datos y precondiciones | Evaluación de `CP-01` completada; DS-08 (valores de 10, 5 y 4 caracteres); US-T1 |
| Procedimiento | 1. Evaluar DS-01 con PF-A y DS-08, y exportar el informe como autor. 2. Revisar el informe con la lista de comprobación de abajo. 3. Revisar todos los textos del resultado y del informe contra la lista de términos prohibidos. |
| Esperado | 1. Elementos de REP-01 presentes: identificador, fecha, usuario y perfil, clasificación, resultado global, hallazgos explicados y enmascarados, resultados por regla, política y control con su estado de validación, estado del proveedor, versiones, recomendaciones de precaución y decisión si existe. 2. Clasificación y resultado de riesgo en campos separados (CLA-08). 3. Valor de 10 caracteres: solo los dos últimos visibles; de 5: dos últimos; de 4: oculto por completo (DOC-06). 4. Ningún valor sensible completo (REP-03). 5. Aviso de apoyo a la revisión humana, de no certificación y de que la ausencia de alertas no autoriza divulgar (REP-02). 6. Controles CT-01 a CT-05 «aplicado», rotulados «control funcional transversal» (POL-02, POL-07). 7. Ningún término prohibido: «cumple», «no cumple», «legal», «ilegal», «autorizado», «aprobado» (POL-09), ni frases que recomienden divulgar (REP-02). 8. Las condiciones del proveedor figuran como declaradas por la fuente, con fecha y sin calificativos de seguridad (PRV-02); la retención, la exclusión y la ubicación aparecen como «información para revisión humana» (REP-01). 9. La exportación se entrega al autor (REP-04). |
| Evidencia | Informe exportado; lista de comprobación diligenciada; acta. |
| Estado | **No ejecutado** |

### CP-13. Historial que no se sobrescribe (adicional)

| Campo | Contenido |
|---|---|
| Tipo y prioridad | Trazabilidad · Adicional |
| Capacidades | 5 |
| Requisitos | REP-07 |
| Reglas | `RJ-05` (CT-06, garantía estructural) |
| Dependencias abiertas | O-01 |
| Datos y precondiciones | Una evaluación con decisión registrada en `CP-08`; US-ADM |
| Procedimiento | 1. US-ADM corrige la decisión registrada. 2. Consultar el historial. 3. Intentar eliminar una entrada del historial desde la aplicación. |
| Esperado | 1. Se añade una entrada nueva y se conserva la original con su fecha y autor (REP-07). 2. El historial muestra qué cambió, quién y cuándo. 3. La aplicación no ofrece o rechaza la eliminación (REP-07). |
| Evidencia | Capturas del historial; acta. |
| Estado | **No ejecutado** |

## 5. Trazabilidad

### 5.1 Reglas y requisitos

Los resultados esperados dependen de reglas **provisionales**; E2 no está aprobada.

| Regla | Requisitos | Pruebas | Escenarios |
|---|---|---|---|
| `RJ-01` | DOC-05, CLA-01, CLA-04, POL-03 | CP-01, CP-02, CP-12 | ED-1 |
| `RJ-02` | CLA-02, CLA-04, POL-03, POL-06 | CP-02, CP-03, CP-05 | ED-2, ED-3 |
| `RJ-03` | POL-06, POL-10, POL-11 | CP-05; CP-04 (adicional) | ED-3 |
| `RJ-04` | POL-04, POL-05, PRV-02, PRV-03 | CP-01, CP-07, CP-12; CP-06 (adicional) | ED-1, ED-2 |
| `RJ-05` | POL-07, DOC-04, DOC-06, DOC-08, REP-03, REP-07 | CP-02, CP-08, CP-09, CP-10, CP-12; CP-13 (adicional) | ED-1, ED-2, ED-3 |

### 5.2 Requisitos y pruebas

Clase: **E** = MVP esencial; **C** = complementario.

| Requisito | Clase | Pruebas |
|---|---|---|
| DOC-01 | E | CP-01, CP-11 |
| DOC-02 | E | CP-01 (y VD-03) |
| DOC-03 | C | Sin prueba (PDF con texto extraíble; solo si se implementa) |
| DOC-04 | E | CP-09 |
| DOC-05 | E | CP-01, CP-02, CP-03, CP-08 |
| DOC-06 | E | CP-12 |
| DOC-07 | E | CP-01, CP-07 |
| DOC-08 | E | CP-10 |
| DOC-09, DOC-10 | C | Sin prueba |
| CLA-01 | E | CP-01, CP-02 |
| CLA-02 | E | CP-03 |
| CLA-03 | E | CP-01, CP-02, CP-08 |
| CLA-04 | E | CP-01, CP-03 |
| CLA-05 | E | CP-02, CP-08 |
| CLA-06 | E | CP-08, CP-11 |
| CLA-07 | E | CP-02, CP-03, CP-08 |
| CLA-08 | E | CP-01, CP-05, CP-07, CP-12 |
| POL-01 | E | **Sin prueba:** VD-02 |
| POL-02 | E | CP-05, CP-12 |
| POL-03 | E | CP-01, CP-02, CP-03, CP-05 |
| POL-04 | E | CP-01, CP-06 |
| POL-05 | E | CP-07 |
| POL-06 | E | CP-05 |
| POL-07 | E | CP-02, CP-08, CP-10, CP-12 |
| POL-08 | E | CP-01, CP-02, CP-05 |
| POL-09 | E | CP-12 |
| POL-10 | E | CP-05, CP-11 |
| POL-11 | E | CP-04, CP-05 |
| PRV-01 | E | **Sin prueba:** VD-01 |
| PRV-02 | E | CP-06, CP-12 |
| PRV-03 | E | CP-01, CP-06, CP-07, CP-09 |
| PRV-04 | C | CP-06 |
| PRV-05 | C | CP-11 |
| REP-01 | E | CP-07, CP-08, CP-12 |
| REP-02 | E | CP-02, CP-12 |
| REP-03 | E | CP-10, CP-12 |
| REP-04 | E | CP-11, CP-12 |
| REP-05 | E | CP-05, CP-07, CP-10 |
| REP-06 | E | CP-08, CP-11 |
| REP-07 | E | CP-05, CP-13 |
| REP-08 | E | CP-08, CP-11 |
| REP-09 | C | Sin prueba |

### 5.3 Requisitos esenciales sin caso propio y verificaciones documentales

Dos requisitos esenciales no tienen caso `CP`. No se les inventa una prueba funcional; se verifican con comprobaciones documentales o de entrada, que **no sustituyen** a los trece casos:

| ID | Requisito | Comprobación | Esperado |
|---|---|---|---|
| VD-01 | PRV-01 | Revisar las entradas del catálogo precargado (sección 6) | Cada entrada tiene proveedor, plan, fuente, fecha, tipo de dato y las cuatro condiciones; una entrada sin fuente o sin fecha se rechaza; las entradas de ejemplo llevan la etiqueta «ejemplo». |
| VD-02 | POL-01 | Consultar el registro de reglas | Aparecen al menos `RJ-01` a `RJ-05`; `RJ-05` figura como «controles funcionales transversales»; las reglas sin fuente verificada figuran «pendiente de fuente». |
| VD-03 | DOC-02 (escenarios de borde) | Texto vacío, texto en el límite exacto y por encima del límite | Se rechaza el vacío; se acepta el texto en el límite y se rechaza el que lo supera por una unidad. **Depende de que se defina el límite (O-03).** |

Los requisitos complementarios sin prueba (DOC-03, DOC-09, DOC-10, REP-09) se probarán solo si se implementan.

## 6. Datos sintéticos

**Reglas de uso** [Docente: sin datos reales ni contraseñas visibles]:
- Todo dato es ficticio. Una segunda persona del equipo lo revisa antes de usarlo (condición E-5).
- Correos con dominio reservado `.invalid`; nombres con "Ficticio" o "Ficticia"; números formados por ceros. **Ningún número debe corresponder a una persona real.**
- Las credenciales son claramente falsas, con la palabra «PRUEBA».
- Los criterios de detección de algunos tipos (financiero, salud, credencial) son provisionales (O-02); los textos podrán ajustarse al criterio final sin cambiar la intención de cada caso.

| ID | Contenido | Se usa en |
|---|---|---|
| DS-01 | Texto con `Nombre: Persona Ficticia Uno`, `correo: persona.uno@ejemplo.invalid` y `documento: 0000000001` | CP-01, CP-06, CP-12 |
| DS-01b | Mismo correo sin etiqueta: «Escriba a persona.uno@ejemplo.invalid» | CP-01 |
| DS-02 | «Resumen de la reunión de coordinación del jueves. Se acordó revisar el calendario del trimestre y la lista de tareas pendientes.» | CP-02, CP-07 |
| DS-02b | «Este es un documento público de ejemplo con el calendario general de actividades.» | CP-02 |
| DS-02c | «La Empresa Ficticia S.A.S. planea una estrategia comercial ficticia para el próximo trimestre.» (información corporativa sin marca) | CP-02 |
| DS-03 | «RESERVADO» más un texto ficticio de una propuesta comercial de «Empresa Ficticia S.A.S.», sin cifras reales | CP-03 |
| DS-03b | Texto con «confidencial» y «reservado» a la vez | CP-03 |
| DS-03c | Variantes: «CONFIDENCIAL», «confidencial», «Informe de control interno ficticio» (sin marca) | CP-03 |
| DS-04 | «USO INTERNO» más una lista ficticia de tareas del equipo de ejemplo | CP-04, CP-05 |
| DS-04b | «USO INTERNO» más `correo: persona.dos@ejemplo.invalid` | CP-03 |
| DS-05 | «Referencia: 1234567890» (secuencia compatible con documento o teléfono) | CP-08 |
| DS-06 | DS-01 más el marcador `TOKEN-CP09-7Q4Z` y la frase `lazo-azul-prueba-0099` | CP-09, CP-10 |
| DS-07 | Un indicador por categoría: correo etiquetado, `cuenta de ahorros: 00000000000`, un dato de salud ficticio rotulado como tal, una afiliación sindical ficticia, un indicio de menor («la persona ficticia es menor de edad»), una marca «CONFIDENCIAL» y `clave: PRUEBA-NO-REAL-0000` | CP-01 |
| DS-08 | Valores detectables de 10, 5 y 4 caracteres (por ejemplo, `documento: 0000000001`, `clave: AB123`, `clave: AB12`) | CP-12 |

**Usuarios de prueba:** US-T1 y US-T2 (Trabajador), US-ADM (Administrador, que actúa como Revisor). Su alta depende de O-10.

**Catálogo precargado, con tipo de dato «ejemplo»** (proveedores y fuentes ficticios):

| ID | Uso para mejorar modelos | Retención | Exclusión | Ubicación | Notas |
|---|---|---|---|---|---|
| PF-A | sí | 30 días (ficticio) | sí | región ficticia R1 | Todas las condiciones informadas |
| PF-B | no | 0 días (ficticio) | sí | región ficticia R2 | Todas las condiciones informadas |
| PF-C | no informado | no informado | no informado | no informado | |
| PF-D | — | — | — | — | **No registrado** en el catálogo |
| PF-V | no | 0 días (ficticio) | sí | región ficticia R2 | Fecha de verificación manipulable para probar el periodo de vigencia (PRV-04) |

**Políticas:** PO-01 «clasificación Interna → requiere revisión humana» (completa); PO-02 igual pero sin resultado recomendado (incompleta).

## 7. Procedimiento general de ejecución

1. Verificar las condiciones de entrada (sección 3) y registrar la versión de la aplicación, de las reglas y de las políticas.
2. Ejecutar el caso con los datos indicados y seguir sus pasos tal como están escritos.
3. Anotar lo observado **tal como ocurrió**, sin interpretarlo, en el acta de la sección 8.
4. Comparar con el resultado esperado y marcar cada punto como cumplido o no cumplido.
5. Capturar la evidencia en el momento. No reconstruirla después.
6. Si el resultado difiere, registrar un defecto (sección 9).
7. Otra persona del equipo revisa el acta y firma como revisora.

## 8. Evidencias que se recopilarán en E6

Ninguna existe todavía. Cada evidencia debe contener solo datos sintéticos y registrar fecha, hora, ejecutante y versión.

| Tipo | Contenido | Casos |
|---|---|---|
| Capturas de pantalla | Hallazgos, clasificación, resultados, estados, denegaciones, avisos | Todos |
| Informe exportado | Archivo generado por la aplicación | CP-01, CP-07, CP-12 |
| Revisión del registro | Revisión del registro persistido (o su exportación): no contiene la frase ni el valor completo | CP-10 |
| Método de aislamiento | Descripción de cómo se bloquearon las conexiones externas y, si se hizo, registro de observación | CP-09 |
| Historial exportado o capturado | Entradas de decisiones, ajustes y políticas | CP-05, CP-13 |
| Lista de comprobación diligenciada | Elementos del informe y términos prohibidos | CP-12 |
| Acta de ejecución | Una por caso | Todos |

**Acta de ejecución (formato; todos los campos vacíos hasta E6):**

| Campo | Valor |
|---|---|
| Caso | |
| Fecha y hora | |
| Ejecutante / revisor | |
| Versión de aplicación, reglas y políticas | |
| Resultado (Aprobado, Fallido, Bloqueado o No aplicable) | |
| Observaciones | |
| Evidencias (nombre y ubicación) | |
| Defectos asociados | |

**Convención de nombres:** `CP-xx_AAAAMMDD_iniciales_nn`. **Ubicación:** carpeta del equipo en OneDrive (EQUIPO_AIDATAGUARD, tarea 7.2); la ruta dentro del repositorio queda por definir (C1).

## 9. Registro de defectos y tratamiento de pruebas fallidas

**Estados de un caso:** Previsto → En ejecución → Aprobado, Fallido, Bloqueado o No aplicable. Hoy todos están en «Previsto».

**Severidad:**

| Nivel | Criterio |
|---|---|
| Crítica | Falla un control de privacidad o seguridad (`CP-09`, `CP-10`, `CP-11`), aparece contenido original o un valor completo en el registro o el informe, o el sistema usa lenguaje de certificación |
| Alta | Falla un resultado esperado de un caso mínimo |
| Media | Falla un resultado secundario o un caso adicional |
| Baja | Diferencia de texto o presentación sin efecto en el comportamiento |

**Registro de defectos (vacío hasta E6):**

| ID | Caso | Severidad | Descripción | Pasos | Evidencia | Estado | Responsable | Fecha |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

**Estados de un defecto:** Abierto, En corrección, Corregido (pendiente de repetir la prueba), Cerrado, Aceptado por el equipo (con el motivo).

**Reglas** [Equipo]:
1. **No se modifica el resultado esperado** para hacerlo coincidir con lo observado. Si el esperado es incorrecto, se corrige con un cambio formal de las specs (flujo de actualización) y se deja constancia.
2. Una prueba fallida se registra como defecto con su evidencia; no se oculta ni se repite hasta que pase sin dejar rastro del primer intento.
3. Tras la corrección se repite el caso completo y se conserva el acta del primer intento.
4. Una prueba **bloqueada** se registra con la dependencia que la bloquea y no cuenta como aprobada.
5. Un defecto crítico en `CP-09`, `CP-10` o `CP-11` impide dar por cerrada la salida (S-4).
6. Los defectos que queden abiertos al cierre de E6 se listan en el informe [Docente: defectos listados].
7. Si una prueba no es ejecutable por falta de infraestructura, se registra «No aplicable» con la justificación y se anota el requisito que queda sin verificar.

## 10. Escenarios de demostración (borrador, pendiente de C4)

La guía fija 15 minutos de demostración y 5 de preguntas, y que todos respondan [Docente]. Los tiempos son una propuesta de reparto [Equipo]. Los escenarios son los de `design.md` y no se han ensayado.

### ED-1. Privacidad y proveedor (unos 6 min)

- **Perfiles y capacidades:** Trabajador; capacidades 1, 2, 3, 4 y 5.
- **Pruebas:** CP-01, CP-09, CP-10, CP-12.
- **Preparación:** DS-06, PF-A en el catálogo, equipo con las conexiones externas bloqueadas.
- **Pasos:** el Trabajador evalúa DS-06 y selecciona PF-A; se muestran los hallazgos enmascarados, la clasificación Confidencial y los resultados de `RJ-01` y `RJ-04`; se abre el informe.
- **Evidencia de privacidad y minimización (se muestra en vivo):** (a) la evaluación se completa con las conexiones externas bloqueadas; (b) el informe muestra CT-01 a CT-05 «aplicado»; (c) la revisión del registro persistido (o de su exportación) muestra que no contiene `lazo-azul-prueba-0099` ni valores completos.

### ED-2. Revisión humana y proveedor no seleccionado (unos 5 min)

- **Perfiles y capacidades:** Trabajador y Revisor (Administrador); capacidades 1, 2, 3 y 5, y la 4 solo en el caso «no seleccionado».
- **Pruebas:** CP-03, CP-07, CP-08.
- **Preparación:** DS-03.
- **Pasos:** el Trabajador evalúa DS-03 sin proveedor; se muestran la clasificación Restringida, `RJ-02` «requiere revisión humana» y `RJ-04` «no evaluada»; el Revisor abre la evaluación pendiente, registra una decisión con justificación y la evaluación pasa a «revisada».

### ED-3. Administración de políticas (unos 4 min)

- **Perfiles y capacidades:** Administrador; capacidades 1, 2, 3 y 5 (no usa el catálogo).
- **Pruebas:** CP-04, CP-05, CP-12.
- **Preparación:** DS-04; PO-01; sin políticas activas.
- **Pasos:** el Administrador evalúa DS-04 sin políticas (`RJ-03` «no evaluada»); crea y activa PO-01; vuelve a someter el mismo texto y muestra que prevalece el resultado más restrictivo; filtra por «pendiente de revisión»; exporta el informe. No selecciona proveedor.

**Cada escenario debe ensayarse** (tarea 8.1) con el reparto de participación de los tres integrantes. La ficha E1 también los incluye como borrador.

## 11. Limitaciones, riesgos y responsabilidades del equipo

### Dependencias de decisiones abiertas

| Decisión | Casos afectados | Qué cambiaría |
|---|---|---|
| **E2 (aprobación de las reglas)** y C7 | CP-01 a CP-07, CP-12 | Los resultados esperados de `RJ-01` a `RJ-05` son provisionales |
| **O-01** (perfiles): decidida por el equipo (dos perfiles, DC-14) | CP-05, CP-08, CP-11, CP-13 | Pendiente de aprobación docente de E1; si cambia, cambia quién registra decisiones y gestiona políticas |
| **O-02** (taxonomía, marcas, criterios; lista de sensibilidad ampliada decidida en DC-18) | CP-01, CP-02, CP-03, CP-05, CP-08 | Textos de DS-03, DS-05 y DS-07 y resultados esperados |
| **O-03** (límite de tamaño; formatos ya decididos: texto esencial, PDF complementario) | VD-03; DOC-03 solo si se implementa | Sin límite definido no se puede probar el borde |
| **O-04** (origen del catálogo; condiciones ya decididas en DC-15) | CP-01, CP-06, CP-07, CP-12 | Datos de PF-A a PF-V |
| **O-05** (escala de resultados) | Todos los funcionales | Vocabulario esperado |
| **O-06** (datos persistidos y excepción de conservación) | CP-07, CP-10 | Qué contiene el registro |
| **O-07** (IA opcional) | CP-09 | Alcance de la verificación de no transmisión |
| **O-10** (gestión de usuarios) | CP-11 | Cómo se crean los usuarios de prueba |
| **C3** (stack) | Todos | Cómo se bloquean las conexiones y cómo se induce un fallo |
| **Papel del proveedor** (`legal-matrix.md`, sección 10, observación 4) | CP-01, CP-06 | Interpretación pendiente; no cambia los resultados esperados, porque el sistema no determina la licitud de una transferencia |
| **PRV-04** (complementario) | CP-06 (paso 4) | Solo se ejecuta si se implementa |

**C5** (seguimiento a compromisos) y **C4** no afectan a las pruebas, salvo que C4 cambie la ubicación de los escenarios.

### Limitaciones

- Las pruebas verifican el comportamiento descrito en las specs, no la validez jurídica de las reglas.
- La detección se prueba con muestras pequeñas y sintéticas. No mide la tasa de falsos negativos ni positivos.
- Los controles CT-01 a CT-05 los reporta el propio sistema; por eso `CP-09`, `CP-10` y `CP-12` los corroboran de forma independiente.
- La comprobación de no transmisión se apoya en ejecutar sin conexiones externas. Si no hay una herramienta sencilla de observación, no se demuestra la ausencia de tráfico con la red activa.
- Los fallos inducidos de `CP-10` pueden no ser factibles sin infraestructura compleja; entonces quedan sin verificar.
- No hay pruebas de rendimiento, usabilidad ni accesibilidad.
- Una sola organización y datos sintéticos: no se prueba un uso real.

### Riesgos

| Riesgo | Mitigación |
|---|---|
| Resultados esperados que cambian tras E2 | Plan v1 (tarea 4.7) y marca «provisional» |
| Plazo de E6 corto (7 a 13 dic) frente a 13 casos | Priorizar los 10 mínimos; los 3 adicionales solo si hay tiempo |
| Carga de revisión humana: toda clasificación pendiente exige un Revisor | Anotar en E6 cuántas evaluaciones quedan pendientes en cada caso |
| Datos sintéticos que se parezcan a datos reales | Revisión por una segunda persona antes de usarlos |
| Casos bloqueados por una decisión abierta | Registrar la dependencia y no contarlos como aprobados |

### Responsabilidades

Los nombres de los tres integrantes están por registrar.

| Tarea | Responsable | Fuente |
|---|---|---|
| Plan de pruebas v0 y v1 | Por asignar | Tareas 3.4 y 4.7 |
| Ejecución de los casos | Por asignar (Excel: 7 a 11 dic) | Tarea 6.1 |
| Revisión de la trazabilidad de las reglas y registro de defectos | Por asignar (Excel: 11 a 13 dic) | Tarea 6.2 |
| Revisión de cada acta | Una persona distinta de quien ejecutó | [Equipo] |
| Datos sintéticos | Por asignar | Tarea 5.5 |
| Aprobación del plan | Docente (fecha no definida) | [Docente] |

El equipo debe evitar que una misma persona ejecute y revise el mismo caso.

## 12. Estado y asuntos pendientes

- **Todas las pruebas están previstas y ninguna ha sido ejecutada.** No hay evidencias ni defectos reales.
- E1 y E2 siguen pendientes de aprobación docente; este plan no las da por aprobadas.
- El documento no modifica `initial-mvp`, `config.yaml`, `project-charter.md`, `legal-matrix.md`, el Excel ni los documentos del docente.
- Nombre del archivo: `test-plan.md` es la ruta oficial (DC-20); equivale a `casos-prueba.md` del Excel.
- Faltan para cerrar el plan v1: resultados de E2, decisiones O-01, O-02, O-04 y O-06, el valor del límite de tamaño y el periodo de vigencia, el método de aislamiento de red, y los responsables de cada caso.
