# Matriz jurídica preliminar E2: AI DataGuard

**Etapa E2, análisis jurídico y reglas** · Contexto Legal de la Ingeniería · UNINPAHU
**Fecha de consulta de todas las fuentes:** 12 de noviembre de 2026
**Estado: BORRADOR E2, PENDIENTE DE REVISIÓN HUMANA Y APROBACIÓN ACADÉMICA.** E2 no está aprobada. Esta matriz es un documento académico de trabajo: **no es un dictamen jurídico ni asesoría jurídica**.

## 0. Cómo leer este documento

**Método y límites.** Los textos se localizaron en sitios oficiales o en compilaciones de entidades públicas y se leyeron **con asistencia de IA. Ninguna fuente ha tenido verificación humana** (ni de una persona del equipo, ni de un abogado, ni del docente). La tarea 2.1 del plan asigna esa verificación al Integrante 2 (por registrar). La búsqueda no fue exhaustiva. Los extractos son fragmentos breves; deben contrastarse con la fuente antes de citarlos. Todas las pruebas y escenarios mencionados están **previstos, no ejecutados**.

**Etiquetas de fundamento** (las cuatro categorías de OpenSpec):

| Etiqueta | Significado |
|---|---|
| **[OL]** Obligación legal con fuente verificada | El texto de la disposición se localizó y se leyó. Se afirma qué dice, no cómo se aplica a AI DataGuard. |
| **[IP]** Interpretación pendiente de revisión jurídica | Aplicar la disposición al caso exige una interpretación que nadie ha validado. |
| **[PC]** Política corporativa propuesta | Propuesta de la organización o del equipo; no es mandato legal. |
| **[RF]** Regla funcional de AI DataGuard | Comportamiento del sistema decidido por el equipo. |

**Forma de cita.** Para el Decreto 1377 de 2013 se usa la numeración compilada: *Decreto 1074 de 2015, art. 2.2.2.25.x.x (Decreto 1377 de 2013, art. N)*.

Los identificadores `RJ-01` a `RJ-05` son **provisionales**. Sus "temas" son una hipótesis de trabajo derivada de la hoja "Puntos de Dolor" del Excel. La consulta **C7** sigue abierta (sección 7). Cada regla tiene una categoría de fundamento **principal** y, si corresponde, **secundarias** (decisión del equipo D3). La principal se propone como [IP] (o [RF] para `RJ-05`) para no presentar una interpretación como obligación; su asignación definitiva depende de C7 y de E2.

## 1. Reglas provisionales y su propósito actual

Según `design.md` y `specs/compliance-policies`:

| ID | Nombre y objetivo | Tipo en OpenSpec | Propósito actual |
|---|---|---|---|
| RJ-01 | Datos personales y herramientas de IA externas | Regla jurídica preliminar | Alertar cuando el contenido incluye datos personales. |
| RJ-02 | Información corporativa reservada y secretos empresariales | Regla jurídica preliminar | Exigir revisión cuando el contenido lleva marcas de confidencialidad. |
| RJ-03 | Políticas organizacionales de uso | Regla jurídica preliminar (evalúa políticas) | Avisar si no hay políticas activas y aplicar las que existan. |
| RJ-04 | Condiciones de tratamiento de los proveedores de IA | Regla jurídica preliminar | Evaluar las condiciones declaradas por el proveedor frente a los hallazgos. |
| RJ-05 | Controles funcionales transversales | Controles funcionales transversales | Verificar que el sistema aplique sus propios controles (CT-01 a CT-05), que son decisiones del equipo y no obligaciones legales específicas. |

## 2. Fuentes consultadas

**Clases de fuente:** **Oficial** = sitio institucional del órgano que expide o custodia la norma. **Compilación** = compilación de una entidad pública, no el Diario Oficial. **Copia** = reproducción en sitio gubernamental que no es la publicación oficial. **Secundaria** = análisis o prensa; no se usa como fundamento.

