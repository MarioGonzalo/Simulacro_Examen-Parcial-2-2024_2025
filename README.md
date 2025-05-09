# Simulacro_Examen-Parcial-2-2024_2025

## Parte I: Capa de Red
### Pregunta 1: Cálculo de Ruta Más Corta
**a) Explica brevemente el funcionamiento del Algoritmo de Dijkstra para encontrar la ruta más corta entre dos nodos en un grafo ponderado.**

- El algoritmo de Dijkstra asigna una "etiqueta" a cada nodo, cada etiqueta es temporal y cuando se encuentra el camino más rápido hace esta etiqueta permanente, el proceso termina si todas las etiquetas se vuelven permanentes o si se llega al nodo destino.

**b) Describe el método de Enrutamiento por Inundación (Flooding) y discute sus ventajas y desventajas comparándolo con Dijkstra.**

- En el enrutamiento por inundación genera infinitos paquetes que se envían por todas las líneas posibles excepto por la que vienen incluyendo en cada paquete un contador de saltos

### Pregunta 2: Cálculo de Direcciones de Broadcast y Subredes
**a) Para la subred 172.29.152.0 con máscara 255.255.248.0, determina la dirección de broadcast. Explica el proceso de conversión de la máscara a binario y cómo se obtiene el resultado.**

Hay que transformar la máscara en binario para hallar los bits de red

La máscara 255.255.248.0 en binario es:

255     = 11111111  
255     = 11111111  
248     = 11111000  
0       = 00000000
21 bits de red $\rightarrow$ /21

Con una máscara /21, cada subred tiene:

- Tamaño: 2^(32 - 21) = 2^11 = 2048 direcciones

- Subredes comienzan en múltiplos de 2048 desde la base de la red en el tercer y cuarto octeto.

Convertimos 172.29.152.0 a su número entero (en base 10):

- 172.29.152.0 $\rightarrow$ Tercer octeto = 152

- 152 en binario = 10011000

- Como 248 cubre 8 bloques de 32 direcciones, buscamos el rango que contiene 152.

La subred 172.29.152.0/21 cubre desde:

- Inicio: 172.29.152.0

- Fin: 172.29.159.255 (porque 152 + 7 = 159)

Dirección de broadcast: **172.29.159.255**

**b) Dado el bloque 172.18.26.0/23, calcula la dirección de broadcast y justifica el proceso.**

/23 = 255.255.254.0

Eso significa que la red agrupa dos bloques de clase C (2 × 256 = 512 direcciones)


Inicio de la subred: 172.18.26.0
Número de direcciones: 2^(32 - 23) = 2^9 = 512

Sumamos 511 a la dirección inicial (la última dirección válida del bloque):

- 172.18.26.0 + 511 direcciones

  - El bloque incluye: 172.18.26.0 $\rightarrow$ 172.18.27.255

Dirección de broadcast: **172.18.27.255**

### Pregunta 3: Última Dirección Válida y Rango de Hosts
**a) Con la subred 172.30.67.192 y máscara 255.255.255.192, determina cuál es la última dirección de host válida (excluyendo la dirección de broadcast).**

Primero analizamos la máscara y sacamos el número de direciones

255.255.255.192 $\rightarrow$ /26 (es decir, 26 bits de red)

Tamaño de subred: 2^(32 - 26) = 64 direcciones

De esas, 2 se reservan (una para la red y otra para el broadcast), así que hay 62 hosts válidos

Luego calculamos el rango

La subred empieza en 172.30.67.192.
Con un bloque de 64 direcciones, las direcciones van de:

Primera dirección de red: 172.30.67.192

Última dirección (broadcast): 192 + 63 = 255 $\rightarrow$ 172.30.67.255

Última dirección de host válida (antes del broadcast): **172.30.67.254**

**b) Para el host 172.22.53.199 con máscara 255.255.252.0, determina el rango de direcciones válidas (primera y última dirección de host) de la subred.**

Primero analizamos la máscara y sacamos el número de direciones

- 255.255.252.0 $\rightarrow$ /22

- Tamaño de subred: 2^(32 - 22) = 1024 direcciones

Tratamos de encontrar la red a la que pertenece

- /22 cubre bloques de 4 en el tercer octeto

- 53 pertenece al bloque que empieza en 52 (porque 52 es múltiplo de 4)

Entonces:

- Red: 172.22.52.0

- Broadcast: 172.22.55.255

Terminamos determinando el rango de hosts válidos con los datos que tenemos quitando la dirección de red y de broadcast.

- Primera dirección de host: 172.22.52.1

