# Examen de Redes II – *En Busca de la Red Perdida*

---

## Parte I: Conceptos y Teoría

---

### 1. El Mural de las Siete Capas

Te adentras en la sala principal del templo y descubres un gran mural compuesto por siete franjas horizontales superpuestas, decoradas con símbolos y jeroglíficos. Cada franja representa un nivel diferente en un ritual de comunicación. Los sabios de esta civilización entendían que un mensaje debía pasar por varias etapas desde su origen hasta su destino, refinándose o traduciendo su forma en cada nivel de la pirámide comunicativa.

**Pregunta:**  
¿Qué representa el mural de las siete capas en términos de las redes de comunicación modernas? Identifica brevemente cada capa y explica cómo se relaciona este antiguo “modelo” con el proceso de comunicación de datos actual.

> El mural de las siete capas representa el modelo OSI o Modelo de Interconexión de Sistemas Abiertos. Ambas tienen siete capas y además en ambos modelos cada franja representa un nivel diferente en un ritual de comunicación. También sabemos que en el modelo antiguo el mensaje debía pasar por varias capas, en el modelo OSI actual deberá recorrer las siete capas las cuales constan de las siguientes:

---

### 2. Los Dos Pergaminos del Mensajero

En una cámara oculta encuentras dos pergaminos polvorientos. El primero describe el Ritual del Mensajero Confiable: antes de entregar un mensaje, el mensajero realiza un saludo de tres pasos con el receptor para asegurarse de que ambos estén listos, luego entrega el mensaje y espera una confirmación de recibido. Si la confirmación no llega, reintenta el envío. El segundo pergamino narra el Ritual del Mensajero Veloz: un mensajero que sale disparado a entregar mensajes sucesivos sin aviso previo ni asegurarse de la recepción, cubriendo la mayor distancia en el menor tiempo, aunque a veces los mensajes se pierdan en el camino.

**Pregunta:**  
Interpreta los dos rituales descritos. ¿A qué protocolos de comunicación actuales equivalen el mensajero confiable y el mensajero veloz? Compara sus características, explicando las ventajas y desventajas de cada enfoque en redes modernas.

> El mensajero confiable corresponde con el protocolo **TCP** mientras que el mensajero veloz corresponde al protocolo **UDP**.

> Por un lado, el protocolo **TCP** o (*Transmission Control Protocol*), que como bien describe el enunciado en referencia al mensajero confiable, este protocolo realiza ese saludo de tres pasos que hace referencia al *Three-Way Handshake*. En este proceso se establece una conexión segura asegurándose de que el receptor del paquete puede recibirlo de forma correcta antes de transmitir los datos. Además, la espera de la confirmación y el reenvío en caso de encontrar algún error son otras de sus características principales.

>- Entre las ventajas de este protocolo, podemos distinguir que al utilizarlo los datos siempre llegarán completos y ordenados, además del correcto uso de mecanismos de control de flujo y de congestión para poder mejorar la comunicación.
>- Pero este protocolo también cuenta con ciertos inconvenientes como son la latencia que tendrá el envío de los datos debido a los múltiples pasos que realiza en el envío, además de un mayor consumo.

> Por otro lado, el protocolo **UDP** o (*User Datagram Protocol*) se caracteriza por el envío de paquetes a gran velocidad, pero sin establecer una conexión previa y sin verificar si llegaron los paquetes de forma adecuada.

>- Las ventajas más notorias de este protocolo son su velocidad y eficiencia en cuanto a su rendimiento.
>- Aunque también cuenta con desventajas como que no se garantiza una entrega completa y ordenada y puede haber pérdidas de los datos.
---

### 3. El Enigma de las Subredes

Avanzando por un pasillo, encuentras una losa de piedra con inscripciones que parecen ser direcciones numéricas. Una inscripción cuenta:  
*"Nuestro reino digital tenía la dirección sagrada 192.168.50.0. Los cuatro grandes gremios de la ciudad exigían su propio distrito en la red, todos de igual tamaño".*  
Junto a esto, ves un diagrama borroso de algo que parecen ser subredes emanando de la dirección principal, cada una con su propio identificador.

**Pregunta:**  
Descifra el enigma de la losa. Si la antigua red usaba la dirección 192.168.50.0 como base y necesitaba dividirse en 4 subredes de igual tamaño (una para cada gremio), ¿qué máscara de subred habrían utilizado los antiguos para lograrlo? ¿Cuántas direcciones de host (utilizables) tendría cada subred resultante? Explica brevemente tu razonamiento al calcular la máscara.

> Primero, debemos identificar la clase de la dirección, en este caso la dirección 192.168.50.0 pertenece a la clase **C**. Esto nos indica que de forma predeterminada tendría la máscara 255.255.255.0 (/24), esta máscara proporciona 256 direcciones a las cuales se le restan dos direcciones que se reservan para la dirección de red y la de broadcast. Por esa razón contamos realmente con **254 direcciones útiles**.

> Segundo, ahora determinamos la cantidad de bits que vamos a necesitar para las cuatro subredes. En la red de clase C con máscara /24 tendremos 8 bits para los hosts. Para poder contar con cuatro subredes será necesario restarle **dos bits adicionales** de la parte del host. Por lo tanto, para la máscara de subred vamos a contar con **26 bits** en vez de 24 y en la parte de host contaremos con **6 bits** en vez de 8. La máscara pasará a ser la **/26 o 255.255.255.192**.

