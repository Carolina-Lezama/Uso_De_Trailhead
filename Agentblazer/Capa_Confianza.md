# ¿Qué es la Capa de confianza de Einstein?
La Capa de confianza de Einstein mejora la seguridad de la IA generativa con controles de datos y privacidad que se integran perfectamente en la experiencia del usuario final. Con estos controles, Einstein es capaz de ofrecer IA basada en los datos de sus clientes y de su compañía sin dar lugar a posibles riesgos para la seguridad. En su forma más simple, la Capa de confianza es una secuencia de puertas de enlace y mecanismos de recuperación que trabajan juntos para permitir que la IA generativa sea abierta y de confianza

Con la Capa de confianza de Einstein, los clientes pueden aprovechar los beneficios de la IA generativa sin comprometer la seguridad de sus datos ni los controles de privacidad. Incluye un conjunto de funciones que protegen sus datos, como la recuperación segura de datos, el anclaje dinámico, el enmascaramiento de datos y la retención cero de datos, para que no tenga que preocuparse acerca del destino de sus datos. La detección de lenguaje tóxico escanea las solicitudes y respuestas para comprobar que sean exactas y adecuadas. Además, para una mayor responsabilidad, una traza de auditoría realiza el seguimiento de una solicitud en cada paso de su recorrido. 

La Capa de confianza se sitúa entre un LLM, y sus empleados y clientes para mantener sus datos seguros mientras utiliza la IA generativa para todos sus casos de uso de negocio, incluidos los emails de ventas, los resúmenes de trabajo y las respuestas de servicio en su centro de contacto.

# El recorrido de la solicitud
las instrucciones claras, la información sobre el contexto y las restricciones permiten crear una buena solicitud que genera una excelente respuesta por parte del LLM.

Cuando se realiza una solicitud a la Capa de confianza desde una de nuestras aplicaciones de Salesforce, la capa solicita la plantilla de solicitud adecuada.

essica empieza a chatear con su primer cliente del día, que necesita ayuda para actualizar su tarjeta de crédito. Respuestas de servicio empieza a sugerir respuestas directamente en la Consola de servicio. Las respuestas se actualizan cada vez que el cliente envía un mensaje nuevo, de modo que tengan sentido en el contexto de la plática. También están personalizadas para el cliente en función de los datos almacenados en Salesforce. Cada respuesta sugerida se genera a partir de una plantilla de solicitud. La plantilla de solicitud contiene instrucciones y marcadores de posición que se completan con datos de negocio; en este caso, los datos relacionados con el cliente de Jessica y su caso de asistencia, así como datos y flujos relevantes de la organización de Jessica. La plantilla de solicitud se encuentra detrás de la Capa de confianza de Salesforce, y Jessica, como usuario final en la Consola de servicio, no puede verla.

Para que las respuestas sean relevantes y de calidad, los datos de entrada deben ser relevantes y de calidad

Respuestas de servicio vincula la conversación a una plantilla de solicitud y empieza a sustituir los campos de marcadores de posición por contexto de página, campos de combinación y artículos de Knowledge relevantes del registro del cliente. Este proceso se denomina anclaje dinámico. En general, cuanto mayor sea el anclaje de una solicitud, más precisa y adecuada será la respuesta. El anclaje dinámico es lo que permite que las plantillas de solicitud se puedan reutilizar, de modo que toda una organización pueda acceder a ellas.

El proceso de anclaje dinámico comienza con la recuperación segura de datos, que identifica los datos importantes sobre el cliente de Jessica procedentes de su organización. Lo más importante es que la recuperación segura de datos respeta todos los permisos de Salesforce vigentes en su organización que restrinjan el acceso a datos específicos sobre objetos, campos, etc. De este modo, Jessica solo podrá obtener la información a la que esté autorizada a acceder. Los datos que se recuperan no contienen información privada, así como tampoco información que requiera permisos especiales.

En el caso de Jessica, los datos del cliente son suficientes para personalizar la plática. La búsqueda semántica utiliza el aprendizaje automático y métodos de búsqueda para encontrar información relevante en otras fuentes de datos que se puedan incluir de manera automática en la solicitud. Esto significa que Jessica no tiene que buscar las fuentes de manera manual

Si bien la solicitud contiene datos precisos sobre el cliente de Jessica y su problema, aún no está lista para pasar al LLM porque contiene información como el nombre y la dirección del cliente. La Capa de confianza agrega otro nivel de protección a los datos de los clientes de Jessica mediante el enmascaramiento de datos. El enmascaramiento de datos implica la tokenización de cada valor, de modo que se sustituyen los valores por un marcador de posición en función de lo que representa.

