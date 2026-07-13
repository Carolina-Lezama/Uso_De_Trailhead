# Conocer los motores de razonamiento
Un motor de razonamiento es un tipo de IA que recopila información, sigue reglas lógicas y toma decisiones: lo mismo que hacen las personas cuando resuelven problemas.

## Tipos de razonamiento
- Deducción: “Todas las frutas tienen semillas. Un mango es una fruta. Por lo tanto, un mango tiene semillas”. (Parte de una regla general y la aplica a un caso específico).
- Inducción: “Las últimas cinco reuniones comenzaron tarde. Probablemente, la próxima también comenzará tarde”. (Analiza patrones de experiencias pasadas para hacer una predicción general).
- Abducción: “Las luces están apagadas y nadie viene a abrir la puerta. Probablemente, no están en casa”. (Hace suposiciones en función de pistas limitadas).

Cuando una solicitud ayuda a un LLM a elaborar un plan lógico para resolver un problema, la llamamos estrategia de razonamiento.

### Cadena de pensamientos (CoT)
Esto es como enseñarle al LLM a “mostrar su trabajo”. La cadena de pensamientos desglosa un problema difícil en una serie de pasos más pequeños, como cuando un humano arma un rompecabezas. Es excelente para resolver problemas matemáticos, razonar con sentido común y realizar otras tareas que requieren lógica.

### Razonamiento y acción (ReAct)
ReAct combina el razonamiento con acciones funcionales. Esta estrategia no depende únicamente del conocimiento del LLM: interactúa, verifica información y perfecciona sus respuestas paso a paso con los comentarios del usuario. Esto reduce la cantidad de “alucinaciones” (o respuestas incorrectas) y genera resultados más confiables.

### Árbol de pensamientos (ToT)
En lugar de seguir un único plan, el árbol de pensamientos explora muchos caminos posibles en cada paso, que es como evaluar varias opciones antes de elegir la mejor.

### Razonamiento mediante planificación (RAP)
El RAP lleva el razonamiento un paso más adelante al ayudar al LLM a simular resultados futuros. Predice cómo se reflejará el uso de acciones, explora alternativas y perfecciona su plan durante el proceso, igual que un estratega humano. El RAP se destaca en tareas que exigen planificación a largo plazo, inferencia lógica o resolución de problemas en varios pasos.