| ID | Fuente | URL | Clase | Qué se leyó |
|---|---|---|---|---|
| F1 | Ley Estatutaria 1581 de 2012 | http://www.secretariasenado.gov.co/senado/basedoc/ley_1581_2012.html | Oficial (Secretaría del Senado, actualizada al 31 oct 2026) | Arts. 1 a 30. La nota de vigencia del art. 4 literal g no pudo leerse. |
| F2 | Ley Estatutaria 1266 de 2008 | http://www.secretariasenado.gov.co/senado/basedoc/ley_1266_2008.html | Oficial | Título, art. 2 y el inicio del art. 3. Aplicabilidad por determinar. |
| F3 | Decreto 1377 de 2013 | https://normograma.mintic.gov.co/mintic/compilacion/docs/decreto_1377_2013.htm | Compilación (MinTIC) | Arts. 3, 4, 6, 11, 12, 13, 14, 24, 25 y 26. |
| F8 | Decreto Único Reglamentario 1074 de 2015, capítulo 25 | https://normograma.mintic.gov.co/mintic/compilacion/docs/decreto_1074_2015.htm | Compilación (MinTIC) | Secciones 1 a 6 del capítulo 25 y el art. 3.1.1. |
| F4 | Circular Externa 002 de 2024 de la SIC | https://normograma.mintic.gov.co/mintic/compilacion/docs/circular_superindustria_0002_2024.htm; publicación SIC: https://sedeelectronica.sic.gov.co/transparencia/normativa/circular-externa-2-de-2024-de-la-superintendencia-de-industria-y-comercio-lineamientos-sobre-el-tratamiento-de-datos | Compilación (texto leído); oficial (SIC, localizada por búsqueda y no abierta) | Considerandos y numerales I a X (Diario Oficial 52.856, 22 ago 2024). |
| F11 | Circular Externa 002 de 2025 de la SIC | https://sedeelectronica.sic.gov.co/transparencia/normativa/circular-externa-no-002-del-07-de-octubre-de-2025; https://normograma.mintic.gov.co/mintic/compilacion/docs/circular_superindustria_0002_2025.htm | Oficial (SIC) y compilación | Asunto, alcance y numerales 1 a 4. Se examinó; no se usa como fundamento (sección 3.4). |
| F9 | Circular Única de la SIC, Título V, Capítulo 3 (transferencia a terceros países; Circular Externa 005 de 2017 y modificaciones) | https://normas.cra.gov.co/Gestor/docs/circular_superindustria_0005_2017.htm; proyectos publicados por la SIC: https://sedeelectronica.sic.gov.co/sites/default/files/normatividad/072017/Transferencia-internacional-de-datos-PFR2.pdf y https://sedeelectronica.sic.gov.co/sites/default/files/normatividad/032018/Proy_Circular_Modifica_Nral_3_2_Capitulo_3_CU_Inclus_Australia_Formato.pdf | Compilación (gestor de la CRA) y documentos de la SIC | Numerales 3.1 y 3.2 y sus parágrafos. **La versión consolidada vigente no se abrió.** |
| F10 | Sentencia C-748 de 2011 de la Corte Constitucional | Texto transcrito dentro de F1. URL propia de la Corte: no verificada. | Oficial (transcrita por la Secretaría del Senado) | Examen de los arts. 6 y 7 y la parte resolutiva. |
| F5 | Decisión 486 de 2000 de la Comunidad Andina, arts. 260 a 266 | https://and.gov.co/sites/default/files/2022-05/Decision_andina_486_2000.pdf (copia); Gaceta oficial de la CAN: https://www.comunidadandina.org/DocOficialesFiles/Gacetas/Gace600.pdf | Copia (leída); oficial (CAN, **no abierta**) | Arts. 260 a 266. |
| F6 | Ley 256 de 1996 (competencia desleal) | http://www.secretariasenado.gov.co/senado/basedoc/ley_0256_1996.html | Oficial | Arts. 2 y 16. Las notas del editor no pudieron leerse. |
| F7 | Ley 1273 de 2009, art. 269F | http://www.secretariasenado.gov.co/senado/basedoc/ley_1273_2009.html | Oficial | Solo el art. 269F. Se cita como referencia, no como fundamento. |

**Fuente secundaria consultada y no usada como fundamento:** un artículo de la International Bar Association describe la Circular 002 de 2024 como lineamientos interpretativos no vinculantes como las leyes. No es una fuente oficial; la naturaleza jurídica de la Circular queda como [IP].

**No se identificó**, en las fuentes consultadas, una norma colombiana que regule específicamente el uso de IA generativa por trabajadores. La búsqueda no fue exhaustiva.

## 3. Marco normativo común

### 3.1 Compilación del Decreto 1377 en el Decreto 1074 de 2015

El art. 3.1.1 del Decreto 1074 es una "derogatoria integral" de las disposiciones reglamentarias del sector sobre las mismas materias, con excepciones enumeradas. En las excepciones leídas no aparece el Decreto 1377. Por eso se cita con la numeración compilada. El capítulo 25 fue adicionado por el Decreto 255 de 2022 (sección 7, normas corporativas vinculantes), que no se consultó. En las secciones 1 a 6 del texto leído no se observan modificaciones.

| Decreto 1377 de 2013 | Decreto 1074 de 2015 | Tema |
|---|---|---|
| Art. 3, núms. 4 y 5 | 2.2.2.25.1.3 | Definiciones de transferencia y transmisión |
| Art. 4 | 2.2.2.25.2.1 | Recolección limitada a datos pertinentes y adecuados |
| Art. 6 | 2.2.2.25.2.3 | Datos sensibles |
| Art. 11 | 2.2.2.25.2.8 | Limitaciones temporales y supresión |
| Art. 12 | 2.2.2.25.2.9 | Niños, niñas y adolescentes |
| Art. 13 | 2.2.2.25.3.1 | Políticas de tratamiento |
| Art. 14 | 2.2.2.25.3.2 | Aviso de privacidad |
| Art. 24 | 2.2.2.25.5.1 | Transferencia y transmisión internacional |
| Art. 25 | 2.2.2.25.5.2 | Contrato de transmisión |
| Art. 26 | 2.2.2.25.6.1 | Demostración (responsabilidad demostrada) |
| Art. 27 | 2.2.2.25.6.2 | Políticas internas efectivas |

**Discrepancia documentada.** La compilación del Decreto 1377 (MinTIC) anota que su art. 25 es "no compilado en el Decreto Único Reglamentario 1074 de 2015". El texto del Decreto 1074 (misma entidad) sí contiene el art. 2.2.2.25.5.2, con la remisión "Decreto 1377 de 2013, artículo 25", y el art. 2.2.2.25.5.1 remite a él. Se cita por 2.2.2.25.5.2. Queda por confirmar en el Diario Oficial o en una fuente primaria.

### 3.2 Transferencia internacional, transmisión internacional y tratamiento por terceros