- Última dirección de host: 172.22.55.254

Rango válido: **172.22.52.1 a 172.22.55.254**

### Pregunta 4: Capacidad y Segmentación de Subredes
**a) Calcula el número de equipos (hosts) que pueden conectarse en la red 172.26.0.0 con máscara 255.255.255.192.**

Para calcular el número de hosts posibles primero analizamos la máscara

- 255.255.255.192 $\rightarrow$ 8+8+8+2 = /26

- Tamaño de subred: 2^(32 - 26) = 64 direcciones

Como se quitan dos direcciones, una para red y otra para broadcast nos quedamos con 62 (64-2) dirrecciones para hosts

**b) Dado el host 172.18.171.190/23, identifica a qué subred pertenece, explicando cómo se determina el bloque correspondiente.**



### Pregunta 5: Número de Subredes Necesarias
Explica cómo se determina el número de subredes disponibles utilizando la fórmula:
$$Nº de subredes = 2^S$$

Donde $S$ es el número de bits prestados al identificador de subred. Aplica este concepto a un escenario en el que se requieren al menos 4 subredes para segmentar una red.

Cuando una red se divide en subredes, se “prestan bits” de la parte del host en la dirección IP para convertirlos en parte del identificador de subred.

- S es el número de bits que se toman de la porción de host para usarlos como subred.

- Como cada bit puede tener 2 valores (0 o 1), al tener S bits disponibles, se pueden formar $2^S$ subredes.

**Aplicación práctica**
Supón que tenemos una red Clase C: 192.168.1.0/24

En una red Clase C, normalmente tienes 8 bits para hosts (/24)

Si prestamos 2 bits:

Nueva máscara: /24 + 2 = /26

Subredes posibles: 
$2^2 = 4$

Hosts por subred: 
$2^6 - 2 = 62$ (porque quedan 6 bits para host)

Resultado:

Se generan 4 subredes:

- 192.168.1.0/26

- 192.168.1.64/26

- 192.168.1.128/26

- 192.168.1.192/26

Parte II: Capa de Transporte
Pregunta 6: Comparación entre TCP y UDP
**a) Compara TCP y UDP en términos de:**

**Necesidad de establecer conexión**<br>
**Fiabilidad y control de errores**<br>
**Control de flujo y congestión**<br>
**Velocidad de transmisión**

| Característica                      | TCP (Transmission Control Protocol)               | UDP (User Datagram Protocol)                   |
|--------------------------------     |---------------------------------------------      |----------------------------------------        |
| **Establecimiento de conexión**     | Requiere conexión previa (orientado a conexión)   | No requiere conexión (no orientado a conexión) |
| **Fiabilidad y control de errores** | Fiable: garantiza entrega y orden de los datos    | No garantiza entrega ni orden                  |
| **Control de flujo y congestión**   | Sí, implementa mecanismos como ventana deslizante | No tiene control de flujo ni congestión        |
| **Velocidad de transmisión**        | Más lenta, debido a los controles y garantías     | Más rápida, al ser más ligera y sin controles  |


b) Menciona dos ejemplos de aplicaciones en las que se prefiera usar UDP y justifica la elección.

Los momentos en los que se prefiere emplear el protocolo UDP es en el que no importa que no lleguen algunos paquetes y premia más la velocidad en que se entreguen, por ejemplo, en una retransmisión en directo on en algún videojuego online que la pérdida de algunos paquetes es necesaria para que la retransmisión o el juego tengan la mínima latencia posible.


Pregunta 7: Establecimiento y Terminación de Conexión en TCP
**Describe en detalle el proceso de establecimiento de conexión en TCP (Three-Way Handshake) y el proceso de terminación de la conexión (Four-Way Handshake). Explica la importancia de cada uno de los pasos involucrados.**

Pregunta 8: Multiplexación y Demultiplexación
**Explica el concepto de multiplexación descendente y multiplexación ascendente en la capa de transporte, y proporciona un ejemplo práctico para cada caso.**

Pregunta 9: Cálculo del Tamaño de Ventana en TCP
Se tiene un enlace con los siguientes parámetros:

RTT = 50 ms
Ancho de banda = 100 Mbps
MSS (Tamaño máximo de segmento) = 1,500 bytes
Realiza lo siguiente:

Convierte las unidades necesarias (por ejemplo, RTT a segundos y ancho de banda a bps).
Calcula el tamaño óptimo de la ventana en bits y en bytes usando la fórmula:
Ventana 
o
ˊ
ptima
=
Ancho de banda
×
RTT
Ventana oˊptima=Ancho de banda×RTT
Determina aproximadamente el número de segmentos MSS que pueden estar en tránsito simultáneamente.
Muestra todos los pasos de tu cálculo.