Salesforce utiliza una combinación de concordancia de patrones y técnicas avanzadas de aprendizaje automático para identificar y enmascarar de forma inteligente datos de clientes como nombres e información de tarjetas de crédito. El enmascaramiento de datos se produce en segundo plano

Aunque Salesforce tiene una política de retención de datos cero con los LLM de terceros, algunas compañías y casos de uso o políticas de reglamentación pueden requerir que los datos confidenciales no se envíen al LLM en absoluto. 

El generador de solicitudes proporciona medidas de seguridad adicionales para proteger a Jessica y a sus clientes. Se trata de instrucciones adicionales para el LLM sobre cómo comportarse en determinadas situaciones para reducir la probabilidad de que envíe algo no deseado o dañino. Por ejemplo, un LLM puede recibir instrucciones de no abordar ningún contenido ni generar ninguna respuesta para la que no disponga de información.

Los hackers, y a veces incluso los empleados, buscan saltarse las restricciones e intentar realizar tareas o manipular los resultados del modelo de maneras que el modelo no fue diseñado para manejar. En la IA generativa, uno de estos tipos de ataques se denomina inyección de solicitud. La protección de la solicitud puede ayudar a defenderse contra estos ataques y reducir la posibilidad de que los datos se vean comprometidos.

## Puerta de enlace de LLM segura
Una vez que se completa con los datos relevantes y las protecciones establecidas, la solicitud está lista para salir del Límite de confianza de Salesforce a través de la puerta de enlace de LLM segura hacia los LLM conectados. En este caso, el LLM al que está conectada la organización de Jessica es OpenAI. OpenAI utiliza esta solicitud para generar una respuesta relevante y de alta calidad que Jessica puede utilizar en su plática con el cliente.

Si Jessica utilizara una herramienta de LLM orientada al consumidor, como un chatbot de IA generativa, sin una capa de confianza sólida, su solicitud, incluidos todos los datos del cliente e incluso la respuesta del LLM, podrían almacenarse en el LLM para el entrenamiento del modelo. Sin embargo, cuando Salesforce se asocia con un LLM externo basado en API, exigimos un acuerdo para proteger toda la interacción, lo que se denomina retención cero de datos. Nuestra política de retención cero de datos implica que ningún dato del cliente, incluidos el texto de la solicitud y las respuestas generadas, se almacenan fuera de Salesforce.

Por lo general, OpenAI desea conservar las solicitudes y las respuestas durante un periodo de tiempo para controlar el mal uso. Gracias a su increíble solidez, los LLM de OpenAI comprueban si sucede algo inusual en sus modelos, como los ataques de inyección de solicitud sobre los que aprendió en la unidad anterior. Sin embargo, nuestra política de retención cero de datos impide que los socios de LLM conserven datos de la interacción.

 La Capa de confianza debe comprobar que no se produzcan resultados no deseados, aunque el tono sea amable y el contenido, exacto. La respuesta aún contiene bloques de datos enmascarados, y Jessica la considera demasiado impersonal para enviarla a su cliente. Antes de que ella vea la respuesta, la Capa de confianza tiene que realizar algunas acciones importantes.

 Cuando la respuesta a la plática de Jessica pasa del LLM al Límite de confianza de Salesforce, ocurren dos cosas importantes. En primer lugar, la detección de lenguaje tóxico protege a Jessica y a sus clientes de la toxicidad. Se preguntará en qué consiste este proceso. La Capa de confianza utiliza modelos de aprendizaje automático para identificar y marcar contenido tóxico en avisos y respuestas, en cinco categorías: violencia, sexual, blasfemias, odio y físico. La puntuación de toxicidad general combina las puntuaciones de todas las categorías detectadas y produce una puntuación general que va de 0 a 1

A continuación, antes de que la solicitud llegue a Jessica, la Capa de confianza debe revelar los datos enmascarados de los que hablamos antes para que la respuesta sea personal y adecuada para el cliente de Jessica. La Capa de confianza utiliza los mismos datos tokenizados que guardamos cuando enmascaramos los datos originalmente para desenmascararlos. Una vez desenmascarados los datos, la respuesta se comparte con Jessica.

Todo lo que ocurrió durante la interacción entre Jessica y su cliente son metadatos con marca de tiempo que recopilamos en una traza de auditoría. Esto incluye la solicitud, la respuesta original sin filtrar, la puntuación de lenguaje tóxico y los comentarios recopilados a lo largo del proceso. La traza de auditoría de la Capa de confianza de Einstein agrega una capa de responsabilidad, por lo que Jessica puede estar segura de que los datos de sus clientes están protegidos.