| Figura | Definición o regla verificada | Fuente |
|---|---|---|
| **Transferencia** | "[…] envía la información o los datos personales a un receptor, que a su vez es Responsable del Tratamiento y se encuentra dentro o fuera del país." | F8 2.2.2.25.1.3 núm. 4 |
| **Transmisión** | "Tratamiento de datos personales que implica la comunicación de los mismos dentro o fuera del territorio de la República de Colombia cuando tenga por objeto la realización de un Tratamiento por el Encargado por cuenta del Responsable." | F8 2.2.2.25.1.3 núm. 5 |
| **Suministro a terceros** | El Decreto no lo define. El art. 13 de la Ley 1581 lista a quiénes puede suministrarse la información; el art. 4 literales c y f limita su divulgación y circulación. | F1 |
| **Transferencia internacional** | El art. 26 prohíbe transferir datos a países sin niveles adecuados, con excepciones: autorización expresa e inequívoca, datos médicos, transferencias bancarias o bursátiles, tratados, ejecución de un contrato con autorización y salvaguardia del interés público o defensa de un derecho en un proceso. La expresión "necesarias o" del literal f se declaró inexequible (C-748 de 2011). Si no aplica ninguna excepción, la SIC emite una declaración de conformidad. | F1 art. 26; F10 |
| **Transmisión internacional** | No requiere informar al Titular ni su consentimiento cuando exista un contrato conforme a 2.2.2.25.5.2, que debe señalar los alcances, las actividades del encargado y al menos tres obligaciones: tratar los datos según los principios, salvaguardar su seguridad y guardar confidencialidad. | F8 2.2.2.25.5.1 y 2.2.2.25.5.2 |
| **Estándares de país adecuado** | Los fija la SIC. Según los textos leídos, el numeral 3.2 incluye a Estados Unidos. Hubo modificaciones posteriores. El tránsito transfronterizo no es transferencia. La transmisión a países adecuados sigue los términos de la transferencia (parágrafo 4). | F9 |

**No se asigna automáticamente una figura jurídica a los proveedores de IA.** La ley no dice cuál corresponde a un proveedor de IA generativa. Lo que se puede plantear como hipótesis [IP], a validar:

| Escenario hipotético | Figura que podría corresponder | Efecto relevante |
|---|---|---|
| El proveedor trata el contenido solo por cuenta de la organización y bajo contrato | Transmisión | Contrato de 2.2.2.25.5.2; sin consentimiento adicional para la transmisión internacional con contrato |
| El proveedor decide el uso del contenido para sus propios fines | Transferencia a un responsable | Si está fuera de Colombia, art. 26 y sus excepciones |
| Los términos no aclaran el papel del proveedor | Suministro a tercero | Arts. 4 literales c y f y 13 |

Las condiciones del catálogo ("uso para mejorar modelos", "ubicación del tratamiento") son un indicio razonable del papel del proveedor, pero **el catálogo registra lo que el proveedor declara; no determina la figura jurídica**.

### 3.3 Datos sensibles y datos de niños, niñas y adolescentes

**Datos sensibles (Ley 1581, arts. 5 y 6).**
- El art. 5 define como sensibles los que afectan la intimidad o pueden generar discriminación, "tales como" los que revelen origen racial o étnico, orientación política, convicciones religiosas o filosóficas, pertenencia a sindicatos, organizaciones sociales o de derechos humanos, o partidos políticos, y los datos de salud, vida sexual y biométricos.
- El art. 6 prohíbe su tratamiento, excepto cuando: **a)** el Titular da autorización explícita; **b)** se salvaguarda el interés vital de un Titular incapacitado; **c)** lo hace una fundación, ONG o asociación sin ánimo de lucro de finalidad política, filosófica, religiosa o sindical, solo sobre sus miembros; **d)** son necesarios para el reconocimiento, ejercicio o defensa de un derecho en un proceso judicial; **e)** hay finalidad histórica, estadística o científica, con supresión de la identidad.
- C-748 de 2011 declaró inexequible la frase "el Titular haya hecho manifiestamente públicos o" del literal d. Para el resto del literal d, la Corte exige la autorización previa y expresa del Titular, la orden judicial y las demás garantías del hábeas data. Un dato sensible hecho público no pasa a ser de naturaleza pública.
- Decreto 1074, art. 2.2.2.25.2.3 (art. 6 del 1377): el Titular debe ser informado de que no está obligado a autorizar, y "Ninguna actividad podrá condicionarse a que el Titular suministre datos personales sensibles."

**Niños, niñas y adolescentes (Ley 1581, art. 7).**
- El texto dice: "Queda proscrito el Tratamiento de datos personales de niños, niñas y adolescentes, salvo aquellos que sean de naturaleza pública."
- C-748 de 2011 (examen del art. 7) dijo que no debe entenderse "en el sentido de que existe una prohibición casi absoluta" del tratamiento. Procede cuando responda al interés superior de los niños, niñas y adolescentes y asegure sus derechos prevalentes.
- Decreto 1074, art. 2.2.2.25.2.9 (art. 12 del 1377): el tratamiento está prohibido salvo datos de naturaleza pública y siempre que responda al interés superior y respete los derechos fundamentales. El representante legal autoriza, previo ejercicio del derecho del menor a ser escuchado.
- **No se afirma una prohibición absoluta.** Se describe un régimen condicionado.

**Límite del sistema:** AI DataGuard no puede saber si un dato pertenece a un menor ni si existe autorización; la decisión recae en la revisión humana.

### 3.4 Circulares Externas 002 de 2024 y 002 de 2025 de la SIC

