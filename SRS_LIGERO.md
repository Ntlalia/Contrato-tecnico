# Especificación de Requisitos (SRS) 

      ## Sistema Inventario

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

 Historias de Usuario de la tarea anterior, aplicadas a este ejemplo del inventario.

 ### Pedido original del cliente
"Hola, necesitamos una plataforma web para registrar nuestros productos. Queremos controlar las existencias de manera estricta y que avise cuando queden pocas unidades de algo. La base de datos debe ser PostgreSQL porque ya tenemos ese servidor configurado, y el sistema debe validar los códigos de barra de El Salvador."

### Requisitos No Funcionales

- **Consistencia de datos**: El sistema debe reflejar en todo momento el nivel real de existencias, sin discrepancias entre lo registrado y el stock físico.
- **Persistencia**: Toda la información de productos e inventario debe almacenarse en PostgreSQL, motor de base de datos ya configurado por el cliente.
- **Validación de entrada**: El sistema debe rechazar cualquier código de barras que no cumpla con el formato estándar de El Salvador.
- **Alertas oportunas**: Las notificaciones de stock bajo deben generarse de forma inmediata al cruzar el umbral mínimo configurado.

---

### HU-01: Registrar un nuevo producto

**COMO** encargado de la tienda
**QUIERO** registrar un nuevo producto con su nombre, código de barras, cantidad y precio
**PARA** mantener actualizado el catálogo de inventario

**Escenario: Registro exitoso de un producto**
```
Dado que el encargado ha iniciado sesión en la plataforma
Cuando ingresa nombre, código de barras válido, cantidad y precio, y presiona "Guardar"
Entonces el sistema debe registrar el producto en la base de datos
Y debe mostrar el producto en el listado de inventario
```

**Escenario: Intento de registro con código de barras inválido**
```
Dado que el encargado está registrando un nuevo producto
Cuando ingresa un código de barras que no cumple el formato estándar de El Salvador
Entonces el sistema debe rechazar el registro
Y debe mostrar un mensaje indicando que el código de barras es inválido
```

---

### HU-02: Recibir alerta de stock bajo

**COMO** encargado de la tienda
**QUIERO** recibir una alerta automática cuando un producto tenga pocas unidades
**PARA** reabastecer a tiempo y no quedarme sin inventario

**Escenario: El stock de un producto baja del umbral mínimo**
```
Dado que un producto tiene definido un umbral mínimo de existencias
Cuando la cantidad disponible del producto cae por debajo de ese umbral
Entonces el sistema debe generar una alerta visible para el encargado
Y la alerta debe indicar el nombre del producto y la cantidad restante
```

**Escenario: El stock se mantiene por encima del umbral**
```
Dado que un producto tiene definido un umbral mínimo de existencias
Cuando la cantidad disponible es igual o mayor a ese umbral
Entonces el sistema no debe generar ninguna alerta
```

---

### HU-03: Validar el código de barras al registrar un producto

**COMO** encargado de la tienda
**QUIERO** que el sistema valide automáticamente el formato del código de barras
**PARA** evitar registrar productos con códigos incorrectos o duplicados

**Escenario: Código de barras válido**
```
Dado que el encargado ingresa un código de barras con formato estándar de El Salvador
Cuando presiona "Guardar"
Entonces el sistema debe aceptar el código y continuar con el registro del producto
```

**Escenario: Código de barras duplicado**
```
Dado que el encargado ingresa un código de barras que ya existe en el inventario
Cuando presiona "Guardar"
Entonces el sistema debe rechazar el registro
Y debe mostrar un mensaje indicando que el producto ya está registrado
```



##  Matriz de Trazabilidad


| ID Requisito | Descripción                                                          | Historia de Usuario | Prioridad |
|---------------|---------------------------------------------------------------    --|----------------------|-----------|
| RF-01         | Validar código de barras formato El Salvador                        | HU-03                | Alta      |
| RF-02         | Registrar productos con nombre, código, cantidad y precio           | HU-01                | Alta      |
| RF-03         | Emitir alerta automática cuando el stock esté por debajo del mínimo | HU-02                | Alta      |
| RNF-01        | Usar PostgreSQL como motor de base de datos obligatorio             | —                    | Alta      |
