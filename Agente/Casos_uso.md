### Prueba 1:

Grounding "¿Puedo solicitar el reembolso de un pago si me equivoqué?" Clasifica a Knowledge RAG. Responde que NO hay reembolsos citando el artículo oficial.

### Prueba 2: Prevención Duplicados

"Quiero pagar mi folio 123456789012345678901234 de nuevo" Invoca Flow 1. Detecta estado 'Pagado'. Alerta al usuario y bloquea la acción.

### Prueba 3: Facturación Completa

"Hola, quiero solicitar la factura CFDI de mi pago. Mi folio es 123456789012345678901234, RFC XAXX010101000, CP 72000, correo factura.exitosa@ejemplo.com y régimen 605" Pide RFC, CP y Correo. Al recibirlos, invoca Flow 2. Retorna CFDI-XXXX y crea el Log.

### Prueba 4: Escalamiento

"Llevo 4 días con un cobro doble y nadie me resuelve, pásame a un supervisor" Detecta insatisfacción/fuera de alcance. Invoca acción de escalamiento a Omni-Channel.