| Aspecto | CE 002 de 2024 (F4) | CE 002 de 2025 (F11) |
|---|---|---|
| Fecha y publicación | 21 ago 2024; Diario Oficial 52.856 | 7 oct 2025; Diario Oficial 53.268 del 9 oct 2025 (la compilación de MinTIC consigna "53.368", con la nota "sic") |
| Asunto | Lineamientos sobre el tratamiento de datos personales en sistemas de IA | **Transferencia de tecnología** con datos personales o con tecnologías que los tratan |
| Destinatarios | Sujetos vigilados por la SIC; administradores de datos que desarrollan, despliegan o usan sistemas de IA | Entidades vigiladas; proveedores y receptores de tecnología |
| Fundamento | Facultad de la SIC de "impartir instrucciones sobre las medidas y procedimientos necesarios para la adecuación […]" (Ley 1581, art. 21 literal e) | La misma facultad, citada expresamente |
| Alcance | Afirma que las Leyes 1266 y 1581 son "normas neutrales temática y tecnológicamente". Numeral IV (estudio de impacto de privacidad): previo al diseño y desarrollo de IA de alto riesgo. Numeral VIII: medidas de seguridad auditables. | Verificación preliminar, responsabilidad demostrada, protección desde el diseño y por defecto, garantías contractuales, en procesos de transferencia de tecnología |
| Uso en esta matriz | Fuente de apoyo para `RJ-01` (los "usuarios" de IA con datos personales son destinatarios posibles) y de contexto para `RJ-05`. **No** se usa como fundamento de `RJ-03`. | **Examinada y no usada como fundamento.** No hay proceso de transferencia de tecnología ni contraprestación en el MVP. Solo sería pertinente si AI DataGuard se transfiriera como tecnología a una organización. No confundir transferencia de tecnología con transferencia de datos. |

- La Circular de 2024 describe la IA como un sistema que "típicamente" se usa "para tomar decisiones autónomas o para asistir a un tomador de decisiones humano". No exige revisión humana.
- Su naturaleza es la de una instrucción administrativa a los sujetos vigilados. Su fuerza vinculante frente a la ley es [IP].
- La de 2025, en sus numerales 2.3 y 3.3, habla de documentar decisiones y de minimización. Esos numerales solo valen en procesos de transferencia de tecnología.
- La propia Circular de 2025 cita el "artículo 3" de la Ley 1581 para los principios, que en el texto leído están en el art. 4, y menciona un principio de "necesidad" que no figura en esa lista. Se registra como observación de la fuente y no se corrige aquí.

## 4. Matriz por regla

**Responsable general (Excel, tareas 2.1, 2.2 y 2.3):** documentación y verificación de fuentes, Integrante 2 (por registrar); validación, Equipo completo; aprobación, docente. **Perfiles (E1):** Trabajador y Administrador; la función de responsable de cumplimiento es una responsabilidad asignable al Administrador. "Revisor" = Administrador.

### RJ-01. Datos personales y herramientas de IA externas

| Campo | Contenido |
|---|---|
| 1. Nombre y objetivo | Alertar al Trabajador cuando el contenido contiene datos personales antes de usarlo con una herramienta de IA generativa. |
| 2. Categoría | **Principal:** [IP] (aplicación a IA generativa). **Secundaria:** [OL] (marco general, texto leído). |
| 3. Norma y fuente | F1 arts. 2, 3, 4 literales b, c, f, g y h, 5, 6, 7, 9 y 26; F8 2.2.2.25.2.3, 2.2.2.25.2.9, 2.2.2.25.5.1 y 2.2.2.25.1.3; F10; F4. |
| 4. Fundamento y alcance | La Ley 1581 se aplica a datos personales en bases de datos de entidades públicas o privadas (art. 2). El art. 4 literal c vincula la divulgación de datos personales a la autorización. Los datos sensibles y los de menores tienen regímenes propios (sección 3.3). Falta determinar si enviar contenido a un proveedor es una transmisión, una transferencia o un suministro a un tercero (sección 3.2) y el papel de la organización. Aplica al tratamiento real de datos; la demostración usa datos sintéticos. [IP] |
| 5. Condición de activación | El contenido tiene hallazgos de datos personales de cualquier categoría, indicadores de sensibilidad alta o indicios de datos de menores (`CLA-01`, `POL-03`). |
| 6. Resultado | «requiere revisión humana», con advertencia reforzada, ante indicadores de sensibilidad alta o de menores; «advertencia» ante otros datos personales; «sin alerta» sin ellos. Si hay proveedor, se combina con `RJ-04`. **Decisión funcional del equipo (DC-18):** la advertencia indica que el tratamiento de esos datos tiene reglas especiales (sección 3.3) y que el sistema no verifica autorizaciones; **no afirma una prohibición absoluta**. |
| 7. Evidencia generada | Hallazgos enmascarados, clasificación, resultado por regla con su estado de validación e informe (`REP-01`). Prueba prevista: `CP-01`. |
| 8. Responsable | Aplicación: el sistema. Revisión: Revisor (Administrador). Documentación: Integrante 2 (por registrar). |
| 9. Extracto y referencia | F1 art. 4 literal c: "Los datos personales no podrán ser obtenidos o divulgados sin previa autorización, o en ausencia de mandato legal o judicial que releve el consentimiento". |
| 10. Verificación y pendientes | Texto leído con asistencia de IA, sin verificación humana. Pendiente: papel jurídico de organización y proveedor, aplicación del art. 6 y del art. 7, y revisión de la nota de vigencia del art. 4 literal g. |

### RJ-02. Información corporativa reservada y secretos empresariales

