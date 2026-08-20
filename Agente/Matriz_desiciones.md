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














Registrar_Log_Escalamiento
El usuario solicita al agente ser escalado con un empleado humano, ya que el problema sobrepasa sus capacidades
Extrae EXCLUSIVAMENTE la dirección de correo electrónico (ej. caro@gmail.com). Este campo NO debe contener texto contextual, solo el email.
Resumen breve de la problemática expresada por el usuario. Queda ESTRICTAMENTE PROHIBIDO incluir la dirección de correo electrónico dentro de esta cadena.

quiero hablar con un humano, tengo un error en mi folio, mi correo es caro@gmail.com

📌 Paso 1: Organizar el Formato de Página de Log_de_Auditoria_IA\_\_c
Vamos a asegurarnos de que la ficha del Log de Auditoría muestre de forma destacada el motivo de escalamiento y el folio.

Entra a Configuración (Setup) > Gestor de Objetos (Object Manager) > Log_de_Auditoria_IA\_\_c.

Entra a Formatos de página (Page Layouts).

Asegúrate de que los campos clave estén bien visibles en dos columnas:

Columna Izquierda: Folio_Log (o Nombre del Log), Motivo_Escalamiento (ej. "cobro doble"), Correo_Ciudadano.

Columna Derecha: Fecha_Hora, Estatus_Atencion, Propietario.

Haz clic en Guardar.

📌 Paso 2: Configurar la Consola de Servicio (Service Console)
En la esquina superior izquierda de Salesforce, haz clic en el Iniciador de aplicaciones (el icono de 9 puntos o "Waffle").

Busca y selecciona Consola de Servicio (Service Console).

En la barra de navegación superior de la Consola de Servicio, haz clic en la flecha hacia abajo junto a las pestañas y selecciona Editar (o el icono de lápiz) para agregar pestañas.

Agrega el objeto Log_de_Auditoria_IA\_\_c para que sea una de las pestañas principales de navegación.

Abre la pestaña Log_de_Auditoria_IA\_\_c y crea una vista de lista llamada "Escalamientos Pendientes IA" (filtrando por los creados hoy).

📌 Paso 3: Probar el Escenario de Escalamiento
Probaremos en el chat del Agente el caso de escalamiento por cobro doble y verificaremos en tiempo real cómo aparece en la Consola de Servicio del Ejecutivo.

Dime si estás lista para iniciar el Paso 1 en Log_de_Auditoria_IA\_\_c.

Abre el Iniciador de aplicaciones (App Launcher) y selecciona Consola de Servicio (Service Console).

Agrega el objeto Log_de_Auditoria_IA\_\_c como una pestaña de navegación principal en la consola.

Crea una Vista de lista (List View) llamada "Escalamientos Pendientes IA" filtrada por registros creados hoy.

Paso 1.3: Dashboard de Control Directivo (Potenciador Visual)
Crea un Informe (Report) sobre Log_de_Auditoria_IA**c agrupado por Motivo_Escalamiento**c.

Crea un Informe (Report) sobre Solicitud_CFDI**c agrupado por Estatus_Emision**c.

Crea un Panel (Dashboard) denominado "Centro de Mando - Atención e Impuestos IA" con 2 componentes visuales (Gráfico de barras y Gráfico de dona).

🟡 URGENCIA 2: La Presentación de Impacto / Pitch Deck (Opción 1)
Prioridad: ALTA | Tiempo estimado: 5 a 6 horas
Al ser un formato de Presentación + Demostración, el "storytelling" y la justificación de negocio definirán al ganador.

1. Investigación de la Situación Actual (El "Problema"):
   o Métrica de dolor: Tiempo promedio de espera presencial en tesorerías para aclaraciones y facturación (ej. 2 a 4 horas).
   o Riesgo fiscal: Pérdidas por cobros dobles, errores manuales en emisión de CFDI y falta de trazabilidad en escalamientos.
2. La Solución (Tu propuesta):
   o Arquitectura Híbrida: IA Generativa (Agentforce Grounded) para la experiencia conversacional + Flujos Deterministas (Flow Builder) para la precisión fiscal cero alucinación.
3. Impacto y ROI:
   o Disminución del 70% en carga operativa presencial.
   o Reducción a 0% en emisión de facturas sobre folios sin pagar.
   o Trazabilidad auditable del 100% de las interacciones humanas.
   🟢 URGENCIA 3: Página Web / Interfaz Visual (Opción 2 - Con Estrategia)
   Prioridad: MEDIA-BAJA (Descartar desarrollo desde cero / Usar alternativa nativa) | Tiempo estimado: 1 hora
   • ¿Por qué NO programar un sitio web externo con API desde cero?
   Desarrollar una web personalizada, conectarle una API REST a Salesforce y agregarle componentes de voz en menos de 48 horas es una trampa de tiempo. Si la API falla por latencia o CORS durante la demo en vivo, destruirá la impecable calificación que ya tienes.
   • La Solución Inteligente (Smart Shortcut):
   Usa Salesforce Embedded Messaging (Chat Incrustado) en una página de Experience Cloud / LWR de Salesforce. Se activa en 15 minutos, te da una URL pública con aspecto de portal gubernamental moderno y el chat del agente ya corre ahí nativamente sin programar APIs.
   📅 Plan de Acción para las Próximas 48 Horas
   Día / Horario Foco Entregable Concreto
   Hoy (Noche) Feedback de Evaluadores Configurar vista de Solicitud_CFDI**c y la Consola de Servicio con el registro de Log_de_Auditoria_IA**c para la continuidad humana.
   Mañana (Mañana) Embedded Chat / Web Desplegar el agente en un sitio simple de Experience Cloud para tener la "página web" lista sin código.
   Mañana (Tarde/Noche) Presentación (Pitch Deck) Diseñar diapositivas (Problema, Solución, Arquitectura, Demo y ROI).
   Día previo (20 Ago) Ensayos y Live Demo Ensayar la presentación ajustando los tiempos exactos del speech y la navegación en Salesforce.
   💡 Argumento de Venta para tu Presentación (Tu diferenciador)
   "La mayoría de los agentes conversacionales fallan en el sector público porque alucinan datos financieros o transfieren conversaciones sin contexto. Nuestra propuesta resuelve esto mediante una Arquitectura Híbrida: Agentforce entiende al ciudadano, pero la lógica de negocio y las reglas fiscales son ejecutadas de forma determinista por Flow Builder, garantizando que nunca se emita un CFDI inválido ni se procese un pago duplicado, manteniendo siempre evidencia auditable y continuidad total hacia el ejecutivo humano."

¿Comenzamos a estructurar el guion y el contenido de las diapositivas para la presentación?
