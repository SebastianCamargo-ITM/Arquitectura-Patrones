Para la reingeniería del sistema de chat, se ha seleccionado el estilo arquitectónico de microservicios. Este enfoque permite dividir las funcionalidades del monolito en microservicios independientes que se comunican entre sí de la siguiente manera: 

 

### Servicio de Mensajería:
Maneja el envío y recepción de mensajes de texto y multimedia. 

### Servicio de Multimedia: 
Procesa y almacena contenido multimedia. 

### Servicio de Autenticación y Autorización:
Gestiona la autenticación de usuarios y la autorización de solicitudes. 

### Servicio de Pagos:
Maneja las transacciones y pagos dentro del sistema. 

### Servicio de Subscripción a Canales:
Utiliza el patrón Observer para manejar la lógica de suscripción y notificación de usuarios. 

### Servicio de Publicidad:
Gestiona y envía publicidad personalizada a los usuarios. 

El módulo de subscripción a canales permitirá a los usuarios suscribirse a canales de interés y recibir notificaciones cuando haya nuevas publicaciones. Este módulo será un microservicio independiente en la arquitectura de microservicios, implementando el patrón de diseño Observer. 

 

## Patrones Arquitectónicos Implementados 

* Database per Service: Cada microservicio utiliza su propia base de datos distribuida para asegurar independencia y escalabilidad. 

* Event-Driven Architecture: Utilizará eventos mediante colas de mensajes para la comunicación entre servicios incluso si los servicios están temporalmente inactivos, pues actuaría como un buffer para manejar picos de carga y asegurar la entrega de mensajes en caso de fallos temporales. El Servicio de Mensajería puede publicar un evento cuando se recibe un nuevo mensaje, y el Servicio de Subscripción a Canales puede escuchar este evento para notificar a los usuarios. Adicionalmente, se usa para encolar los videos que requieren procesamiento. 

* API Gateway: Un punto de entrada único para todas las solicitudes de los clientes, manejando autenticación, autorización y enrutamiento a los microservicios correspondientes. 

* Service Discovery: Utiliza Eureka para permitir que los microservicios se encuentren y se comuniquen entre sí dinámicamente. 

* Load Balancer: Utiliza Nginx como balanceador de carga para distribuir el tráfico entre las instancias del API Gateway y los microservicios solicitados. 

 

## Uso del Patrón Observer 

El patrón Observer se utilizará para la notificación eficiente de eventos dentro de los microservicios, asegurando una reacción oportuna y correcta a eventos clave como el procesamiento de un nuevo video cuando se encola, cuando un archivo multimedia se almacena o para las notificaciones nuevas de publicaciones del módulo de publicidad. 

 

 

## Cache Distribuido 

Adicionalmente se propone un sistema de cache distribuido para almacenar los datos frecuentemente accedidos, reduciendo la carga en las bases de datos. 

 

## Escalamiento Horizontal 

El conjunto de patrones, estilos y arquitecturas seleccionadas facilitan el escalamiento horizontal de la solución pues se busca que la solución tenga un bajo nivel de acoplamiento y que, aprovechando el estilo arquitectónico de microservicios puede ser escalada de forma independiente, sin tener que modificar la arquitectura planteada cada vez gracias al uso de balanceadores de carga para garantizar la alta disponibilidad incluso cuando algunas instancias fallan o están sobrecargadas  y del registro de servicios y API Gateway ya que actúan como un único punto de entrada para todas las solicitudes entrantes, lo que facilita la gestión de la carga pues en combinación con servicios de orquestación de contenedores o plataformas en la nube, el API Gateway puede permitir el escalado automático de los servicios en función de la demanda, lo que contribuye al escalado horizontal. 

## Arquitectura Propuesta 

A continuación, se presenta el diagrama con todos los componentes y sus interacciones que representan la arquitectura propuesta de la solución.

![Diagrama de Componentes drawio](https://github.com/SebastianCamargo-ITM/Arquitectura-Patrones/assets/160674875/b8981385-fe20-49f5-bbc4-e24f3171ae44)