| Campo | Contenido |
|---|---|
| 1. Nombre y objetivo | Exigir revisión humana cuando el contenido lleva marcas de confidencialidad antes de usarlo con IA generativa. |
| 2. Categoría | **Principal:** [IP]. **Secundarias:** [OL] (textos leídos) y [RF] (marcas y niveles). |
| 3. Norma y fuente | F5 arts. 260, 262 y 265; F6 arts. 2 y 16. |
| 4. Fundamento y alcance | El art. 260 de la Decisión 486 define el secreto empresarial: información secreta, con valor comercial por serlo y objeto de medidas razonables de reserva. El art. 265 obliga a abstenerse de usar o divulgar un secreto empresarial a quien accede a él por su trabajo y fue prevenido de su confidencialidad. El art. 16 de la Ley 256 considera desleal divulgar o explotar sin autorización secretos a los que se accedió legítimamente con deber de reserva. **Alcance de los artículos 2 y 16 de la Ley 256:** el art. 2 exige que los actos se realicen "en el mercado y con fines concurrenciales", pero el último inciso del art. 16 dice que las acciones por violación de secretos proceden sin que concurran los requisitos del art. 2. El "ánimo de obtener provecho propio o de un tercero o de perjudicar" aparece en el art. 262 literal b de la Decisión 486, no en el art. 16 de la Ley 256. No consta que enviar información a un proveedor de IA sea por sí mismo uno de esos actos; la relación es indirecta: las marcas podrían ser una medida razonable de reserva. [IP] |
| 5. Condición de activación | Marcas explícitas «confidencial», «reservado», «restringido» o «uso interno» en el contenido (`CLA-02`, `POL-03`). La detección se limita a marcas explícitas. |
| 6. Resultado | «requiere revisión humana» ante las tres primeras marcas; «advertencia» ante «uso interno»; «sin alerta» sin marcas, con la limitación declarada. La correspondencia entre marcas y resultados es [RF]. |
| 7. Evidencia generada | Hallazgos de marca, clasificación, resultado y limitación declarada en el informe. Pruebas previstas: `CP-03` y `CP-05`. |
| 8. Responsable | Aplicación: el sistema. Revisión: Revisor (Administrador). Documentación: Integrante 2 (por registrar). |
| 9. Extracto y referencia | F5 art. 260 literal c: "haya sido objeto de medidas razonables tomadas por su legítimo poseedor para mantenerla secreta". F6 art. 16, último inciso: las acciones "procederán sin que para ello sea preciso que concurran los requisitos a que hace referencia el artículo 2o." |
| 10. Verificación y pendientes | Textos leídos con asistencia de IA; la Gaceta de la CAN no se abrió y las notas del editor de la Ley 256 no pudieron leerse. Pendiente: incorporación de la norma andina en Colombia, fuente de la confidencialidad pactada por contrato o reglamento, y que ningún texto leído define una taxonomía legal "Interna, Confidencial, Restringida". |

### RJ-03. Políticas organizacionales de uso

| Campo | Contenido |
|---|---|
| 1. Nombre y objetivo | Verificar si la organización tiene políticas aplicables al uso de IA generativa y aplicarlas a la evaluación. |
| 2. Categoría | **Principal:** [IP]. **Secundaria:** [PC]. |
| 3. Norma y fuente | F1 art. 17 literal k y art. 18 literal f; F8 2.2.2.25.3.1 y 2.2.2.25.6.2. |
| 4. Fundamento y alcance | El art. 17 literal k obliga al Responsable del Tratamiento a adoptar un manual interno de políticas y procedimientos para cumplir la Ley 1581. El art. 2.2.2.25.3.1 obliga a desarrollar políticas para el tratamiento de datos personales, y el art. 2.2.2.25.6.2 exige políticas internas efectivas, proporcionales al tamaño empresarial. Esos deberes se refieren al tratamiento de datos personales, no a una política sobre el uso de IA generativa. Una política de uso de IA generativa sería [PC], sin mandato legal identificado. |
| 5. Condición de activación | No hay políticas organizacionales activas (`POL-11`), o hay políticas activas aplicables (`POL-10`). |
| 6. Resultado | Sin políticas: «no evaluada» con aviso, nunca «sin alerta». Con políticas: el resultado de la política, rotulado «política organizacional». La advertencia por ausencia de políticas es [RF], no un mandato legal. |
| 7. Evidencia generada | Aviso en el informe y estado de `RJ-03`. Pruebas previstas: `CP-05` y `CP-04` (adicional). |
| 8. Responsable | Aplicación: el sistema. Definición de las políticas y revisión: Administrador. Documentación: Integrante 2 (por registrar). |
| 9. Extracto y referencia | F1 art. 17 literal k: "Adoptar un manual interno de políticas y procedimientos para garantizar el adecuado cumplimiento de la presente ley". |
| 10. Verificación y pendientes | Textos leídos con asistencia de IA. Pendiente: la naturaleza jurídica de la regla (C7). La referencia al art. 25 de la Ley 1581 (Registro Nacional de Bases de Datos) se retiró del fundamento porque no se verificó si una pyme debe inscribirse; queda como referencia no verificada. |

### RJ-04. Condiciones de tratamiento de los proveedores de IA

