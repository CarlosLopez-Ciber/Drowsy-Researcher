# Topologías de Red LAN: Arquitectura y Diseño Físico

Cuando se diseña una Red de Área Local (LAN), no basta con tener los dispositivos y los cables; es crucial definir cómo se interconectarán. Esta disposición física o lógica determina la eficiencia con la que viajan los datos y qué tan resistente será la red ante posibles fallas.

En este artículo exploraremos el concepto de topología de red y los esquemas más utilizados en la industria.

### <mark style="color:yellow;">¿Qué es una Topología de Red?</mark>

La topología se define como el mapa físico o lógico de una red. Representa la disposición geométrica de los nodos (computadoras, impresoras, servidores) y los medios de transmisión (cables) que los enlazan.

La elección de una topología adecuada es crítica porque impacta directamente en cuatro áreas clave:

1. **Rendimiento:** La velocidad y fluidez del tráfico de datos.
2. **Escalabilidad:** La facilidad para agregar nuevos equipos.
3. **Tolerancia a fallos:** La capacidad de la red para seguir operando si un cable o dispositivo se rompe.
4. **Mantenimiento:** La complejidad para detectar y reparar errores.

***

### <mark style="color:yellow;">Tipos de Topologías LAN</mark>

#### <mark style="color:$danger;">1. Topología en Bus (Bus Topology)</mark>

Es una de las arquitecturas más antiguas y sencillas.

* **Descripción:** Todos los dispositivos se conectan a un único cable central, conocido como _backbone_ o troncal. Los datos enviados por un nodo viajan a lo largo del cable en ambas direcciones hasta encontrar al destinatario.
* **Ventajas:**
  * Es muy económica y requiere menos cableado que otras opciones.
  * Fácil de implementar en instalaciones muy pequeñas o temporales.
* **Desventajas:**
  * **Punto único de fallo:** Si el cable principal se corta, toda la red deja de funcionar.
  * El rendimiento disminuye drásticamente a medida que se agregan más dispositivos (colisiones de datos).

<figure><img src="https://virima.com/wp-content/uploads/2024/07/Bus-topology-1024x512.png.webp" alt=""><figcaption></figcaption></figure>

#### <mark style="color:$danger;">2. Topología en Estrella (Star Topology)</mark>

Es el estándar actual para la mayoría de las redes LAN Ethernet (oficinas y hogares).

* **Descripción:** Cada dispositivo tiene un enlace dedicado y directo hacia un nodo central, que suele ser un Switch o un Hub. El nodo central actúa como un repetidor o conmutador de tráfico.
* **Ventajas:**
  * **Facilidad de gestión:** Es sencillo agregar o quitar dispositivos sin interrumpir al resto.
  * **Aislamiento de fallos:** Si un cable individual falla, solo ese dispositivo pierde conexión; el resto de la red sigue operando.
* **Desventajas:**
  * Dependencia crítica del nodo central: Si el Switch falla, toda la red queda inoperativa.
  * Requiere más cableado que la topología de bus.

<figure><img src="https://virima.com/wp-content/uploads/2024/07/Star-topology-1024x512.png.webp" alt=""><figcaption></figcaption></figure>

#### <mark style="color:$danger;">3. Topología en Anillo (Ring Topology)</mark>

* **Descripción:** Los dispositivos se conectan en un circuito cerrado (círculo), donde cada nodo está conectado exactamente a otros dos (el anterior y el siguiente). Los datos viajan en una única dirección pasando por cada nodo hasta llegar a su destino.
* **Ventajas:**
  * Ofrece un rendimiento predecible y ordenado, ya que elimina las colisiones de datos típicas del Bus.
* **Desventajas:**
  * En una configuración simple, si un solo nodo o enlace falla, el círculo se rompe y toda la red cae (a menos que se utilice una topología de doble anillo para redundancia).

<figure><img src="https://virima.com/wp-content/uploads/2024/07/Ring-topology-1024x512.png.webp" alt=""><figcaption></figcaption></figure>

#### <mark style="color:$danger;">4. Topología en Malla (Mesh Topology)</mark>

Es común en redes donde la continuidad del servicio es la prioridad absoluta.

* **Descripción:** Cada dispositivo está conectado directamente a todos (malla completa) o a varios (malla parcial) de los demás dispositivos de la red. No existe una jerarquía central estricta.
* **Ventajas:**
  * **Alta redundancia:** Es la topología más robusta. Si un cable se corta, los datos toman automáticamente una ruta alternativa.
* **Desventajas:**
  * Es extremadamente costosa debido a la gran cantidad de cables y puertos necesarios.
  * Su instalación y configuración son complejas.

<figure><img src="https://virima.com/wp-content/uploads/2024/07/Mesh-topology-1024x512.png.webp" alt=""><figcaption></figcaption></figure>

#### <mark style="color:$danger;">5. Topología Híbrida</mark>

En el mundo real, las redes grandes rara vez son puras; suelen ser una mezcla.

* **Descripción:** Integra dos o más topologías básicas para aprovechar las fortalezas de cada una. Por ejemplo, varias redes en "Estrella" interconectadas a través de un enlace en "Bus".
* **Ventajas:**
  * **Flexibilidad:** Permite adaptar el diseño a las limitaciones físicas del edificio o a las necesidades de expansión de la empresa.
* **Desventajas:**
  * La administración y detección de errores puede volverse compleja debido a la mezcla de arquitecturas.

<figure><img src="https://virima.com/wp-content/uploads/2024/07/hybrid-topology-1024x512.png.webp" alt=""><figcaption></figcaption></figure>
