# ¿Qué es Agentforce?
Agentforce utiliza su información, como una solicitud, y los datos de confianza de su organización para proporcionar respuestas precisas y ejecutar las acciones adecuadas.

Un agente es un asistente de IA autónomo que se adapta y mejora con cada interacción.

El agente interpreta su solicitud, traza un plan para abordarla y después llama a las mejores acciones para cumplir sus necesidades.

Cuando más descriptiva sea la solicitud, más detallada será la respuesta.

Ya hemos mencionado que Agentforce selecciona la mejor acción para llevar a cabo una tarea. Las acciones son la manera en la que el agente realiza las cosas. Una agente incluye una biblioteca de acciones, que consiste, básicamente, en una serie de tareas que Copilot puede realizar.

Todas las acciones de un agente se asignan a un subagente.

Los subagentes son una capa de organización y personalización que hace que el agente tome decisiones más acertadas y genere respuestas predecibles y más relevantes. 

Cuando un usuario introduce una pregunta o una solicitud, el agente selecciona un subagente relevante y luego inicia una o más acciones incluidas en ese subagente. Esto hace que el agente se centre en las acciones y en los datos más pertinentes de la conversación actual.

los bots son más predecibles porque siguen rutas predefinidas de conversación.

Agentforce confía en varias capas de seguridad para proteger los datos de entidades externas y asegurar que, de manera interna, solo las personas que cuenten con los permisos adecuados puedan acceder a los datos.

Cuando un usuario introduce una solicitud en un agente y se llama a una acción, dicha acción necesitará los datos de su empresa o de su cliente para completar los pasos. Las acciones de Agentforce reconocen y respetan la configuración de permisos de las organizaciones y los usuarios de la persona que realiza la solicitud, y solo devolverán información pertinente que el usuario esté autorizado a ver. 

# Subagentes y acciones
Los agentes están formados por subagentes, que definen las diferentes funciones que puede desempeñar cada agente. Los subagentes incluyen instrucciones que indican al agente cómo tomar decisiones y qué debe o no debe hacer. Al definir subagentes, debe establecer unos límites y un contexto claros para controlar el comportamiento del agente.

Cuando un usuario realiza una pregunta o envía una solicitud, el agente selecciona el subagente adecuado e inicia las acciones correspondientes dentro del subagente. Esto hace que el agente se centre en las tareas y los datos más relevantes para la conversación actual.

## Subagentes personalizados
Los subagentes personalizados le permiten personalizar un agente para que se ajuste a necesidades específicas de la empresa. Puede definir el subagente, las acciones y las instrucciones para que se alineen con sus procesos y requisitos únicos.

## Acciones personalizadas
Si necesita personalizar su agente para procesos y flujos de trabajo específicos de su empresa, puede crear acciones personalizadas para los subagentes. ¿Lo mejor de todo? No tiene que empezar desde cero. Las acciones personalizadas utilizan tecnología de Salesforce que ya conoce y le gusta.

A la hora de crear una acción personalizada, se crea en función de las características de la plataforma existente, como clases de Apex invocables o de REST, flujos iniciados automáticamente, plantillas de solicitud y servicios externos.

# ¿Qué es un motor de razonamiento?
El motor de razonamiento que impulsa Agentforce se llama motor de razonamiento Atlas y está basado en gráficos. Puede pensar en ello como si fuese un diagrama de flujo con nodos, variables y transiciones, de manera que los agentes pueden seguir rutas específicas y predecibles.

A diferencia de los motores de razonamiento basados en solicitudes, Atlas separa el flujo de trabajo general de un agente de sus habilidades conversacionales. Utiliza Script del agente, el lenguaje para crear agentes, a fin de combinar expresiones programáticas con instrucciones en lenguaje natural. El resultado es un razonamiento híbrido que proporciona la capacidad de predicción y el control que exige la empresa, y la flexibilidad y creatividad de los modelos de lenguaje grandes (LLM).

- Paso 1: el proceso comienza cuando un usuario introduce una pregunta o solicitud.
- Paso 2: el agente distribuye al subagente definido como el subagente inicial.
- Paso 3: después de que el agente seleccione un subagente, empieza a resolver las instrucciones de razonamiento del subagente en el orden en que se han escrito. Esta parte es determinante, lo que significa que el agente resuelve expresiones programáticas antes de comunicarse con el LLM. Si el agente cambia a otro subagente durante el proceso, redirige la conversación inmediatamente.
- Paso 4: después de que se haya completado el razonamiento, el agente utiliza las instrucciones generadas para crear una solicitud y enviársela al LLM. La solicitud incluye lo siguiente: instrucciones a nivel de agente, el historial de la conversación reciente, las instrucciones que se han resuelto y las acciones disponibles para el subagente.
- Paso 5: el agente envía la solicitud al LLM iniciar el proceso de razonamiento y actuar. El agente utiliza el LLM para analizar la información disponible en la solicitud y determinar los siguientes pasos. El LLM puede responder al usuario o desencadenar una acción. Si el LLM elige responder al usuario, completa el bucle de razonamiento y formula una respuesta. Si el LLM elige ejecutar una acción, se inicia la acción y cualquier lógica después de la acción asociada a la misma.