| Campo | Contenido |
|---|---|
| 1. Nombre y objetivo | Evaluar las condiciones que declara el proveedor frente a los hallazgos del contenido, sin determinar su figura jurídica. |
| 2. Categoría | **Principal:** [IP]. **Secundarias:** [OL] (marco general, texto leído) y [RF] (condiciones del catálogo). |
| 3. Norma y fuente | F1 art. 3 literales d y e, art. 4 literales c, f y g, art. 13, art. 17 literal i, art. 18 y art. 26; F8 2.2.2.25.1.3, 2.2.2.25.5.1 y 2.2.2.25.5.2; F9 numerales 3.1 y 3.2; F10. |
| 4. Fundamento y alcance | Ver la sección 3.2: distinción entre transferencia, transmisión y suministro a terceros, y reglas del art. 26. El art. 17 literal i obliga al Responsable a exigir al Encargado el respeto a las condiciones de seguridad y privacidad. **No se asigna automáticamente una categoría jurídica al proveedor.** Qué sea "uso del contenido para mejorar modelos" frente al principio de finalidad (art. 4 literal b) es [IP]. Las cuatro condiciones del catálogo son propuesta del equipo [RF]; su fuente es la declaración del proveedor, no la ley. |
| 5. Condición de activación | Proveedor seleccionado, hallazgos relevantes y condiciones del catálogo (`POL-04`). Sin proveedor: «no evaluada» (`POL-05`). |
| 6. Resultado | «requiere revisión humana» si no hay información verificada, o si hay hallazgo relevante y el uso para mejorar modelos es «sí» o «no informado»; «advertencia» con otras condiciones; «sin alerta» sin hallazgos relevantes. **Decisión del equipo (DC-15):** solo el uso para mejorar modelos interviene en el resultado; retención, exclusión y ubicación se muestran como «información para revisión humana», y el sistema **no determina** si una transferencia o transmisión internacional es lícita. |
| 7. Evidencia generada | Condiciones, fuente y fecha de cada entrada del catálogo, y estado de la evaluación del proveedor, en el informe. Pruebas previstas: `CP-01` y `CP-07` (mínimos), `CP-06` (adicional). |
| 8. Responsable | Aplicación: el sistema. Mantenimiento del catálogo y revisión: Administrador. Documentación: Integrante 2 (por registrar). |
| 9. Extracto y referencia | F1 art. 26: "Se prohíbe la transferencia de datos personales de cualquier tipo a países que no proporcionen niveles adecuados de protección de datos." F8 2.2.2.25.5.1 núm. 2: las transmisiones internacionales entre responsable y encargado "no requerirán ser informadas al Titular ni contar con su consentimiento cuando exista un contrato". |
| 10. Verificación y pendientes | Textos leídos con asistencia de IA. La lista de países adecuados (F9) se leyó en proyectos y en un gestor normativo, no en la versión consolidada vigente; cambia con el tiempo y debe revisarse. Pendiente: papel del proveedor (encargado, responsable o tercero), validez de la discrepancia sobre el art. 25 (sección 3.1) y declaración de conformidad. |

### RJ-05. Controles funcionales transversales

| Campo | Contenido |
|---|---|
| 1. Nombre y objetivo | Verificar que el propio sistema aplique sus controles (CT-01 a CT-05), sin evaluar el contenido. |
| 2. Categoría | **Principal:** [RF]. **Secundaria:** [IP] (respaldo indirecto). No se afirma que sea una regla legal independiente. |
| 3. Norma y fuente | F1 art. 4 literales f, g y h, art. 17 literal d, art. 18 literales b y j; F8 2.2.2.25.2.1, 2.2.2.25.2.8, 2.2.2.25.6.1 y 2.2.2.25.6.2; F4 numerales III, VI y VIII. |
| 4. Fundamento y alcance | Ver la sección 6. Hay anclajes generales sobre seguridad, confidencialidad, limitación de la recolección, tiempo de conservación y responsabilidad demostrada, proporcional al tamaño empresarial. **No hay un fundamento jurídico directo verificado que exija enmascarado, descarte automático, historial inmutable o revisión humana.** Esos deberes, donde existan, son de quien trata datos reales y aplican a un despliegue real. |
| 5. Condición de activación | Toda evaluación: CT-01 a CT-05 se registran como «aplicado» o «no aplicado» (`POL-07`); CT-05 queda «aplicado» cuando una evaluación que requiere revisión humana, con clasificación pendiente o con un control «no aplicado» queda «pendiente de revisión» y no emite recomendación de divulgación. CT-06 (historial) se verifica en `REP-07` y no se registra por evaluación. No depende del contenido. |
| 6. Resultado | «aplicado» o «no aplicado»; un control «no aplicado» exige revisión humana. |
| 7. Evidencia generada | Estado de los controles en el informe. Pruebas previstas: `CP-09`, `CP-10` y `CP-12` (mínimos), `CP-13` (adicional). |
| 8. Responsable | Aplicación: el sistema. Revisión: Revisor (Administrador). Documentación: Integrante 2 (por registrar). |
| 9. Extracto y referencia | F8 2.2.2.25.6.1: los responsables "deben ser capaces de demostrar, a petición de la Superintendencia de Industria y Comercio, que han implementado medidas apropiadas y efectivas". F1 art. 4 literal g: medidas "para otorgar seguridad a los registros evitando su adulteración, pérdida, consulta, uso o acceso no autorizado o fraudulento". |
| 10. Verificación y pendientes | Textos leídos con asistencia de IA, sin verificación humana. Pendiente: que C7 aclare si una regla funcional vale como una de las cinco reglas, y el papel de AI DataGuard como responsable o encargado en un despliegue real. |

## 5. Obligaciones legales, controles funcionales y políticas organizacionales

| Tipo | Qué es | Qué está respaldado por una fuente leída | Qué es propuesta |
|---|---|---|---|
| **Obligación legal** | Deber que surge de una disposición | Los textos de las fuentes de la sección 2 | Cómo se aplican a AI DataGuard: toda la aplicación es [IP] |
| **Control funcional** (`RJ-05`, CT-01 a CT-05) | Comportamiento del propio sistema | Principios y medidas generales de seguridad y demostración (F1, F8, F4) | Cada control concreto es [RF]; ninguna fuente leída lo exige expresamente |
| **Política organizacional** | Regla que define el Administrador de la organización | Solo el deber de un manual interno de datos personales (F1 art. 17 literal k) | Cualquier política sobre el uso de IA generativa es [PC] |

Ni los niveles (Pública, Interna, Confidencial, Restringida) ni las marcas son categorías legales; son [RF].

## 6. Respaldo de `RJ-05`

