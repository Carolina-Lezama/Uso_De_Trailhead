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

revisar el plan de trabjo
problemas que debes decirle a la ia en tu siguiente prompt:

necesitamos re elaborar el plan de trabajo
en el log del CFDI aunque se crea, muestra nombre y detalles de la solicitud, no se marca que ciudadano lo realizo, tampoco ninguno de los datos que se le pidio al usuario antes de hacer la solicitud

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
