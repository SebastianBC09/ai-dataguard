# Ficha de proyecto E1: AI DataGuard

**Etapa E1, selección y delimitación** · Contexto Legal de la Ingeniería · UNINPAHU · 12 de noviembre de 2026
**Equipo:** 3 integrantes (nombres y responsabilidades por registrar)
**Estado: BORRADOR ACADÉMICO, PENDIENTE DE APROBACIÓN DOCENTE.** E1 y E2 no están aprobadas.

*Convención:* **[Docente]** = requisito expreso de la guía docente; **[Equipo]** = propuesta del equipo sujeta a revisión.

## 1. Nombre y descripción

**AI DataGuard** es una aplicación de apoyo preventivo para quien use inteligencia artificial generativa en su trabajo. Antes de compartir un texto con una de estas herramientas, advierte si contiene datos personales o información confidencial, lo evalúa frente a cinco reglas jurídicas preliminares y a las políticas de la organización, muestra las condiciones del proveedor y genera un informe. **Apoya la decisión humana; no certifica cumplimiento jurídico ni sustituye asesoría jurídica** [Docente].

## 2. Problema concreto

Los trabajadores pueden introducir datos personales o información reservada en herramientas de IA generativa sin conocer las condiciones del proveedor ni sus implicaciones jurídicas. En las pymes se agrava por la falta de políticas internas y de trazabilidad. El plan de trabajo señala como puntos de dolor la exposición de datos, la divulgación de información reservada y la ausencia de políticas; sus pesos relativos son una estimación del equipo, sin fuente.

## 3. Justificación

- **Académica** [Docente]: se exige un problema real, un usuario concreto, una aplicación de principio a fin que guarde información y genere un informe, y un plan verificable.
- **Jurídica** [Equipo]: las normas aplicables se identificaron preliminarmente en E2, sin verificación humana ni aprobación.
- **Organizacional** [Equipo]: ofrece a las pymes un control preventivo y explicable, sin conservar los documentos originales.

## 4. Usuarios objetivo

Trabajadores y administradores de organizaciones colombianas, principalmente pymes. Para el MVP [Equipo] hay **dos perfiles**:

| Perfil | Necesidad |
|---|---|
| Trabajador | Evaluar un contenido antes de usarlo con IA y entender cada alerta. |
| Administrador | Definir políticas, revisar casos pendientes y consultar la trazabilidad. La revisión de cumplimiento es una responsabilidad del Administrador, no un tercer perfil. |

**Caso hipotético de referencia** [Equipo]: una pyme colombiana de servicios administrativos o comerciales. Es un supuesto, no una organización real.

## 5. Objetivos

**General:** apoyar a trabajadores y administradores de pymes colombianas para prevenir la divulgación no autorizada de datos personales e información confidencial mediante IA generativa, con revisión humana y explicabilidad.

**Específicos** [Equipo]:
1. Detectar y explicar indicadores de datos personales e información confidencial.
2. Clasificar la sensibilidad y evaluar el contenido frente a las reglas y políticas.
3. Informar las condiciones de los proveedores de IA, con fuente y fecha.
4. Registrar de forma mínima evaluaciones y decisiones, y generar un informe exportable.
5. Cumplir los mínimos [Docente]: 5 reglas, 10 pruebas y 3 escenarios.

## 6. Alcance del MVP y exclusiones

**Cinco capacidades** [Equipo]: análisis de texto directo y PDF complementario (`document-analysis`); clasificación de sensibilidad (`information-classification`); evaluación de reglas jurídicas preliminares, políticas y controles funcionales (`compliance-policies`); catálogo de proveedores de IA (`ai-provider-catalog`); informes, registro mínimo y trazabilidad (`assessment-reports`).

**Exclusiones:** no certifica cumplimiento [Docente]; sin pagos, IA opcional y solo datos de ejemplo sintéticos [Docente]; no envía contenido sensible a terceros [Equipo]; sin otras capacidades ni despliegue en producción. **No se selecciona tecnología**: la decisión está aplazada.

## 7. Escenarios de demostración (borrador)

- **ED-1, privacidad:** un trabajador evalúa un texto sintético con datos personales y elige un proveedor; se muestra que no se guarda el contenido.
- **ED-2, revisión humana:** un texto sintético que representa un documento, marcado como reservado y sin proveedor, queda pendiente; el administrador decide y justifica.
- **ED-3, administración:** un administrador crea una política, vuelve a someter un texto, consulta la trazabilidad y exporta el informe.

## 8. Estado y decisiones pendientes

E1 y E2 están **pendientes de aprobación docente**; no consta fecha. Pruebas y escenarios están previstos, no ejecutados, y el MVP no está implementado.

| Decisión | Quién | Estado |
|---|---|---|
| **C5**: si "seguimiento a compromisos" es obligatorio | Docente | Consulta pendiente |
| **C7**: si las cinco reglas requieren fundamento jurídico directo | Docente | Consulta pendiente |
| **C4**: si los 3 escenarios van en esta ficha o solo en E8 | Docente | Pendiente; se incluyen como borrador |
| **C3**: selección tecnológica | Equipo y docente | Aplazada; antes de E5 |

Nombre oficial del archivo: `project-charter.md` (el Excel indica `ficha-e1.md`). Faltan: nombres y responsabilidades de los integrantes, y el criterio de aprobación del docente.