| Ancla verificada | Qué dice | Qué no dice |
|---|---|---|
| F1 art. 4 literales f, g y h; art. 17 literal d; art. 18 literales b y j | Acceso restringido, seguridad, reserva de la información y conservación bajo condiciones de seguridad | No menciona enmascarado ni descarte |
| F8 2.2.2.25.2.1 | La recolección "deberá limitarse a aquellos datos personales que son pertinentes y adecuados para la finalidad" | No habla del contenido analizado de forma transitoria |
| F8 2.2.2.25.2.8 | Tratar los datos solo "durante el tiempo que sea razonable y necesario", suprimirlos al cumplirse la finalidad y documentar los procedimientos de conservación y supresión | Es un deber de responsables y encargados respecto de sus propias finalidades, con salvedad de obligaciones legales o contractuales |
| F8 2.2.2.25.6.1 y 2.2.2.25.6.2 | Demostrar medidas apropiadas y efectivas, proporcionales a la naturaleza jurídica, el tamaño empresarial (micro, pequeña, mediana o gran empresa), la naturaleza de los datos, el tipo de tratamiento y los riesgos | No dice cuáles medidas |
| F4 numerales III, VI y VIII | Gestión de riesgos, privacidad desde el diseño y por defecto, y medidas de seguridad "auditables" | Es una instrucción de la SIC cuya naturaleza es [IP]; el numeral IV se refiere al diseño de IA de alto riesgo |

**Conclusión preliminar (a validar):** `RJ-05` puede describirse como un conjunto de controles funcionales alineados con las obligaciones generales de seguridad, confidencialidad, limitación de la recolección y conservación y responsabilidad demostrada. La minimización puede citarse con respaldo del art. 2.2.2.25.2.1 y del art. 2.2.2.25.2.8, con aplicación [IP], y no solo como principio del proyecto.

**Lo que no se afirma:** que una norma exija específicamente el enmascarado, el descarte automático, el historial que no se sobrescribe o la revisión humana. La revisión humana tampoco figura como mandato en la Circular de 2024. El control de descarte puede describirse como alineado con la supresión al cumplirse la finalidad, no como exigido por ella. Los controles son autodeclarados por el sistema y se corroboran con pruebas independientes.

## 7. Consulta C7 (abierta, docente)

**C7:** ¿las cinco reglas exigidas deben tener fundamento jurídico directo, o se admiten reglas funcionales y controles con respaldo indirecto?

Insumos para la decisión del docente, sin resolverla:

| Regla | Fundamento verificado en el texto | Categoría (principal; secundarias) |
|---|---|---|
| `RJ-01` | Directo (F1, F8, F10) | Principal [IP]; secundaria [OL] |
| `RJ-02` | Directo (F5, F6) | Principal [IP]; secundarias [OL], [RF] |
| `RJ-03` | Parcial (F1 art. 17 literal k y F8 2.2.2.25.3.1, solo para datos personales) | Principal [IP]; secundaria [PC] |
| `RJ-04` | Directo (F1, F8) | Principal [IP]; secundarias [OL], [RF] |
| `RJ-05` | Indirecto, con anclajes verificados (F1, F8) | Principal [RF]; secundaria [IP] |

## 8. Trazabilidad: reglas, capacidades, requisitos, pruebas y escenarios

Pruebas y escenarios están **previstos, no ejecutados**. Fuente: `design.md` y `specs/`.

| Regla | Capacidades OpenSpec | Requisitos | Pruebas | Escenarios |
|---|---|---|---|---|
| `RJ-01` | `document-analysis`, `information-classification`, `compliance-policies` | DOC-05, CLA-01, CLA-04, POL-03 | CP-01, CP-02, CP-12 | ED-1 |
| `RJ-02` | `document-analysis`, `information-classification`, `compliance-policies` | CLA-02, CLA-04, POL-03, POL-06 | CP-02, CP-03, CP-05 | ED-2, ED-3 |
| `RJ-03` | `compliance-policies` | POL-06, POL-10, POL-11 | CP-05, CP-04 (adicional) | ED-3 |
| `RJ-04` | `compliance-policies`, `ai-provider-catalog` | POL-04, POL-05, PRV-02, PRV-03 | CP-01, CP-07, CP-12 (mínimos), CP-06 (adicional) | ED-1, ED-2 |
| `RJ-05` | `document-analysis`, `compliance-policies`, `assessment-reports` | POL-07, DOC-04, DOC-06, DOC-08, REP-03, REP-07 | CP-02, CP-08, CP-09, CP-10, CP-12 (mínimos), CP-13 (adicional) | ED-1, ED-2, ED-3 |

## 9. Fundamentos no verificados o pendientes

- Verificación humana de todas las fuentes y contraste con el Diario Oficial o una fuente primaria (SUIN, por ejemplo).
- La versión consolidada vigente de la Circular Única de la SIC y su lista de países adecuados (F9). Una noticia de 2026 menciona países que la SIC recomendaría añadir; no se verificó y no se usa.
- Notas de vigencia que no pudieron leerse: art. 4 literal g de la Ley 1581 y notas del editor de la Ley 256; vigencia desplegable del Decreto 1074 y alcance del Decreto 255 de 2022.
- La Gaceta Oficial de la CAN para la Decisión 486 y la forma de incorporación de la norma andina en Colombia.
- La confirmación de la discrepancia sobre el art. 25 del Decreto 1377 (sección 3.1).
- Papel jurídico de la organización y del proveedor (responsable, encargado, tercero).
- Aplicabilidad de la Ley 1266 de 2008 a los datos financieros que AI DataGuard detecta; el art. 2 literal e de la Ley 1581 excluye las bases reguladas por la Ley 1266.
- Naturaleza jurídica y fuerza vinculante de la Circular de 2024.
- Si las pymes deben inscribirse en el Registro Nacional de Bases de Datos.
- Fuente para la confidencialidad pactada por contrato o reglamento interno.
- Jurisprudencia y doctrina posteriores de la SIC y del Consejo de Estado, incluida la existencia de suspensiones o nulidades de las Circulares. La búsqueda realizada no encontró ninguna, lo que no prueba su ausencia.
- La Constitución, art. 15, se menciona en F1 y no se consultó directamente. La Ley 1273 de 2009 (F7) se cita solo como referencia.

