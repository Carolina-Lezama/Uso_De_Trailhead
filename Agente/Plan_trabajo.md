# Plan Maestro de Trabajo: Agente Gubernamental de Conciliación y Facturación (Agentforce)

## Fase 1: Fundamentos y Modelo de Datos en Salesforce CRM

Justificación: Salesforce funciona como una base de datos relacional. Antes de que el Agente pueda consultar o modificar información, debemos construir las "tablas" (Objetos) y "columnas" (Campos) donde se almacenarán las líneas de captura, las solicitudes de CFDI y el historial de auditoría.

## 1.1. Creación de Objetos Personalizados (Custom Objects)

En Salesforce, ve a Setup (Configuración) > Object Manager (Administrador de objetos) > Create > Custom Object.

1. Objeto Linea_de_Captura\_\_c (Línea de Captura de Pago)

- Campo de nombre de objeto: Numero_de_Folio (Text)
- Campos personalizados:
- Monto\_\_c (Currency)
- Estatus\_\_c (Picklist: Pendiente, Pagado, Procesado, Cancelado)
- Fecha_de_Pago\_\_c (Date/Time)
- Servicio\_\_c (Text: ej. "Licencia de Conducir", "Predial")
- Ciudadano\_\_c (Lookup al objeto estándar Contact o Account)

2. Objeto Solicitud_CFDI\_\_c (Solicitud de Facturación)

- Campo de nombre de objeto: Numero_Solicitud (Auto-Number: CFDI-{0000})
- Campos personalizados:
- RFC\_\_c (Text)
- Regimen_Fiscal\_\_c (Text)
- Codigo_Postal\_\_c (Text)
- Uso_CFDI\_\_c (Text)
- Correo_Notificacion\_\_c (Email)
- Estatus_Factura\_\_c (Picklist: Solicitado, En Proceso, Emitido, Rechazado)
- Linea_de_Captura**c (Lookup a Linea_de_Captura**c)

3. Objeto Log_de_Auditoria_IA\_\_c (Trazabilidad y Event Logging)

- Campo de nombre de objeto: Nombre_Log (Auto-Number: LOG-{0000})
- Campos personalizados:
- Accion_Ejecutada\_\_c (Text: ej. "Consulta de Estatus", "Bloqueo de Doble Pago", "Creación CFDI")
- Detalle\_\_c (Long Text Area: Descripción detallada de lo ejecutado)
- Id_Ciudadano\_\_c (Text o Lookup a Contact)
- Fecha_Hora\_\_c (Date/Time)
- Agente_Invocador\_\_c (Text: "Agentforce Bot")

## Fase 2: Capa de Inteligencia y Conocimiento (Knowledge RAG)

Justificación: Cumple con la Dimensión 1 (Knowledge RAG). El agente no debe inventar políticas del gobierno. Cargarás artículos oficiales para que el LLM responda basándose únicamente en esta base de conocimientos.

## 2.1. Habilitar Salesforce Knowledge

1. Ve a Setup > Knowledge Settings y marca la casilla Enable Knowledge.

2. Asigna la licencia de usuario Knowledge a tu usuario en Setup > Users > tu usuario > Knowledge User (marcar).

## 2.2. Creación e Indexación de Artículos de Conocimiento

Crea tres artículos de conocimiento en Knowledge App:

1. Artículo 1: Politica_Pagos_No_Reembolso
   o Contenido: "De acuerdo con el Artículo 45 del Código Fiscal del Estado, todo pago realizado a líneas de captura oficiales no es sujeto a reembolso directo por canal digital. Si realiza un pago duplicado, deberá iniciar un trámite presencial en la Secretaría de Finanzas."
2. Artículo 2: Requisitos_Emision_CFDI
   o Contenido: "Para la emisión del Comprobante Fiscal Digital por Internet (CFDI) se requiere: RFC activo, Código Postal del domicilio fiscal, Régimen Fiscal y Uso de CFDI. La solicitud debe realizarse dentro del mismo mes en que se efectuó el pago."
