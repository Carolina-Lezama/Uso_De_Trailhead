
•	Arquitectura Básica (Visual): Captura rápida de Flow Builder o Agent Builder (5-10 segundos) para demostrar que no es una simulación.

•	Escenario 1 (Validación y CFDI 4.0): Bloqueo de pago duplicado + generación del registro de factura fiscal en una sola interacción.

•	Escenario 2 (Escalamiento a Auditoría): Traspaso a atención humana con captura del motivo y entrega del folio del Log_de_Auditoria_IA__c.

•	Comprobación en Backend: Mostrar la vista de lista (List View) de Salesforce con los registros recién creados para evidenciar la persistencia de datos real.

Estructura y Tiempos del Video (3 Minutos)

Bloque	Tiempo	Qué Mostrar en Pantalla
1. Introducción	0:00 - 0:20	Pantalla principal de Salesforce / Agent Builder.
2. Escenario 1: Bloqueo y CFDI	0:20 - 1:30	Agent Preview procesando la línea de captura pagada y generando el CFDI.
3. Escenario 2: Escalamiento	1:30 - 2:20	Agent Preview registrando el reporte de anomalía y devolviendo el folio de auditoría.
4. Evidencia en Backend y Cierre	2:20 - 3:00	Vistas de lista de Solicitud_CFDI__c y Log_de_Auditoria_IA__c.
Guión Paso a Paso




Bloque 3: Escenario 2 - Escalamiento y Auditoría IA (1:30 - 2:20)
(Acción en pantalla: Escribes: Llevo 4 días con un cobro doble y nadie me resuelve, pásame a un supervisor)


"Ahora probaremos la atención a casos complejos. Al detectar la solicitud de atención humana por un cobro doble, la IA invoca la acción @Logs_Atencion.

El flujo autolanzado extrae automáticamente la causa de la conversación, inserta el log de auditoría y le confirma al ciudadano entregándole su folio oficial de seguimiento."

Bloque 4: Verificación en Backend y Cierre (2:20 - 3:00)
(Acción en pantalla: Cambias de pestaña a Salesforce y abres la vista de lista de Solicitud_CFDI__c y Log_de_Auditoria_IA__c refrescando la página).


"Finalmente, verificamos la persistencia en el backend de Salesforce. En el objeto Solicitud_CFDI__c podemos observar la factura recién emitida, y en Log_de_Auditoria_IA__c consta el registro del escalamiento con su folio autonumérico y motivo capturado.

Con esto demostramos una solución 100% funcional, transaccional y segura con Agentforce. Gracias."

Recomendaciones Técnicas de Grabación


•	Cortes entre secciones: Haz un corte limpio (jump cut) cuando la IA esté "pensando" o cargando para ahorrar de 3 a 5 segundos por interacción.

•	Resolución y Formato: Graba en 1080p a 30fps y exporta en MP4 con bitrate medio/bajo para asegurar que el archivo pese menos de 80 MB (muy por debajo del límite de 150 MB).

•	Zoom en pantalla: Haz un zoom leve (110% o 125%) en la ventana de chat para que el texto de las respuestas de la IA sea legible en el video.


### Prueba 1:

Grounding "¿Puedo solicitar el reembolso de un pago si me equivoqué?" Clasifica a Knowledge RAG. Responde que NO hay reembolsos citando el artículo oficial.

### Prueba 2: Prevención Duplicados

"Quiero pagar mi folio FOL-1001 de nuevo" Invoca Flow 1. Detecta estado 'Pagado'. Alerta al usuario y bloquea la acción.

### Prueba 3: Facturación Completa

"Hola, quiero solicitar la factura CFDI de mi pago. Mi folio es 123456789012345678901234, RFC XAXX010101000, CP 72000, correo factura.exitosa@ejemplo.com y régimen 605" Pide RFC, CP y Correo. Al recibirlos, invoca Flow 2. Retorna CFDI-XXXX y crea el Log.

### Prueba 4: Escalamiento

"Llevo 4 días con un cobro doble y nadie me resuelve, pásame a un supervisor" Detecta insatisfacción/fuera de alcance. Invoca acción de escalamiento a Omni-Channel.