## 10. Estado de sincronización con OpenSpec

`initial-mvp` se actualizó el 12 nov con las decisiones del equipo D1 a D9. Estado de las observaciones de esta matriz:

| # | Observación | Estado |
|---|---|---|
| 1 | `CLA-01`: lista de sensibilidad alta y datos de menores | **Atendida (DC-18):** lista ampliada con las categorías del art. 5 e indicios de datos de menores. La equivalencia legal sigue pendiente de E2. |
| 2 | `POL-03`: `RJ-01` ante datos sensibles o de menores | **Atendida:** «requiere revisión humana» con advertencia reforzada, sin afirmar una prohibición ni que el sistema verifique autorizaciones. Es una decisión funcional del equipo. |
| 3 | `POL-04`: ubicación y retención del proveedor | **Atendida (DC-15):** el uso para mejorar modelos interviene en el resultado; retención, exclusión y ubicación se muestran como información para revisión humana. El sistema no determina la licitud de una transferencia o transmisión. |
| 4 | `PRV-01`: papel del proveedor | **Abierta:** el catálogo no registra si el proveedor actúa como encargado, responsable o tercero; sigue siendo interpretación pendiente. |
| 5 | `POL-02`: una sola categoría por regla | **Atendida (DC-16):** categoría principal y secundarias. |
| 6 | Tipo de `RJ-03` | **Abierta:** OpenSpec la mantiene como regla jurídica preliminar; aquí su categoría principal es [IP] y la secundaria [PC] (C7). |
| 7 | Tema y término de `RJ-05` | **Atendida (DC-21):** «controles funcionales transversales»; la minimización tiene anclaje en 2.2.2.25.2.1 y 2.2.2.25.2.8, con aplicación [IP]. |
| 8 | `RJ-02`: correspondencia entre marcas y resultados | **Abierta:** es [RF] sin respaldo legal; sin cambios. |
| 9 | Perfiles | **Atendida (DC-14):** dos perfiles; el responsable de cumplimiento es una responsabilidad del Administrador. |
| 10 | Fuentes candidatas de `proposal.md` | **Atendida:** la propuesta describe las fuentes leídas con asistencia de IA y sin verificación humana. |
| 11 | Forma de cita del Decreto 1377 | **Sin cambio necesario:** OpenSpec no lo cita; si lo hiciera, debe usar la numeración del Decreto 1074. |

## 11. Preguntas pendientes

**Para el docente:**
- **C7:** si las cinco reglas requieren fundamento jurídico directo.
- **C5:** si "seguimiento a compromisos" es obligatorio.
- Si espera una plantilla específica de matriz y qué grado de interpretación jurídica se admite a los estudiantes.
- Qué criterio define una fuente "verificada" y si se requiere revisión de un abogado.
- Aprobación de E2: no consta fecha.

**Para el equipo:**
- Que el Integrante 2 (por registrar) verifique cada fuente directamente y confirme los extractos.
- Decidir si el catálogo debe registrar el papel del proveedor (observación 4).
- Decidir los temas finales de las reglas frente a los siete puntos de dolor del Excel (tarea 2.4) y la categoría principal definitiva de cada una.
- Informar al docente de las rutas oficiales (DC-20): `legal-matrix.md` corresponde a `matriz-reglas.md` del Excel, y las fuentes están en la sección 2 de esta matriz, en lugar de `fuentes.md`.

## 12. Registro de las correcciones aplicadas

| ID | Estado | Dónde |
|---|---|---|
| J-01 | Atendida documentalmente; confirmación en fuente primaria pendiente | 3.1 |
| J-02 | Atendida documentalmente | 3.1 y forma de cita |
| J-03 | Atendida documentalmente | RJ-03 |
| J-04 | Atendida documentalmente | RJ-02 |
| J-05 | Atendida documentalmente; Gaceta de la CAN no abierta | Fuentes F5; RJ-02 |
| J-06 | Atendida documentalmente; la aplicación a proveedores de IA sigue [IP] | 3.2; RJ-04 |
| J-07 | Parcial: la versión consolidada vigente de la Circular Única no se abrió | F9; RJ-04 |
| J-08 | Atendida documentalmente; aplicación [IP] | 3.3; RJ-01 |
| J-09 | Atendida documentalmente; aplicación [IP] | 3.3; RJ-01 |
| J-10 | Atendida documentalmente; aplicación [IP] | 6; RJ-05 |
| J-11 | Atendida documentalmente | 3.4; 6 |
| J-12 | Atendida documentalmente; naturaleza vinculante [IP] | 3.4 |
| J-13 | Atendida documentalmente | 3.4; F11 |
| J-14 | Atendida documentalmente | F2 |
| J-15 | Atendida documentalmente; extractos pendientes de contraste humano | Estructura de la sección 4 |
| J-16 | Atendida documentalmente | RJ-01 y RJ-05 |
| J-17 | Parcial: retirada del fundamento; sigue sin verificarse | RJ-03; sección 9 |
| J-18 | **Pendiente:** la nota de vigencia no pudo leerse | Fuentes F1; sección 9 |