3. Artículo 3: Tiempos_Acreditacion_Servicios
   o Contenido: "Los pagos realizados en ventanilla bancaria tardan de 24 a 48 horas hábiles en reflejarse. Los pagos en línea mediante tarjeta de crédito o débito se acreditan de forma inmediata."

## 2.3. Configuración de Agent Search / Data Cloud

1. Publica los tres artículos (Publish).

2. Asegúrate de que el perfil del Agente tenga acceso de lectura a Knowledge.

## Fase 3: Capa de Acción y Trazabilidad (Flow Builder)

Justificación: Cumple con la Dimensión 2 (Agentic Flows) y la Dimensión 3 (Event Logging). Los Flows son scripts visuales (pro-code/no-code) que el agente ejecuta como herramientas cuando decide tomar una acción.

## 3.1. Flow 1: Verificar Estatus y Bloquear Pago Duplicado (Autolaunched Flow)

• Propósito: Recibir una línea de captura, revisar si ya está pagada y evitar que el ciudadano vuelva a pagar.

• Entradas (Variables con "Available for input"): var_NumeroFolio (Text).

• Pasos del Flow:

1. Get Records: Buscar en Linea_de_Captura\_\_c donde Numero_de_Folio sea igual a var_NumeroFolio.
2. Decision:

-     ¿Existe y está Pagado? -> Asignar mensaje de salida: "El folio X ya cuenta con un pago verificado el día Y. No vuelva a realizar el pago."
-     ¿Existe y está Pendiente? -> Asignar mensaje de salida: "El folio X está listo para pago."
-     ¿No existe? -> Asignar mensaje de salida: "El folio no fue encontrado en el sistema."

3. Create Record (Event Logging Integrado): Crear un registro en Log_de_Auditoria_IA\_\_c guardando la acción: "Consulta de Folio: " + var_NumeroFolio.

• Salidas (Variables con "Available for output"): var_MensajeRespuesta (Text), var_EstatusPago (Text).

## 3.2. Flow 2: Registrar Solicitud de CFDI (Autolaunched Flow)

- Propósito: Recibir los datos fiscales extraídos por el agente y crear el registro de facturación en la BD.
- Entradas: var_Folio, var_RFC, var_CP, var_Regimen, var_Correo.
- Pasos del Flow:

1. Get Records: Validar que la línea de captura existe y su estatus sea 'Pagado'.
2. Decision:

- Si NO está pagado: Regresar error "No se puede generar CFDI para un pago no verificado".
- Si está pagado:
- Create Record: Insertar en Solicitud_CFDI\_\_c con los datos recolectados.
- Update Record: Cambiar estatus de Linea_de_Captura\_\_c a 'Procesado'.
- Create Record (Event Logging): Insertar en Log_de_Auditoria_IA\_\_c con la nota "CFDI Creado exitosamente para el RFC " + var_RFC.
-     Salidas: var_ResultadoCFDI (Text), var_NumeroSolicitudCFDI (Text).

## Fase 4: Configuración del Agente en Agentforce (Agent Builder)

Justificación: Es la "capa cerebral". Aquí se le enseña al agente cómo razonar mediante intenciones (Topics), qué reglas seguir (Instructions) y qué herramientas usar (Actions).

## 4.1. Acceso a Agent Builder

1. En Setup, busca Agents (o Agent Studio / Agent Builder).
2. Selecciona New Agent > Service Agent (o Agente de Servicio Personalizado).
3. Asigna el nombre: Agente_Atencion_Ciudadana_Puebla.

## 4.2. Definición del Topic 1: Gestion_de_Pagos_y_Folios

-     Classification Description: "Úsalo cuando el usuario pregunte sobre el estatus de su pago, desee saber si su línea de captura fue acreditada o intente pagar de nuevo un servicio."
-     Instructions (Instrucciones del Agente):
-     "Solicita siempre al usuario su número de línea de captura (folio de 24 dígitos o identificador único)."
-     "Una vez obtenido el folio, invoca la acción 'Verificar Estatus de Pago'."
-     "Si la respuesta indica que el folio ya está PAGADO, advierte expresamente al usuario que no debe realizar otro pago porque no existen reembolsos digitales."
-     "Nunca adivines el estatus de un pago sin haber ejecutado la acción."
-     Actions vinculadas: Asignar el Flow Verificar Estatus y Bloquear Pago Duplicado.

