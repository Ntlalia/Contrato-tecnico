# Especificación de Requisitos (SRS) - Sistema Inventario

## Alcance y Fronteras del Software

El sistema será una plataforma web para la gestión de inventario de una tienda local. Dentro del alcance, el sistema podra realizar las siguientes acciones.

- Registrar productos (nombre, código de barras, cantidad disponible, precio, categoría).
- Consultar, actualizar y eliminar productos del catálogo.
- Controlar las existencias de manera estricta, reflejando en tiempo real la cantidad disponible de cada producto.
- Emitir alertas automáticas cuando el nivel de stock de un producto caiga por debajo de un umbral mínimo definido.
- Validar que los códigos de barra ingresados correspondan al formato estándar utilizado en El Salvador.

**Fuera del alcance** 

- Procesamiento de ventas o generación de facturas.
- Integración con pasarelas de pago.
- Aplicación móvil nativa (el sistema es exclusivamente una plataforma web).
- Gestión de múltiples sucursales o bodegas.
- Reportes financieros o contables avanzados.

##  Restricciones Tecnológicas Obligatorias

- **Base de datos**: El sistema debe implementarse obligatoriamente sobre PostgreSQL, ya que el cliente cuenta con este servidor previamente configurado. No se permite el uso de otro motor de base de datos.
- **Validación de códigos de barra**: El sistema debe validar que los códigos de barra ingresados cumplan con el formato estándar utilizado en El Salvador, rechazando entradas que no cumplan dicho formato.

##  Requisitos de Calidad (IEEE 830)

- **Confiabilidad**: El sistema debe reflejar de manera consistente y estricta el nivel real de existencias, evitando discrepancias entre el inventario físico y el registrado.
- **Usabilidad**: La interfaz debe permitir a personal no técnico de la tienda registrar productos y consultar existencias sin necesidad de capacitación extensa.
- **Rendimiento**: Las alertas de stock bajo deben generarse de forma inmediata al momento en que la cantidad de un producto cruce el umbral mínimo, sin retrasos perceptibles para el usuario.
- **Disponibilidad**: El sistema debe estar accesible durante el horario operativo de la tienda para permitir el registro continuo de movimientos de inventario.
- **Mantenibilidad**: El código y la estructura de la base de datos deben permitir agregar nuevas funcionalidades

 Historias de Usuario


Pedido original del cliente
Dev, quiero que los choferes vean viajes cercanos en tiempo real, pero que sea seguro y no se roben los datos. Y que si aceptan, les diga la ruta más corta para no gastar gas. Ah, y que la app no se trabe si hay 1,000 personas al mismo tiempo.




Requisitos No Funcionales


Seguridad: Toda comunicación entre la app del chofer y el servidor debe ser cifrada (SSL/TLS), para evitar el robo  de datos.

Rendimiento: El sistema debe soportar al menos 1,000 usuarios conectados de forma simultánea sin que la aplicación se caiga y afecte los tiempos de respuesta.

Disponibilidad y Estabilidad: La aplicación no debe trabarse ni caerse bajo demasiados usuarios conectados simultáneamente .

Tiempo real: La ubicación de los viajes cercanos debe actualizarse en tiempo real,  (latencia baja, idealmente menor a 3 segundos).



Ver viajes cercanos en tiempo real

COMO chofer registrado en la plataforma
QUIERO: ver en tiempo real los viajes disponibles cerca de mi ubicación actual
PARA: poder elegir y aceptar el viaje más conveniente sin perder tiempo


Visualización de viajes cercanos en tiempo real

  Escenario: El chofer puede ver viajes disponibles cerca de su ubicación
    Dado que el chofer ha iniciado sesión y activó su ubicación GPS
    Cuando existan viajes solicitados dentro de su radio
    Entonces el sistema debe mostrar dichos viajes en el mapa en tiempo real
    Y la lista debe actualizarse automáticamente sin que el chofer recargue la app

  Escenario: No hay viajes cercanos disponibles
    Dado que el chofer ha iniciado sesión y activó su ubicación GPS
    Cuando no existan viajes solicitados dentro del radio configurado
    Entonces el sistema debe mostrar un mensaje indicando que no hay viajes cercanos




Recibir la ruta más corta al aceptar un viaje

COMO: chofer que acepta un viaje
QUIERO: que la aplicación me muestre automaticamente la ruta más corta hacia el punto de recogida
PARA: ahorrar combustible y tiempo durante el trayecto



Cálculo de la ruta más corta al aceptar un viaje

  Escenario: El chofer acepta un viaje y recibe la ruta mas conveniente 
    Dado que el chofer visualiza un viaje disponible
    Cuando el chofer presiona el botón "Aceptar viaje"
    Entonces el sistema debe calcular y mostrar la ruta más corta hacia el punto de recogida
    Y la ruta debe considerar el tráfico actual para optimizar el consumo de combustible

  Escenario: Falla el cálculo de ruta por pérdida de conexión
    Dado que el chofer acepta un viaje
    Cuando el sistema no logre calcular la ruta por falta de conexión a internet
    Entonces la app debe notificar al chofer del error
    Y debe permitir reintentar el cálculo de la ruta manualmente

##  Matriz de Trazabilidad

 ID Requisito    Descripción                                                     | Historia de Usuario | Prioridad |

| RF-01          Validar código de barras formato El Salvador                    | HU-03                | Alta      |
| RF-02         | Registrar productos con nombre, código, cantidad y precio       | HU-01                | Alta      |
| RF-03         | Emitir alerta automática cuando el stock esté por debajo del mínimo | HU-02             | Alta      |
| RNF-01        | Usar PostgreSQL como motor de base de datos obligatorio          | —                    | Alta      |
