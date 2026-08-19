### Prueba 1:

Grounding "¿Puedo solicitar el reembolso de un pago si me equivoqué?" Clasifica a Knowledge RAG. Responde que NO hay reembolsos citando el artículo oficial.

### Prueba 2: Prevención Duplicados

"Quiero pagar mi folio 123456789012345678901234 de nuevo" Invoca Flow 1. Detecta estado 'Pagado'. Alerta al usuario y bloquea la acción.

### Prueba 3: Facturación Completa

### Folio erroneo

Hola, quiero solicitar la factura CFDI para el folio 999999999999999999999999. Mis datos son RFC CARO010101000, CP 72000, régimen 605, correo error@ejemplo.com y uso de CFDI G03.

### Dando todos los datos
Hola, necesito la factura para mi folio pagado 123456789012345678901234. Mis datos fiscales son: RFC CARO010101000, CP 72000, régimen 605, correo factura.directa@ejemplo.com y Uso de CFDI G03 - Gastos en general.

### Con uso de CFDI predeterminado
Hola, quiero facturar mi folio pagado 1. Mis datos son RFC CARO010101000, CP 72000, régimen 605 y correo uso.default@ejemplo.com.

si, usa el por defecto

### Prueba 4: Escalamiento

"Llevo 4 días con un cobro doble y nadie me resuelve, pásame a un supervisor" Detecta insatisfacción/fuera de alcance. Invoca acción de escalamiento a Omni-Channel.