> Tercero, pasaremos ahora a calcular cuánto host tiene cada subred y cuántos de ellos serán utilizables. Como ya he dicho anteriormente sabemos que cada subred cuenta con 6 bits para los hosts correspondientes, por lo tanto, contaremos con 2⁶ = **64 direcciones por subred**. Pero solo serán **utilizables 62**, ya que la primera será para la dirección de red, y la última será para la dirección de broadcast.

---

#### Esta tabla representa el rango de las direcciones por cada subred:

| Subred | Dirección de Red     | Primer Host         | Último Host         | Dirección de Broadcast |
|--------|-----------------------|----------------------|----------------------|--------------------------|
| 1      | 192.168.50.0/26       | 192.168.50.1         | 192.168.50.62        | 192.168.50.63            |
| 2      | 192.168.50.64/26      | 192.168.50.65        | 192.168.50.126       | 192.168.50.127           |
| 3      | 192.168.50.128/26     | 192.168.50.129       | 192.168.50.190       | 192.168.50.191           |
| 4      | 192.168.50.192/26     | 192.168.50.193       | 192.168.50.254       | 192.168.50.255           |

---
### 4. La Encrucijada de las Rutas

Llegas a una encrucijada dentro de las ruinas: cuatro caminos diferentes se extienden hacia distintas aldeas en los alrededores de la ciudad antigua. En el centro, un tótem tallado muestra flechas apuntando hacia cada camino, con inscripciones de destinos y distancias. Notas que algunas flechas parecen fijas e inmutables (talladas en la piedra), mientras que otras son piezas móviles que pudieron reorientarse si se abría o cerraba algún camino en el pasado. Este tótem se asemeja a un antiguo dispositivo de enrutamiento que dirigía el tráfico de datos por el camino adecuado.

> **Pregunta:**  
> ¿Qué concepto moderno de redes representa el tótem con flechas de la encrucijada? Explica qué es una tabla de enrutamiento y cómo funciona en un router actual. Además, interpreta la diferencia entre las flechas talladas en piedra y las flechas móviles en términos de enrutamiento estático vs. enrutamiento dinámico en redes.

**Respuesta:**

El tótem representa el concepto moderno de **tabla de enrutamiento**, el cual es un componente fundamental en los routers actuales.

Una tabla de enrutamiento es un conjunto de normas que se almacena en el router y que tiene como función principal escoger el camino que tomarán los paquetes para llegar de forma óptima a su destino. Esta tabla funciona como un mapa. Cada entrada en la tabla suele incluir:

- Una red de destino (donde se dirige).
- Una máscara de subred (rango de direcciones dentro de la red de destino).
- Su próximo salto (dirección del router al que se debe enviar para seguir su camino).
- Una interfaz de salida (la interfaz del router que será utilizada para enviar el paquete).
- Una métrica (valor que indica la calidad de la ruta).

Las **flechas talladas en piedra** representan el **enrutamiento estático**, caracterizado por caminos fijos que se configuran manualmente y no pueden cambiar automáticamente, aunque el camino deje de estar disponible. Es más apropiado en redes pequeñas o cuando se requiere un control más preciso.

Las **flechas móviles** representan el **enrutamiento dinámico**, caracterizado por rutas ajustables que pueden modificarse según el estado de la red. Si una conexión falla y el camino se cierra, el sistema puede calcular una nueva ruta automáticamente. Este sistema utiliza protocolos de enrutamiento como **OSPF**, **BGP** o **RIP**, que son capaces de intercambiar información entre routers para actualizar las tablas de enrutamiento.

---

### 5. El Guardián de la Máscara Única

En la última sala del templo, frente a la salida, te encuentras con la estatua de un guardián con dos caras. Según una leyenda grabada en la base, este guardián protegía la ciudad oculta de los forasteros. Cuando un mensajero salía de la ciudad, el guardián reemplazaba su máscara por la suya propia, de modo que, para el mundo exterior, todos los mensajes parecían venir únicamente del guardián. Al regresar la respuesta, el guardián recordaba qué máscara original correspondía a cada mensaje y reenviaba la respuesta al habitante correcto dentro de la ciudad. Gracias a este ardid, la ciudad pudo ocultar la identidad de sus miembros y usar un único rostro para todas sus comunicaciones externas.

> **Pregunta:**  
> ¿Qué técnica de redes moderna se refleja en la leyenda del Guardián de la Máscara? Nombra y describe brevemente este mecanismo, explicando cómo permite que múltiples dispositivos internos de una red compartan una única identidad (dirección) al comunicarse con el exterior, y menciona dos beneficios que brinda esta estrategia a las redes actuales.

**Respuesta:**

La leyenda del Guardián con dos caras se asemeja a la técnica moderna conocida como **NAT (Network Address Translation)**. Este es un mecanismo que permite que varios dispositivos dentro de una red privada utilicen la **misma dirección IP pública** para comunicarse con el exterior.



**Beneficios de NAT:**

- **Reducción del uso de direcciones IPv4:** Se utiliza solo una IP pública para múltiples dispositivos.
- **Mayor seguridad:** Oculta las IPs internas, dificultando el acceso directo desde el exterior.

---

> _Profesor, tómese un respiro. Ha guiado a su alumnado a través de los enigmas teóricos de esta antigua civilización. Ahora, prepárese para la siguiente fase: reconstruir las redes que alguna vez hicieron vibrar esta metrópolis tecnológica. ¡Ánimo, que aún queda camino por recorrer! 😆_