## 4.3. Definición del Topic 2: Facturacion_y_CFDI

- Classification Description: "Úsalo cuando el usuario requiera la emisión de su comprobante fiscal, factura o CFDI sobre un trámite realizado."
- Instructions:
- "Solicita en orden los siguientes datos obligatorios: Folio de pago, RFC, Código Postal y Correo electrónico."
- "Consulta los artículos de Knowledge sobre requisitos de CFDI si el usuario expresa dudas sobre su régimen o parámetros."
- "Llama a la acción 'Registrar Solicitud de CFDI' únicamente cuando tengas los 4 datos obligatorios."
- "Muestra al usuario el número de solicitud de CFDI generado como confirmación."
- Actions vinculadas: Asignar el Flow Registrar Solicitud de CFDI.

## 4.4. Reglas de Inviolabilidad (Guardrails / System Instructions)

- En la sección System Instructions (Instrucciones Generales del Agente), agrega estas reglas globales:
- "1. No generes información financiera ni simules pagos sin consultar la base de datos."
- "2. Si el usuario intenta forzar una devolución o reembolso, responde basándote estrictamente en la política de no reembolsos y no prometas transacciones fuera de sistema."
- "3. Si el usuario realiza solicitudes fuera del ámbito gubernamental o muestra frustración extrema por cobros indebidos, escala la conversación inmediatamente a un agente humano."

## Fase 5: Capa de Confianza y Escalamiento Humano (Omni-Channel)

Justificación: Cumple con la Dimensión 4 (Confianza y Escalamiento). Si el agente encuentra un escenario ambiguo o un usuario con cobros duplicados no resolutivos, debe transferir sin perder el contexto.

## 5.1. Configuración de Omni-Channel

1. En Setup, busca Omni-Channel Settings y activa Omni-Channel.
2. Crea una Service Channel para Chat / Messaging.
3. Crea una Queue (Cola de atención) llamada Atencion_Humana_Especializada.
4. Asigna a tu usuario de desarrollo a esa cola.

## 5.2. Configuración del Topic de Escalamiento (Escalation / Fallback)

5. En Agent Builder, configura la acción nativa de escalamiento (Escalate to Agent).
6. Vincula la acción a la cola Atencion_Humana_Especializada.
7. Define la instrucción: "Si el usuario solicita hablar con una persona, reporta una anomalía no cubierta por las acciones o exige una aclaración de saldo de más de 72 horas, invoca la transferencia a agente humano."

## Escenario de Prueba 1 – Consulta de Estatus de Pago

Prompt de entrada:

"Hola, me gustaría revisar el estatus de mi pago de la línea de captura 123456789012345678901234."

Qué debes verificar en la respuesta:

- Tema activado: Debe clasificar la consulta dentro de Gestion_de_Pagos_y_Folios.
- Acción ejecutada: Debe llamar a la acción Verificar Estatus de Pago.
- Mensaje del agente: Si el flujo devuelve que está pagado, debe incluir la advertencia de que no existen reembolsos digitales.

## Escenario de Prueba 2 – Solicitud de Facturación / CFDI

Prompt de entrada:

"Quiero solicitar la factura CFDI de mi pago realizado."

Qué debes verificar en la respuesta:

- Tema activado: Debe clasificar la consulta dentro de Facturacion_y_CFDI.
- Comportamiento del agente: La IA te solicitará secuencialmente o en conjunto los datos faltantes: Folio de pago, RFC, Código Postal y Correo electrónico.
- Segunda interacción: Al enviarle datos ficticios (ej. Folio: 12345, RFC: XAXX010101000, CP: 72000, Correo: test@example.com), debe ejecutar la acción Registrar Solicitud de CFDI y devolver el número de confirmación.


## Escenario de Prueba 3 – Escalamiento a Atención Humana
Prompt de entrada:

"Necesito hablar urgentemente con una persona, mi caso tiene una anomalía de saldo."

Qué debes verificar en la respuesta:

- Tema activado: Debe transferir la conversación al tema # Escalation.
- Acción ejecutada: Debe invocar la acción nativa escalate_to_human.

