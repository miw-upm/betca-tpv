# Tecnología Spring: Proyecto TPV - Back-end
### Back-end con Tecnologías de Código Abierto (SPRING)
### [Máster en Ingeniería Web por la U.P.M.](http://miw.etsisi.upm.es)
---

# Curso 2021-22. Enunciado de prácticas

## `story: TPV`
> **Autor: Jesús Bernal**  
> **GitHub: [@miw-upm](https://github.com/miw-upm)**   
> **User on commit: `jbernal`**

- [X] Crear las arquitecturas de los proyectos & Core.

## `story: Article Family CRUD`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Permitir realizar un CRUD de las familias de artículos.
- [ ] En el menú de administración, al pulsar **Article Family**, cambia a la vista de la pantalla principal para su gestión.
- [ ] Se permite realizar las funciones CRUD.

![](https://github.com/miw-upm/betca-tpv/blob/main/docs/family-crud.png)

## `story: Article Family View`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Permitir la búsqueda de productos mediante agrupaciones jerárquicas. Un artículo puede pertenecer a varias familias. Aquí se utiliza el **patrón Composite**. El modelo de entidades ya está resuelto en BD con un conjunto de datos para probar.
- [ ] Cuando se pulsa el botón de agrupaciones (es un triangulo, cuadrado y circulo juntos) en la página del carrito de la compra, se muestra un dialogo con el contenido de `root`, que es el primer nivel.
- [ ] Si se pulsa sobre uno de tipo `ARTICLE` se añade al carro de la compra.
- [ ] Si se pulsa sobre un `SIZES` se muestra dialogo con todas las tallas con su stock que son de tipo `ARTICLE`. La talla se encuentra al final de la descripción del artículo. Al elegir uno se cierra el dialogo y se añade al carro de la compra.
- [ ] Si se pulsa sobre un tipo `ARTICLES`, se cambia el contenido de la familia dentro del dialogo.

![](https://github.com/miw-upm/betca-tpv/blob/main/docs/family-view.png)

## `story: Article Size Family Creation`
> **Autor: Hao Liu**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Permitir realizar una creación rápida de familias de tallas de artículos de un solo proveedor, incluyendo la creación de artículos con asignación automática de código, 840000000000x y hasta el 840000099999x (EAN13), Habrá que consultar la BD y controlar su valor. Las tallas podrían ser 0..60, se podrá configurar la distancia entre tallas, o "XXS", "XS", "S", "M", "L", "XL", "XXL", "XXXL", "Especial".
- [ ] En el menú de administración, al pulsar **Articles Sizes Family Creator**, muestra un dialogo para la creación.
- [ ] Una vez rellenado se crea la familia de tallas.

![](https://github.com/miw-upm/betca-tpv/blob/main/docs/family-creator.png)

## `story: Budgets`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar los presupuestos. Es similar a un ticket, pero sin la gestión de pago.
```typescript
class Budget {reference:String; creationDate:LocalDate; shoppings:Shopping[];}
```
- [ ] Una vez relleno un carro de la compra, si se pulsa **Budge** se genera el presupuesto con código QR de la referencia.
- [ ] Se permite rellenar un carro de la compra desde un presupuesto, si el precio hubiese cambiado, se le aplica el descuento necesario. La búsqueda es de tipo __like__, si la respuestas son varios, muestra un dialogo para que se elija entre las encontrados. Tienen una caducidad de un mes.

## `story: Cashier`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Registrar movimientos de caja: ingresos o extracciones de dinero de la caja. Permitir procesar los cierres de caja.
- [ ] Si se pulsa en el menú de administración **Cash Movement**, abre un dialogo para realizar un movimiento de efectivo de caja. En el proceso de cierre de caja, existe el botón **Cash movement** que lanza el mismo dialogo. Solo se permite si la caja está abierta.
- [ ] Si se pulsa en el menú de administración **Cashier Closure**, se cambia de visualización para ver los cierres de caja.
- [ ] Tiene un filtro para buscar el mes presente, un mes concreto, año presente o un año concreto.
- [ ] Después de buscar, muestra al principio de la página, los totales.

## `story: Complaints`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Quejas de productos comprados. Son quejas por productos que no son satisfactorios, porque no cumplen las espectativas.
```typescript
class Complaint{reference:String; registrationDate:LocalDate; mobile:String; barcode:String; description:String, state:Opened|Closed; reply:String;}
```
- [ ] El cliente, una vez logeado, puede poner una reclamación.
- [ ] El cliente puede ver sus quejas, y puede actualizar la descripción. También puede eliminarla si se arrepiente.
- [ ] El empleado (MANAGER), puede establecer la respuesta y se evoluciona a cerrado. En este caso, el cliente, ya no la puede eliminar.


## `story: Credit Line`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar una línea de crédito de clientes especiales.
```typescript
class Credit{user:User; creationDate:LocalDate; sales:CreditSale[] }
class CreditSale{ticket:Ticket, payed:Boolean}
```
- [ ] En el menú de administración, crear una línea de crédito para un usuario.
- [ ] En el menú de administración, se podrá listar los usuarios con deuda, y su deuda total.
- [ ] En el proceso de pago de un ticket, ampliarlo para que se pueda pueda pagar con una línea de crédito. En este caso, el cash es 0, y no habrá ingresos en caja, pero se añade a la lista del cliente con el estado de no pagado.
- [ ] En la administración, permitir que el cliente pague un conjunto de tickets pendientes. Esto solo se puede realizar con la caja abierta, y se debe alterar el estado de **cash** y **card**, dependiendo como pague, y añadiendo un mensaje al campo **note**, de la operación realizada.

## `story: Customer Discount`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar el descuento de los clientes especiales, tienen descuento en todas sus compras siempre que sean superiores a una cantidad.
```typescript
class CustomerDiscount {user:User; note:String; registrationDate:LocalDate; discount:Integer; minimmumPurchase:Integer; }
```
- [ ] En la pantalla del carrito de la compra, se debe poder aplicar el descuento a un cliente especial, a través de su móvil.
- [ ] Permitir CRUD sobre los descuentos de clientes.

## `story: Customer Points`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar los puntos de clientes. En función de la compra del usuario (de la cantidad) se darán una serie de puntos. Se almacena la fecha de la última vez que se añadieron puntos. Si durante un año, no se realizan compras, se pierden los puntos. Cuando se leen los puntos o se modifican, es un buen momento para comprobar su validez, pero existen otras opciones. Los puntos equivalen a dinero que se puede descontar en una compra, pero no puede superar al 50% del valor de la compra y hay un mínimo de puntos para canjear.
```typescript
class CustomerPoints{user:User; value:Integer; lastDate:LocalDate; }
```
- [ ] En el carrito de la compra, se permite el consumo de puntos de un usuario.
- [ ] Cuando se realiza una compra, si el ticket tiene asociado un usuario, añadir los puntos.
- [ ] Si un ticket está asociado a un usuario, en la impresión del ticket se le indica los puntos acumulados hasta el momento.
- [ ] El usuario puede consultar los puntos dentro de su perfil.

## `story: Customer Reviews`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestión de votaciones con comentarios de los productos comprados, con valores 1..5, utilizando algún elemento visual, por ejemplo estrellas. Esta funcionalidad se encuentra en la página de Home, está programado en Python.
```typescript
class Review{user:User; article:Article; stars:Integer; opinion:String}
```
- [ ] El usuario puede ver sus productos comprados, y valorar cada uno de ellos con un voto (stars) (1..5) y un comentario.
- [ ] El usuario puede cambiar sus valoraciones.
- [ ] Implementar un método que devuelve los artículos mas valorados, debe situarse en Home, y se resuelve en el menú secundario `adviser - Popular`. Esta relacionada con la historia `News`

## `story: Data Protection Act`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Ley de Protección de Datos. existen tres niveles:
* Básico Se conceden permisos para registrar los datos única y exclusivamente para realizar correctamente la compra y envío de los productos de la tienda.
* Medio: Además del anterior, el usuario concede permisos para que se realicen envíos informándole de ofertas u oportunidades especiales para adquirir productos en oferta.
* Avanzado: Incluye todo lo del contrato medio, y además el usuario concede permiso para que la empresa ceda sus datos a terceros.
  El texto a firmar podría ser:
  [una aproximación del texto a imprimir para firmar](https://github.com/miw-upm/betca-tpv/blob/main/docs/data-protection-act.txt)

```typescript
enum RgpdType{BASIC,MEDIUM,AVANCE}
class Rgpd{user:User, type:RgpdType, agreement:byte[]}
```
- [ ] En el menú de administración, en **Data Protection Act**, dado un usuario, te informa si tiene aceptado el tratamiento de datos, y te deja bajarte el texto firmado.
- [ ] Además, te permite imprimir un texto con los datos del usuario y el texto legal.
- [ ] Te deja subir el fichero con el texto y firma, y se le asocia al cliente un nivel.

## `story: Gift Tickets`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Es un documento que referencia a un ticket con una `reference` no predecible. Se puede añadir un mensaje personalizado. La `reference` se imprime con el código QR
```typescript
class GiftTicket {reference:String; message:String; ticket:Ticket;}
```
- [ ] En el proceso de Check-out se puede activar y se imprime aparte, debe aparecer los datos básicos de la empresa y la fecha de caducidad.
- [ ] Debe ser posible localizar un ticket a partir del ticket-regalo, en el CRUD tickets.

## `story: Github Issues`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Conectar con GitHUb para la publicación de un issue por problemas con la aplicación.
- [ ] En el menú de administración, **Publish a Issue**, saca un formulario para rellenar y publicar un Error/Mejora de la aplicación como un `issue`, en el repositorio betca-tpv. Debería tener `title`, `body` con el conenido del issue, `label` (bug o enhancement).
- [ ] En el menú de administración, te permite leer los issues (bug, enhancement), indicando si esta asignado, si esta abierto/cerrado, el hito asociado estimado y la fecha de creación, además de los datos enviados.
- [ ] Cuando se ejecutan los test, se utilizan mooks, y no se envía a GitHub, y no pueden fallar aunque no se tenga la variable de entorno GITHUB_SECRET definida.

Para mas información: https://docs.github.com/en/free-pro-team@latest/rest/reference/issues#create-an-issue.

Para la autenticación se realiza mediante Basic Auth, con usuario:'miw-upm' y clave '${GITHUB_SECRET}'. La api-key se debe solicitar al profesor y tenerla siempre oculta mediante variable de entorno. Se consigue en la ruta: `Perfil de cunta >> Settings > Developer settings > Personal access tokens` Si se utiliza en ejecución local, y no existe la variable de entorno, debe lanzar una excepción indicando el problema.

## `story: Invoices`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Implementar la creación de facturas. Deberá tener los datos completos del usuario (DNI, nombre completo y dirección completa). Cuando se cree una factura se debe calcular **baseTax** & **tax**. Un ticket puede tener solo una factura positiva y varias negativas. Tener en cuenta que cada artículo puede tener un Tax diferente. El precio de los artículos es con Tax incluido.
Por cada articulo, se calcula: **baseTax=retailPrice/(1+Tax/100)** & **taxValue=retailPrice-baseTax**, se suma todo y en la factura se pone los totales.
```typescript
class GiftTicket {identity:Integer; creationDate:date; baseTax:BigDecimal; taxValue:BigDecimal; user: User; ticket: Ticket;}
```
- [ ] Implementar la creación de facturas a partir de un ticket, en el proceso de creación del ticket.
- [ ] En el menú de administración, **invoices**, se enlaza a la gestión de facturas
- [ ] Permitir la búsqueda de facturas por móvil o por ticket.
- [ ] Permitir la creación de facturas a partir de un ticket, se debe asegurar que no tiene factura previa creada.
- [ ] Permitir la reimpresión de facturas existentes.
- [ ] Se puede modificar una factura, pero sólo los datos del usuario.
- [ ] En el servicio de facturas, se podrá crear una factura negativa a partir de una devolución. Se debe sincronizar con la práctica de `Ticket`.

## `story: Messengers`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Crear notas internas entre vendedores.
```typescript
class Message{fromUser:User; toUser:User; subject:String; text:String;}
```
- [ ] Cuando se realiza el login, si existe mensaje pendiente, se muestra con un dialogo emergente.
- [ ] En el menú de administración, Se puede crear un mensaje nuevo.
- [ ] Se puede consultar el historial de mensajes enviados o recibidos.

## `story: News`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestión de noticias en la pantalla principal
- [ ] En el menú segundario, `adviser` si se elige `New` aparecen los productos nuevos, se presenta en tipo carrusel. Este se ejecuta de forma automática al cargar la página. Se considera nuevo si su fecha de creación esta entre los X días anteriores.
- [ ] En el menú segundario, `adviser` si se elige `Popular` aparecen los productos más populares, se presenta en tipo carrusel. Los más populares son aquellos con mejores votaciones, pero esto se debe calcular en la historia `Reviews`, en esta historia, si no esta realizado el servicio, simplemente se realiza un método mock de devuelve una lista fija de artículos.
- [ ] En el menú segundario, `Top 5` aparecen los productos mas vendidos, en la última semana. Se deben mirar los tickets para calcular dicho valor.

## `story: Offers`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Una oferta es un conjunto de artículos donde se aplica un descuento (%) igual para todos los artículos. Se identifican por `reference`, que debe ser de tipo UUID.

```typescript
class Offer {reference:String; description:String; creationDate:LocalDate; expiryDate:LocalDate; discount:Integer; articles: Article;}
```
- [ ] En el menu de administración, **offers**, enlazar con el CRUD ofertas.
- [ ] En la pantalla del carrito de la compra, si se escribe la referencia de la oferta, revisa el carrito de la compra y se lo aplica a los artículos que la tienen.
- [ ] Se permite imprimir con código QR de la URL, con la referencia de la oferta, descripción, fecha caducidad.
- [ ] Se permite conocer los detalles completos a través de la URL, en entorno `dev`, http://localhost:4200/home/offers/WNX5uTC5SIeC60M6noyhWg. Esta URL debe ser pública.

## `story: Online Orders`
> **Autor: Wang Zhengrong**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar la compra realizada directamente por nuestros clientes en la Web.
```typescript
class OnlineOrder {reference:String; state:OnlineOrderState; deliveryDate:LocalDate; ticket:Ticket;}
enum OnlineOrderState{PREPARING, SENT, DELIVERED}
```
- [ ] Realizar la cesta de la compra. Al final se utiliza el recurso Ticket para crear primero un ticket, con todos sus productos a no entregados, y luego se crea el pedido. El pago es contra rembolso.
- [ ] Un cliente, si está logeado, en el perfil, puede ver sus pedidos y el estado en que se encuentran.
- [ ] En el menú de administración, se puede hacer evolucionar un pedido online. El estado de los productos del ticket, tienen que ser coherentes con el estado del pedido.

![](https://github.com/miw-upm/betca-tpv/blob/main/docs/online-order.png)

## `story: Provider Invoices`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar las facturas de los proveedores.

```typescript
class ProviderInvoice{identity:Integer; creationDate:LocalDate; baseTax:BigDecimal; taxValue:BigDecimal; provider:Provider; order:Order}
```
- [ ] En el menú de administración, **Provider Invoice**, realizar el CRUD.
- [ ] Dado un trimestre del año, devuelve el total de baseTax & taxValue.

## `story: Provider Orders`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestión de pedidos. Se organizarán por proveedor, es decir, un pedido solo puede tener productos de un proveedor. Deberá tener una lista de artículos con una cantidad pedida. Un pedido sin cerrar se podrá eliminar. Se permite modificar la cantidad pedida, antes de cerrar el pedido. Se podrá cerrar un pedido, poniendo la cantidad que realmente llego a tienda. Un vez cerrado no se puede modificar ni eliminar.
```typescript
class Order{reference:String, description:String, provider:String, openingDate:LocalDate, closingDate:LocalDate, orderLines:OrdenLine[]}
class OrderLine{article:Article, requiredAmount:Integer, finalAmount:Integer}
```
- [ ] Realizar el CRUD con las limitaciones expuestas.
- [ ] Permitir crear un pedido a partir de algún pedido anterior.
- [ ] Cuando se crea un pedido, en el back-end, se llamara al servicio de ticket-tracking, para actualizar el estado de los artículos pendientes de entregar a REQUIRE_PROVIDER en los tickets. Sincronizarse con la práctica de Ticket-tracking.
- [ ] Cuando se cierra un pedido, en el back-end, se llamara al servicio de ticket-tracking, para actualizar el estado de los artículos pendientes de entregar a IN_STOCK en los tickets. Sincronizarse con la práctica de Ticket-tracking.

![](https://github.com/miw-upm/betca-tpv/blob/main/docs/order.png)

## `story: Refunds`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestión de devoluciones de pedidos on-line

## `story: Salespeople`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Asociar los tickets a los vendedores.
```typescript
class Salesperson{salesperson:User; ticket:Ticket}
```
- [ ] En el proceso de creación de tickets, **check-out**, asociar al ticket el vendedor. Debe aparecer en la impresión del ticket el nombre del vendedor, dentro del campo **note** del ticket.
- [ ] En el menú de administración, **Salespeople**, se pueden realizar buscas varias.
- [ ] Dado un vendedor y un rango de fechas, ver sus ventas por días, especificando: tickets, artículos y valor final.
- [ ] Dado un mes o el mes en curso, ver las ventas de cada vendedor en el mes indicado, en orden descendiente por valor final vendido o cantidad de artículos vendidos.

## `story: Slack Webhook`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Conectar con Slack para la publicación de mensajes.
- [ ] En el menú de administración, **Publish on Slack**, saca un formulario para rellenar y publicar en Slack, en el canal #betca-tpv. Debería tener nivel del mensaje (info, warning, critical), varios campos... El mensaje debiera tener aspecto gráfico del TPV, UPM con iconos o imágenes.
- [ ] Cuando se cierra la caja, se publica automáticamente un resumen en Slack del cierre de caja.
- [ ] Cuando se ejecutan los test, se utilizan mooks, y no se envía a Slack.

Para mas información: https://api.slack.com/messaging/webhooks. Habrá que realizar la publicación con formato (https://api.slack.com/reference/surfaces/formatting) y diseño (https://api.slack.com/messaging/composing/layouts).

Para la autenticación, Slack funciona mediante api-key en la url de la petición, se debe mantener oculta mediante variable de entorno: ${SLACK_URI}. La URL se debe solicitar al profesor y tenerla siempre oculta. Si se utiliza ejecución en el perfil `dev` y si no existe la variable de entorno, debe lanzar una excepción indicando el problema.

Mostramos abajo un ejemplo sencillo, metiendo en el cuerpo el mensaje.
`POST https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX`
```json
{
    "text": "Hello, world."
}
```

## `story: Staff`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar vendedores (operator & Manager). Gestiona la ficha de entrada y salida por día. Tiene que ser automático con el login-logout, pero se debe tener en cuenta que puede haber varios login-logout al día, pero sólo se almacena el primer login y el último logout.
```typescript
class Staff{ user:User; login:LocalDate; logout:LocalDateate;}
```
- [ ] Dado un empleado y un rango de días, listar las horas trabajadas de cada día.
- [ ] Dado un empleado y un rango de meses, listar las horas trabajadas de cada mes.
- [ ] Dar un informe mensual de las horas trabajadas por día entre todos los empleados, se puede elegir un mes cualquiera.

## `story: Stock Alarms`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Establecer valores mínimos (con nivel WARNING y CRITICAL) de un conjunto de artículos. Los warning-critical específicos predominan respecto a los genéricos.
```typescript
class StockAlarm{name:String; description:String; warning:Integer; critical:Integer; stockAlarmLines:StockAlarmLine[];}
class StockAlarmLine{Article:Article; warning:number; critical:number;}
```
- [ ] Realizar el CRUD. Al trabajar con alarmas, siempre se debe mostrar el stock actual de cada artículo
- [ ] Realizar una consulta de artículos que se encuentran en **WARNING** o **CRITICAL**

## `story: Stock Audit`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Auditar el stock existente, en un momento dado. Cuando se abre una auditoría, se crea con la lista de todos los artículos. Poco a poco, se va mirando artículo a artículo el stock existente y si coincide con el teórico. Cuando se cierra deben quedar los artículos no auditados y la lista de artículo con su cantidad, que han tenido perdidas, y con el valor monetario de la perdida total. Una vez cerrado ya no se puede alterar.
```typescript
class StockAudit {creationDate:LocalDate; closeDate:LocalDate; articlesWithouAudit:Article[]; lossValue:number; losses:ArticleLoss[];}
class ArticleLoss {barcode:string; amount:number;}
```
- [ ] En la administración, **Stock Audit**, realizar la gestión de la auditoría.
- [ ] Realizar el CRUD, pero update solo antes de cerrar la auditoria.

## `story: Stock Manager`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Ayudar a gestionar el stock.  Permite realizar búsquedas variadas.
- [ ] Productos por debajo de un stock. El stock puede ser negativo, indicando que existen reservas del mismo.
- [ ] Productos vendidos en un determinado rango.
- [ ] Ayuda a predecir el stock de futuro. Dado un producto, te indica que stock va haber a lo largo del tiempo.
- [ ] Dado un producto, te dice cuando llegará a stock 0

## `story: Tags`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Agrupar artículos. Una etiqueta, se referencia por un nombre.
```typescript
class Tag {name:String; group:String; description:String, articles:Article[];}
```
- [ ] En el menú de administración, permitir la creación, lectura, modificación y borrado de etiquetas (CRUD).
- [ ] Dar funcionalidad al menú `Adviser` de la página `Home` listando un conjunto de artículos asociados a la etiqueta. Permitir añadir a la cesta de la compra el artículo (**ShoppingBasketService**).

![](https://github.com/miw-upm/betca-tpv/blob/main/docs/tag.png)


## `story: Technical Support`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Asistencia técnica vía chat
- [ ] El cliente inicia un chat realizando una consulta técnica sobre un producto. El Empleado ve los chats abiertos y puede contestar a las consultas realizadas.

## `story: Tickets`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Facilitar la lectura y modificación de tickets, permitiendo sólo la reducción de la cantidad y el estado. Si se tiene que devolver dinero se llamara a: **SharedVoucherService::printVoucher** para la impresión de uno. Cuando un producto pase a estado de commited, se debe cobrar el dinero que falta.
- [ ] En el menú de administración, al pulsar **Tickets**, cambia la vista para su gestión.
- [ ] Se realizará una búsqueda por `id` de ticket o `reference` o `mobile`, pero utilizando la función like y un sola caja de entrada.
- [ ] Se puede realizar modificaciones de ticket solo con la caja abierta.

## `story: Ticket Tracking`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Facilitar el seguimiento de artículos por falta de stock de los clientes. Cuando se cree un ticket con una compra no entregada, se habilitará la referencia del ticket para que el cliente pueda acceder al ticket vía Internet para comprobar su estado. El usuario podrá escanear la referencia del ticket mediante un código QR, la cual referencia una URL en la que podrá seguir el estado de los artículos que no se le entregaron por falta de stock.
- [ ] Permitir el acceso mediante la URL: http://localhost:4200/home/ticket-traking/xxxxxxxxxxxxxx, siendo xxxx una referencia generada automáticamente al crear el ticket, no hace falta logearse para ver su contenido.
- [ ] Incluir un servicio, por el cual, a partir de una lista de `barcode - amount`, devolver los teléfonos & nombres de los tickets involucrados, por orden de antigüedad del ticket.
- [ ] Incluir un servicio en el back-end, por el cual, a partir de una lista de `barcode - amount`, modifica el estado de los artículos del ticket a **REQUIRE_PROVIDER**,  por orden de antigüedad del ticket.
- [ ] Incluir un servicio en el back-end, por el cual, a partir de una lista de `barcode - amount`, modifica el estado de los artículos del ticket a **IN_STOCK**,  por orden de antigüedad del ticket. En este caso, enviar un email al cliente. Para los test se debe emplear un **mock**. Cuidado de no exponer la cuenta y clave personal de Gmail!

## `story: Users`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**


Gestionar la cuenta de los clientes, con auto registro y recuperación de contraseña.
- [ ] Crear un recurso independiente "/customers", facilita toda la gestión de permisos, aunque se pueden reutilizar el resto de capa si asi se prefiere.
- [ ] En el dialogo de login, surge la posibilidad de darse de alta como nuevo usuario, mostrando un dialogo independiente.
- [ ] En el dialogo de login, surge la posibilidad de recuperar la contraseña.


- [ ] Permitir que los usuarios cambien sus datos personales a través de su perfil`, tanto en **home** como en **shop**, pero el rol, la fecha de creación y la desactivación de la cuenta son inalterables.
- [ ] Terminar el desarrollo para la creación rápida (móvil-nombre) o/y (datos para factura), en el dialogo del proceso de realizar el `check out`, permitiendo asociar el ticket a un usuario. Cuando se busca a un usuario, si no se encuentra, debe sacar dialogo de creación rápida, donde el _firstName _& _mobile _son obligatorios, el resto _familyName_, _dni_, _address _son opcionales.
- [ ] Permitir la creación y actualización de usuarios, incluido el rol, cumpliendo una lógica de autorizaciones. Un `admin` puede todo. Un `manager` puede modificar `manager`, `operator` y `customer`. Un `operator` no puede alterar roles pero si activación de `customer`.

## `story: VAT Management`
> **Autor: Xuran Liu**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar el Tax trimestral: A partir de un trimestre introducido por el usuario, el sistema devolverá el calculo del Tax para ese trimestre asociado a cada uno de los tipos de Tax. El año se divide en cuatro trimestres. Dado un trimestre se debe calcular el baseTax y valueTax, de todos los artículos sumados, de todos los tickets creados en el trimestre de análisis, agrupados según los tres tipos de Tax:  SUPER_REDUCED("4"), REDUCED("10"), GENERAL("21").
- [ ] Se solicita un trimestre de un año, y devuelve: año, trimestre, baseTax(4):?, valueTax(4):?, baseTax(10):?, valueTax(10):?, baseTax(21):?, valueTax(21):?, totalBaseTax y totalValueTax.

## `story: Vouchers`
> **Autor: ???**   
> **GitHub: [@???](https://github.com/???)**   
> **User on commit: `???`**

Gestionar los vales. En la tienda no se devuelve dinero, se dan vales. Su referencia debe ser tipo UUID
```typescript
class Voucher{reference:String; value:BigDecimal; creationDate:LocalDate; dateOfUse:LocalDate; user:User}
```
- [ ] Realizar la creación y lectura. No se debe permitir el borrado ni cambiar su contenido.
- [ ] Permitir la impresión de vales.
- [ ] Permitir el consumo de un vale. Se debe asegurar previamente que el vale no ha sido ya consumido.
- [ ] Implementar **SharedVoucherService::printVoucher** en Angular. A partir de una cantidad, crea e imprime un vale.
- [ ] Realizar una consulta de vales generados entre dos fechas, pendientes de ser consumidos.

