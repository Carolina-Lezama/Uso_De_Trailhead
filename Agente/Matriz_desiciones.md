# URGENCIA 1: Atender el Feedback Exacto + Continuidad Humana (Opción 3)

1. Demostrar apertura de Solicitud_CFDI\_\_c:

- Configura un formato de página (Page Layout) limpio en Salesforce para el objeto Solicitud_CFDI\_\_c.
- En la demostración, muestra el momento exacto en que abres el registro recién creado desde la vista de lista, destacando los campos poblados por la IA: RFC, CP, Régimen, Correo y la relación con la Linea_de_Captura\_\_c.

2. Demostrar Continuidad con el Ejecutivo Humano (El cambio clave):

-     Configura la vista de la Consola de Servicio (Service Console), construir/configurar es la Pantalla del Ejecutivo de Soporte (Perspectiva Humana).
-     Muestra la pantalla desde la perspectiva del ejecutivo humano: abre el registro de Log_de_Auditoria_IA__c o el Caso generado.
-     Muestra cómo el ejecutivo ve la alerta, el motivo del escalamiento ("cobro doble"), el historial de la conversación y el número de folio entregado al ciudadano.

- ¿Se deben agregar Dashboards? SÍ, pero uno muy sencillo (opcional, de 10 minutos). Un Dashboard nativo en Salesforce con 2 gráficos ("Total de Escalamientos por Motivo" y "Estatus de Solicitudes CFDI") le dará un impacto visual de nivel directivo a la presentación final.

# Plan de trabajo para el PASO 1

## Paso 1.1: Configuración de la Página de Detalle de Solicitud_CFDI\_\_c

- Por qué corregirlo: En la normativa fiscal del SAT (CFDI 4.0), el Uso del CFDI es un campo obligatorio (ej. G03 - Gastos en general o CP01 - Sin efectos fiscales). Dejarlo vacío invalida el registro para timbrado.

- Cómo solucionarlo: Modifica la instrucción en las acciones del agente para que solicite explícitamente el Uso de CFDI, o tambien configuraremos una predeterminada(si no se proporciona una el agente debe preguntar si continua con CP01 - Sin efectos fiscales como Uso del CFDI)

## PARTE 2: Ajuste en el Agente de Agentforce

- Objetivo: Dictar las reglas de interacción conversacional para que el agente pida el dato o sugiera el valor por defecto.
- Entra a Configuración (Setup) > Agentforce Studio / Agentes (Agents).
- Abre tu agente conversacional y entra al Tópico/Acción (Topic / Action) responsable de la gestión de facturas CFDI (ej. Facturación y CFDI).
- Entra a editar las Instrucciones (Instructions) del Tópico o de la Acción de creación de CFDI y actualiza las reglas con el siguiente texto:

## PARTE 3: Visualizacion

- Entra a Configuración (Setup) > Gestor de Objetos (Object Manager) > Solicitud_CFDI\_\_c.
  Dirígete a Diseños de página (Page Layouts).

Organiza los campos en dos secciones claras:

- Sección 1: Información General del Trámite (Linea_de_Captura**c, Estatus_Emision**c, Fecha/Hora).
- Sección 2: Datos FiscalesExtraídos por IA (RFC**c, Codigo_Postal**c, Regimen_Fiscal**c, Uso_CFDI**c, Correo_Electronico\_\_c).
- Entra a Páginas de registros Lightning (Lightning Record Pages) para Solicitud_CFDI\_\_c, activa un diseño de 2 columnas con panel de aspectos destacados (Highlights Panel) y guarda/activa como predeterminado de la organización.

## PARTE 4: Configurar la Página de Registro Lightning

- En el menú lateral izquierdo de tu pantalla, haz clic en Páginas de registros Lightning (está justo debajo de Formatos de página).
- Haz clic en el botón Nuevo.
- Selecciona Página de registro y haz clic en Siguiente.
- Completa la información inicial:
- Etiqueta: Página de Solicitud CFDI
- Objeto: Selecciona Solicitud CFDI
- Haz clic en Siguiente.
- Selecciona la plantilla: Encabezado y dos columnas (o Header and Two Columns) y haz clic en Finalizar.
- Agregar componentes en el lienzo:
- En el menú de componentes de la izquierda, busca Panel de aspectos destacados (Highlights Panel) y arrástralo a la región superior (el Encabezado).
- Busca el componente Detalles del registro (Record Detail) y arrástralo a la columna izquierda.
- (Opcional) En la columna derecha, puedes arrastrar el componente Listas relacionadas (Related Lists).
- Haz clic en Guardar (esquina superior derecha).
- Se abrirá una ventana o botón de Activación:
- Haz clic en Activar.
- Selecciona la pestaña Predeterminado de la organización (Org Default).
- Haz clic en Asignar como predeterminado de la organización.
- Haz clic en Guardar.

## Paso 1.2: Configuración de la Perspectiva del Ejecutivo Humano (Continuidad)

Entra al Gestor de Objetos en Log_de_Auditoria_IA\_\_c.

Asegúrate de que el Diseño de página (Page Layout) muestre de forma prominente:

