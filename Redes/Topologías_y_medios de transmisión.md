# Redes de computadoras
base de las comunicaciones digitales, la transferencia de informacion sigue una estructura organizada que define como estan conectados los equipos, esto se llama **TOPOLOGIA DE RED**

# Influencias al mommento de elegir una topologia.
- Distancia(a mayor distancia la señal se debilita "Atenuacion")
- Trafico de red
- Disponibilidad
- Inversion de la infraestructura (podria alterar los datos)
- Condiciones del lugar

# Topologia en bus
Una de las formas mas antiguas de conectar computadoras en red, todos los dispositivos se conectan a un unico cable principal, recorre toda la instalacion y aqui viaja toda la informacion. Al mandar informacion, todos los equipos reciben la señal, pero solo la que tiene la direccion correcta la procesa, el error surge cuando 2 equipos intentan mandar informacion al mismo tiempo(colision), las 2 señales se mezclan y los datos se pierden, los equipos deben esperar antes de volver a intentarlo

Utilizaba cable coaxial con conectores BNC

## Ventajas
- instalacion economica y simple
- poco cableado necesario
- sin dispositivo central requerido
- facil de ampliar en tramos cortos

## Descentajas
- un fallo en el cable corta toda la red
- colisiones frecuentes con muchos nodos
- rendimiento degradado al agregar mas dispositivos
- diagnostico de fallas fisicas complejo

# Topologia token ring
Conecta los dispositivos formando un anillo cerrado, cada equipo esta unido al siguiente mediante su propio segmento de cable, los datos simpre circulan en la misma direccion.

Existe una señal llamada token o testigo que circula constantemente por el anillo, si algun dipositivo necesita enviar datos, espera a que el token llegue a el, lo toma y lo marca como ocupado y ya transmite la informacion, los demas ven que el canal esta ocupado y esperan su turno

# Topologia estrella
Mas usada actualmente, cada dispositivo tiene su propio cable que lo conecta directamente a un equipo central llamado Switch. no cables compartidos, cada computadora tiene su canal exclusivo de comunicacion.

el switch es inteligente ya que sabe enviar los datos únicamente al dispositivo al que van dirigidos sin
molestar a los demás(eliminando las colisiones).

Cable mas utilizado es el UTP, longitud máxima de 100 m, si se rompe el dable de una computadora, solo afecta a esa, las demas siguen funcionando, pero si el switch central falla, toda la red se detiene.

# Topologia arbol o jerarquica
organiza los equipos en niveles en forma de piramida, a parte más alta está el equipo principal que administra el tráfico de toda la red, seguido de los switches intermedios que se encargan de diferentes áreas o pisos y en el nivel más bajo están las computadoras y dispositivos de los usuarios.

Facilita la escalabilidad, permite separar lógicamente las distintas áreas de una empresa, lo que mejora la seguridad y el control del tráfico.

Fibra optima en niveles superiorer y cable UTP para conexiones en la parte mas inferior.

si el switch principal falla, todos los niveles inferiores quedan sin comunicación.

# Topologia malla
lleva la redundancia al máximo. En esta configuración, cada dispositivo está conectado directamente con varios otros, creando múltiples rutas posibles para que los datos lleguen a su destino.

Si alguna ruta falla, los datos simplemente toman otro camino, lo que ofrece la mayor tolerancia posible a fallos, pero resulta muy costoso.

en la práctica  se usa la malla parcial, donde cada equipo se conecta solo con algunos

Internet en su conjunto funciona bajo este principio. Hoy es el estándar para cualquier infraestructura donde la disponibilidad continua sea indispensable.

La topología malla se utilizó principalmente como un método de defensa.
Se podría pensar como una topología que
conecta todos con todos. Su ventaja es alta tolerancia a fallos

# Topología híbrida

La topología híbrida combina dos o más tipos de topología dentro de la misma red. Su objetivo es tomar las ventajas de cada una y aplicarlas donde más convienen.

La flexibilidad de la topología híbrida es su mayor ventaja. El mayor reto es la complejidad de gestión, ya que requiere personal técnico especializado para mantenerla con buen funcionamiento.

La forma en que se conectan los dispositivos determina la resistencia,  el rendimiento y el costo de toda la infraestructura

# Medio de transmisión.
Cada vez que un dispositivo envía información a otro, necesita un camino para que dicha información llegue a su destino.

Es un canal por donde viajan los datos en forma de señales  eléctricas, pulsos de luz u sondas de radio.

los medios de transmisión eh se dividen principalmente en dos grandes tipos, que son los cableados o los físicos y los
inalámbricos.

### medios guiados
- cable de cobre
- fibra optica

### medios no guiados
- redes Wi-Fi 
- celulares

La elección del medio determina la velocidad, la distancia y la resistencia a interferencias de toda la red. 