## Fase 6: Pruebas, Trazabilidad y Calibración (Reasoning Logs)

Justificación: Garantiza la solidez antes de la presentación. Permite verificar la ejecución paso a paso del motor Atlas.

## 6.1. Ejecución de Matriz de Pruebas en Agent Builder
Escenario de Prueba Entrada del Usuario Comportamiento Esperado de Atlas

### Prueba 1: 
Grounding "¿Puedo solicitar el reembolso de un pago si me equivoqué?" Clasifica a Knowledge RAG. Responde que NO hay reembolsos citando el artículo oficial.


### Prueba 2: Prevención Duplicados 
"Quiero pagar mi folio FOL-1001 de nuevo" Invoca Flow 1. Detecta estado 'Pagado'. Alerta al usuario y bloquea la acción.

### Prueba 3: Facturación Completa 
"Hola, quiero solicitar la factura CFDI de mi pago. Mi folio es 123456789012345678901234, RFC XAXX010101000, CP 72000, correo factura.exitosa@ejemplo.com y régimen 605" Pide RFC, CP y Correo. Al recibirlos, invoca Flow 2. Retorna CFDI-XXXX y crea el Log.

### Prueba 4: Escalamiento 
"Llevo 4 días con un cobro doble y nadie me resuelve, pásame a un supervisor" Detecta insatisfacción/fuera de alcance. Invoca acción de escalamiento a Omni-Channel.

## 6.2. Auditoría en Log_de_Auditoria_IA__c 

8. Tras ejecutar las pruebas, ve al tab del objeto Log de Auditoría IA en Salesforce. 
9. Verifica que existan registros creados en tiempo real con las marcas de tiempo y acciones que el agente ejecutó durante las pruebas.


Fase 7: Despliegue en Interfaz Ciudadana y Estrategia de Demo (Pitch)
Justificación: La solución debe ser presentada a los jueces en un portal funcional. Un sitio web de Experience Cloud simula la ventanilla virtual del gobierno de Puebla.
7.1. Creación de Portal Ciudadano (Experience Cloud) 10. En Setup, busca Digital Experiences > Settings y actívalo. 11. Crea un nuevo sitio con la plantilla Help Center o Customer Service. 12. Nómbralo: Portal de Trámites y Servicios Puebla. 13. Agrega el componente de Embedded Messaging / Agent Chat en la página de inicio. 14. Publica el sitio (Publish).
7.2. Estructura del Pitch para los Jueces (Demo de 3 a 5 minutos) 15. Problema Real (30 seg): Presentar la desorganización actual en trámites locales (doble pago sin reembolso, tardanza de 3 días en CFDI, falta de auditoría). 16. Demostración de las 4 Dimensiones (3 min):
o Capa 1 (RAG): Preguntar por la política de reembolsos (demostrar respuesta grounded sin alucinación).
o Capa 2 (Acción): Ingresar un folio ya pagado para intentar pagar de nuevo -> El agente lo bloquea ejecutando el Flow.
o Capa 2 y 3 (CFDI + Logs): Solicitar un CFDI ingresando datos -> Mostrar la creación del registro en Salesforce y el registro automático en el Log_de_Auditoria_IA\_\_c.
o Capa 4 (Confianza): Simular una queja compleja -> Mostrar el escalamiento fluido a Omni-Channel. 17. Impacto en el Negocio/Gobierno (30 seg): Reducción de carga operativa del 80% en ventanillas de finanzas y cero cobros duplicados no rastreados.
Fase 8: Funcionalidades Opcionales (Solo si sobra tiempo)
Justificación: Tareas secundarias que no forman parte de las 4 dimensiones principales. Solo deben abordarse cuando la Fase 7 esté 100% probada. 18. Voz (Service Cloud Voice / Speech-to-Text): Habilitar el módulo de dictado de voz nativo del navegador en la ventana de chat del portal para permitir accesibilidad ciudadana por voz. 19. App Móvil Externa / Mobile Publisher: Envolver la comunidad de Experience Cloud en una vista responsiva accesible mediante contenedor móvil web.