- Folio_Log\_\_c (Encabezado principal).
- Motivo_Escalamiento\_\_c (Campo de texto enriquecido/largo bien visible).
- Correo_Ciudadano**c y Fecha_Hora**c.

## Paso 1: Organizar el Formato de Página de Log_de_Auditoria_IA\_\_c

Vamos a asegurarnos de que la ficha del Log de Auditoría muestre de forma destacada el motivo de escalamiento y el folio.

- Entra a Configuración (Setup) > Gestor de Objetos (Object Manager) > Log_de_Auditoria_IA\_\_c.
- Entra a Formatos de página (Page Layouts).

Asegúrate de que los campos clave estén bien visibles en dos columnas:

- Columna Izquierda: Folio_Log (o Nombre del Log), Motivo_Escalamiento (ej. "cobro doble"), Correo_Ciudadano.
- Columna Derecha: Fecha_Hora, Estatus_Atencion, Propietario.
- Haz clic en Guardar.

## Paso 2: Configurar la Consola de Servicio (Service Console)

- En la esquina superior izquierda de Salesforce, haz clic en el Iniciador de aplicaciones (el icono de 9 puntos o "Waffle").

- Busca y selecciona Consola de Servicio (Service Console).

- En la barra de navegación superior de la Consola de Servicio, haz clic en la flecha hacia abajo junto a las pestañas y selecciona Editar (o el icono de lápiz) para agregar pestañas.

- Agrega el objeto Log_de_Auditoria_IA\_\_c para que sea una de las pestañas principales de navegación.

- Abre la pestaña Log_de_Auditoria_IA\_\_c y crea una vista de lista llamada "Escalamientos Pendientes IA" (filtrando por los creados hoy).

## Paso 1.3: Dashboard de Control Directivo (Potenciador Visual)

- Crea un Informe (Report) sobre Log_de_Auditoria_IA**c agrupado por Motivo_Escalamiento**c.
- Crea un Informe (Report) sobre Solicitud_CFDI**c agrupado por Estatus_Emision**c.
- Crea un Panel (Dashboard) denominado "Centro de Mando - Atención e Impuestos IA" con 2 componentes visuales (Gráfico de barras y Gráfico de dona).

## Parte 3: Panel "Centro de Mando - Atención e Impuestos IA"

- Abre la pestaña Paneles (Dashboards) en la barra de navegación y haz clic en Nuevo panel.

Configura los datos iniciales:

- Nombre: Centro de Mando - Atención e Impuestos IA
- Carpeta: Paneles públicos
- Haz clic en Crear.

### Agregar Componente 1 (Gráfico de Barras):

- Haz clic en + Componente.
- Selecciona el informe Informe: Escalamientos por Motivo y presiona Seleccionar.
- En el panel derecho, elige el icono de Gráfico de barras (horizontal o vertical).
- Verifica que el Eje Y sea Motivo Escalamiento y el Eje X sea Recuento de filas.
- Haz clic en Agregar.

### Agregar Componente 2 (Gráfico de Dona):

- Haz clic en + Componente.
- Selecciona el informe Informe: CFDI por Estatus y presiona Seleccionar.
- En el panel derecho, elige el icono de Gráfico de dona.
- Verifica que la métrica de valor sea Recuento de filas y el segmento sea Estatus Emision.
- Haz clic en Agregar.

Finalizar:

- Reorganiza los bloques arrastrándolos si deseas ajustar la maquetación.
- Haz clic en Guardar y luego en Listo.

## Paso 1: Crear Fórmulas de Flujo para los datos de la cita

Fecha_Cita: Fórmulada como DATETIMEVALUE(TODAY() + 1) (asigna automáticamente el día siguiente).

Link_Meet: Fórmula que concatene [https://meet.google.com/](https://meet.google.com/) + un código aleatorio o el Id del Log de Auditoría.

## Paso 2: Diseñar una Plantilla de Texto HTML (Text Template)

Crea un recurso dentro del flujo de tipo Plantilla de texto en formato HTML para darle un diseño profesional corporativo:

Asunto: Confirmación de cita con especialista - Folio {!$Record.Name}

Cuerpo:

Hola,

Hemos recibido tu solicitud de escalamiento por el motivo: {!$Record.Motivo_Escalamiento\_\_c}.

Un agente humano dará seguimiento a tu caso. Hemos agendado una sesión de atención prioritaria:

Fecha y Hora: {!Formula_Fecha_Cita}

Enlace de acceso: Unirse a la sesión en Google Meet

Saludos,

Centro de Atención e Impuestos IA

## Paso 3: Agregar la Acción "Enviar correo electrónico" en el Flujo

En el flujo donde creas el registro de Log_de_Auditoria_IA\_\_c:

Agrega el elemento Acción (Action).

Selecciona Enviar correo electrónico (Send Email).

Configura los parámetros:

Cuerpo del correo: {!Plantilla_Texto_HTML}

Asunto: Confirmación de atención humana - Folio {!$Record.Name}

Dirección de correo del destinatario: {!$Record.Correo_Solicitante\_\_c}

Procesar el cuerpo como HTML: Verdadero ($GlobalConstant.True)