Pregunta 10: Control de Congestión en TCP
Explica brevemente cómo TCP implementa mecanismos de control de congestión, haciendo énfasis en:

El Algoritmo de Arranque Lento (Slow Start)
El Algoritmo de Nagle
El Algoritmo de Clark
Para cada uno, menciona cuál es su objetivo y cómo contribuye a optimizar el rendimiento de la red.

Parte III: Capa de Aplicación y Aplicaciones Multimedia
Pregunta 11: Funcionamiento de DNS
Describe el proceso completo de resolución de nombres en el Sistema de Nombres de Dominio (DNS), desde que el usuario ingresa un dominio en el navegador hasta que se obtiene la dirección IP del servidor.

Pregunta 12: Protocolos de Correo Electrónico
Compara las características de los protocolos POP3, IMAP y SMTP en términos de:

Función principal
Tipo de uso y acceso
Modo de almacenamiento de correos
Incluye ejemplos de situaciones en las que cada uno es más adecuado.

Pregunta 13: Funcionamiento de HTTP y FTP
a) Explica el funcionamiento básico de HTTP, mencionando los métodos más utilizados (GET, POST, PUT, DELETE).
b) Describe el funcionamiento de FTP y señala las diferencias esenciales con HTTP, en especial en lo que se refiere al uso de conexiones (control y datos).

Pregunta 14: Streaming y VoIP
a) Define y compara brevemente los siguientes tipos de streaming:

UDP Streaming
HTTP Streaming
Adaptive HTTP Streaming (DASH)
Menciona un ejemplo de aplicación para cada uno.
b) Explica el proceso de funcionamiento de VoIP (Voz sobre IP) y enumera algunos problemas comunes (como retardo, pérdida de paquetes y eco) junto con posibles soluciones.

Pregunta 15: Control de Congestión en Redes Multimedia
Describe dos técnicas utilizadas para evitar la congestión en aplicaciones multimedia (por ejemplo, el uso de buffering en el cliente o el marcado de paquetes – DiffServ) y explica cómo contribuyen a mejorar la calidad del servicio.

Pregunta 16: Best-Effort vs Servicios Multiclase
Compara el modelo Best-Effort con los Servicios Multiclase, enfatizando:

La manera en que se maneja el tráfico
La garantía (o falta de ella) en la calidad de servicio
Ejemplos de aplicaciones en las que se utiliza cada enfoque
Parte IV: Seguridad en Redes
Pregunta 17: Problemas de Seguridad en Redes
Identifica y explica brevemente las siguientes áreas críticas de seguridad en redes:

Confidencialidad
Autenticación
No repudio
Integridad
Para cada una, menciona una solución o técnica que se emplea para mitigar el riesgo (por ejemplo, cifrado, autenticación multifactor, firmas digitales, etc.).

Pregunta 18: Cifrado Simétrico vs Asimétrico
Realiza una comparación entre cifrado simétrico y asimétrico, abordando:

Número de claves requeridas
Velocidad y eficiencia
Ejemplos de algoritmos y aplicaciones típicas en cada caso
Pregunta 19: Funcionamiento del Algoritmo RSA
a) Describe el proceso de generación de claves en RSA, incluyendo la selección de dos números primos, el cálculo de 
n
n y 
ϕ
(
n
)
ϕ(n), y la determinación de 
e
e y 
d
d.
b) Realiza un ejemplo numérico sencillo (por ejemplo, usando 
p
=
3
p=3, 
q
=
11
q=11, 
e
=
7
e=7) para demostrar el cifrado y descifrado de un mensaje (puedes usar 
M
=
4
M=4).

Pregunta 20: Firewalls, VPN e IPSec
a) Explica el funcionamiento de un firewall, mencionando al menos dos tipos (por ejemplo, filtrado de paquetes y firewall de estado) y su importancia en la protección de la red.
b) Compara VPN e IPSec en términos de propósito, modo de operación y ejemplos de uso (por ejemplo, acceso remoto a recursos corporativos vs. cifrado entre routers).

Pregunta 21: SSL/TLS y DNS Spoofing
a) Describe brevemente el funcionamiento del protocolo SSL/TLS y su importancia para la seguridad en la web (por ejemplo, en HTTPS).
b) Explica qué es el DNS Spoofing y cómo la extensión DNSSEC contribuye a proteger la integridad de las respuestas DNS.
