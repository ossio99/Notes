### Comilla en la url (virgulilla)
indica el root de nuestra aplicacion  
example:
```html
<link rel="stylesheet" href="~/css/custom.css" asp-append-version="true" />
```
esto es de asp.net, de razor o de c#???


### asp-append-version
propiedad que se conoce como tag helper, los tag helpers nos ayudan a añadir funcionalidad util a nuestras etiquedas html, en el caso especifico de este tag helper lo que hace es que añade un string a la url del css de manera que si el css cambia, el string cambia, lo que provoca que el usuario no tenga una version desactualizada del archivo css, basicamente nos ayuda a no tener problemas con el cache de los navegadores ya que para hacer la carga de las aplicaciones mas eficiente los navegadores por defecto guardan una version de los distintos archivos que componen nuestro sitio web.  
esto es de asp.net, de razor o de c#???

### Razor
Sintaxis para usar c# en archivos cshtml
##### Expresiones c# en archivos cshtml
con el arroba permite pasar de codigo HTML a c#, al leer el @ entendera que lo que viene inmediatamente despues es una expresion de c#, exmaple:
```csharp
    <h1 class="display-4">Soy @Model.Nombre y tengo @Model.Edad años</h1>
```
##### Bloques de codigo
```csharp
@{
    ViewData["Title"] = "Home Page";
}
```

#### Vistas parciales
se debe crear un empty razor view el cual se llamara con la etiqueta partial:
```html
<partial name="_Presentacion" />
```
este parcial solo estara disponible para las vistas de la misma carpeta, para que lo puedan usar vistas de otras carpetas deberia ubicarse en la carpeta shared

### Acciones
```csharp
public IActionResult x()
{
    return Vista();
}
```
a estos metodos les llamamos acciones, estas acciones son las que se ejecutan al hacer una peticion http a una ruta especifica de nuestra aplicacion, un controlador contiene una o mas acciones, las acciones en este ejemplo regresa una vista cuyo nombre es el mismo de la accion a menos que se le pase el nombre de la vista por parametro a `Vista()`

duda: entonces aqui no tienes un controller por cada ruta, sino un solo controller con multiples acciones???

las vistas estaran vinculadas a las acciones del controlador cuyo nombre sea el mismo del nombre de la carpeta donde estan estas vistas

### Layout
el layout se crea en la carpeta views/shared, en este archivo tendremos el layout y el `@renderbody()` donde se renderizara el contenido que use este layout
duda: como decirle a la vista que herede del layout, si no se puede entonces como le hariamos en caso de que no queramos que una vista herede del layout

#### Seteando layout
para configurar un layout debemos ir al archivo _ViewStart.cshtml el cual esta en la carpeta views y donde seteamos el archivo que se usara como layout de la siguiente manera:
```csharp
@{
    Layout = "_Layout";
}
```

### Routing
el routing se configura en la clase program, hay varias maneras de hacer routing en asp.net core, routing por atributo y routing convencional, en este routing convencional tenemos las reglas de routeo centralizadas en un solo lugar  
ejemplo de routeo convencional:
```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```
`name` indica que es la regla de ruteo por defecto  
`pattern` es el patron que define nuestra regla el cual se compone de 3 partes, `controller=home` indica que en caso de no indicarse en la url un controller se usara el home, `action=Index` por defecto ejecutara el action Index y `id?` indica que puede recibir un id opcional (se sabe que es opcional por el ?), este ultimo permite, por ejemplo, obtener un registro en particular

### Traer data del controller a la vista
#### ViewBack
Es un objeto que permite transmitir información desde el controlador hacia la vista
Ejemplo:
```csharp
public IActionResult Index()
{
    ViewBag.nombre = "Eduardo Ossio";
    return View();
}
```
Es del tipo dinamic, eso significa que se puede usar cualquier propiedad  
Para acceder a la propiedad en el html lo haremos de la siguiente manera:
```html
<h1 class="display-4">Soy @ViewBag.nombre</h1>
```
Esta propiedad solo estara disponible en la vista Index

#### Modelos fuertemente tipados
Es mejor ya que no es dinamic  
Primero de debe especificar el tipo de dato del modelo
Example:  
```csharp
@model string
```

Ahora toca pasar el string a la vista desde el controlador
```csharp
public IActionResult Index()
{
    return View("Index", "Agelito");
}
```
Si le pasamos solo un string a la funcion view que es la que permite invocar una vista lo que hacemos el pasarle el nombre de la vista, por lo que debemos pasar el nombre de la vista y posteriormente el string que queremos pasar a la vista

#### Accediendo al modelo en la vista

```csharp
@model string

@{
    ViewData["Title"] = "Home Page";
}

<div class="text-center">
    <h1 class="display-4">Soy @Model</h1>
    <h2>Soy un desarrollador full stack especializado en tecnologías .NET y JavaScript</h2>
    <img
        id="foto"
        src="/imagenes/me.jpg" 
    />
</div>
```

###### @model
especificar el tipo de dato que va a recibir la vista

###### @Model  
sirve para acceder al valor del modelo

### Recibiendo 2 valores en la vista con una clase
Si se quiere pasar 2 datos del controlador a la vista debo crear una clase y luego colocar dicha clase como el tipo de dato del modelo de la vista. Para esto se debe crear una clase en la carpeta Models (es opcional la ubicacion)
```csharp
namespace Portafolio.Models
{
    public class Persona
    {
        public string Nombre { get; set; }
        public int Edad { get; set; }
    }
}
```
posterior en la vista usamos la clase como el tipo de dato del modelo y entonces @Model sera la clase
```csharp
@model Persona

@{
    ViewData["Title"] = "Home Page";
}

<div class="text-center">
    <h1 class="display-4">Soy @Model.Nombre</h1>
</div>
```
ahora podemos recibir muchos datos desde el controlador a la vista y fuertemente tipado, de modo que si intentamos acceder a una propiedad que no existe nos dara error.   
Por ultimo en el controlador tenemos que crear una instancia de la clase y pasarsela al metodo view()
```csharp
public IActionResult Index()
{
    var persona = new Persona()
    {
        Nombre = "Agel chiquitito",
        Edad = 20
    };
    return View(persona);
}
```
al metodo `View()` ya no es necesario pasarle la vista ya que anteriormente si era necesario porque como le pasabamos un string que se pasaria a la vista si no le pasabamos la vista tomaria el string como la vista


### ViewData (asp.net)
En ASP.NET, ViewData es un objeto de tipo ViewDataDictionary que actúa como un diccionario de clave-valor. Es una propiedad del controlador que permite pasar datos desde el controlador a la vista. El ViewDataDictionary es una colección de datos que se utiliza para compartir información específica entre el controlador y la vista.

En el controlador, puedes asignar valores a ViewData utilizando la sintaxis de diccionario, como mencioné anteriormente:

```csharp
public class MiControlador : Controller
{
    public IActionResult MiAccion()
    {
        // Asignar un valor a ViewData
        ViewData["Mensaje"] = "¡Hola desde ViewData!";
        return View();
    }
}
```

Y en la vista, puedes acceder a los valores de ViewData utilizando la misma clave que se utilizó en el controlador:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mi Página</title>
</head>
<body>
    <h1>@ViewData["Mensaje"]</h1>
</body>
</html>
```

El objeto ViewDataDictionary es creado y administrado por el framework ASP.NET, y se pasa automáticamente a la vista durante el proceso de representación. Aunque ViewData es útil para compartir pequeñas cantidades de datos entre el controlador y la vista, también tiene algunas limitaciones. No proporciona comprobaciones de tipos en tiempo de compilación, lo que significa que cualquier error tipográfico en las claves podría llevar a errores en tiempo de ejecución.

Por lo tanto, en versiones más recientes de ASP.NET Core, se recomienda usar "ViewBag" o un modelo fuertemente tipado ("Model") en lugar de ViewData, ya que ofrecen una experiencia más segura y tipos resueltos en tiempo de compilación.

### ViewBag (razor)
En el contexto de ASP.NET, `ViewBag` es una característica específica de Razor, el motor de vistas de ASP.NET. Razor es una sintaxis de marcado utilizada en ASP.NET para crear vistas dinámicas, donde se mezcla código C# (o VB.NET) con HTML para generar contenido de página. 

`ViewBag` es una forma de pasar datos desde el controlador a la vista en ASP.NET MVC y ASP.NET Core MVC, que son dos frameworks de desarrollo web de ASP.NET. Permite que el controlador comparta información con la vista para que esta última pueda acceder a esos datos y mostrarlos en la página.

El uso de `ViewBag` es bastante sencillo. En el controlador, puedes asignar valores a propiedades dinámicas del `ViewBag`, y luego en la vista, puedes acceder a esos valores utilizando la sintaxis de Razor.

Ejemplo de uso en el controlador (C#):

```csharp
public ActionResult MiVista()
{
    ViewBag.NombreUsuario = "Juan";
    ViewBag.EdadUsuario = 30;
    return View();
}
```

Ejemplo de uso en la vista (Razor):

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mi Página</title>
</head>
<body>
    <h1>Bienvenido, @ViewBag.NombreUsuario</h1>
    <p>Tu edad es @ViewBag.EdadUsuario años.</p>
</body>
</html>
```

Cuando se ejecute esta vista, mostrará un saludo personalizado utilizando los datos del `ViewBag`. Es importante tener en cuenta que el `ViewBag` utiliza propiedades dinámicas, lo que significa que no se realiza una comprobación de tipo en tiempo de compilación, por lo que es necesario tener cuidado al usarlo para evitar errores de tiempo de ejecución.

En resumen, `ViewBag` es una funcionalidad específica de Razor, el motor de vistas de ASP.NET, y se utiliza para pasar datos desde el controlador a la vista para su visualización.


### Model (razor)
Cuando se trabaja con Razor, los modelos suelen ser clases o estructuras de datos definidas en el código del controlador. Estos modelos se utilizan para pasar la información necesaria desde el controlador a la vista.

Aquí tienes un ejemplo simple de cómo se puede utilizar un modelo en una vista Razor:

Supongamos que tenemos un modelo llamado `Producto`:

```csharp
public class Producto
{
    public int Id { get; set; }
    public string Nombre { get; set; }
    public decimal Precio { get; set; }
}
```

En el controlador, podemos instanciar y asignar valores a una instancia de `Producto` y luego pasar esa instancia a la vista:

```csharp
public class ProductosController : Controller
{
    public IActionResult Detalles()
    {
        // Supongamos que aquí obtenemos los datos del producto desde algún lugar
        Producto producto = new Producto
        {
            Id = 1,
            Nombre = "Producto de ejemplo",
            Precio = 19.99m
        };

        // Pasamos el modelo a la vista
        return View(producto);
    }
}
```

Luego, en la vista Razor (archivo `.cshtml`), podemos acceder a las propiedades del modelo y mostrar la información:

```html
@model MiProyecto.Models.Producto

<!DOCTYPE html>
<html>
<head>
    <title>Detalles del Producto</title>
</head>
<body>
    <h1>@Model.Nombre</h1>
    <p>Precio: @Model.Precio</p>
</body>
</html>
```

En este ejemplo, `@model MiProyecto.Models.Producto` especifica que la vista espera un modelo de tipo `Producto`. Luego, podemos acceder a las propiedades del modelo (`Nombre` y `Precio`) utilizando `@Model.Nombre` y `@Model.Precio` respectivamente.

En resumen, en Razor, el "modelo" es la estructura de datos que se pasa desde el controlador a la vista y que permite mostrar información dinámica en la página web generada por ASP.NET MVC.

### Notas
**entity framework core**  
- es un orm
- igual dapper un orm para la plataforma .net

**extension .cs**  
los archivos html y css tienen extension que empeiza con cs

- por convencion los elementos compartidos de razor los nombramos con un guion bajo al inicio, aunque sean archivos que solo se vayan a usar en una vista

### Notas de situaciones
**Comportamiento de modelos fuertemente tipados en vistas parciales en ASP.NET**

En ASP.NET, cuando se trabaja con vistas fuertemente tipadas, es posible encontrarse con un problema al intentar acceder a propiedades del modelo en una vista parcial. Si la vista parcial no está configurada adecuadamente para heredar el mismo modelo que la vista principal, el modelo se tratará como dynamic, lo que impide el acceso directo a sus propiedades y métodos.

Para resolver esta situación, es crucial seguir estos pasos:

1. Asegurarse de que la vista principal esté fuertemente tipada y reciba un modelo específico desde el controlador. Esto se logra declarando la directiva de modelo en la parte superior de la vista, como se muestra en el siguiente ejemplo:

   ```csharp
   @model TuNamespace.TuModelo // Reemplaza "TuNamespace.TuModelo" con el nombre correcto del modelo
   ```

2. Al crear la vista parcial, es fundamental heredar el mismo modelo que la vista principal. La vista parcial también debe estar fuertemente tipada con el mismo modelo para evitar que se trate como dynamic. La definición del modelo debe estar presente en la vista parcial, tal como se muestra a continuación:

   ```csharp
   @model TuNamespace.TuModelo // Asegúrate de usar el mismo modelo que en la vista principal
   ```

3. Con estas configuraciones en su lugar, la vista parcial podrá acceder directamente a las propiedades y métodos del modelo fuertemente tipado sin que se genere el error de "dynamic".

Siguiendo estos pasos, se asegurará una correcta herencia de modelos y permitirá un acceso sin problemas a las propiedades y métodos en vistas parciales, lo que mejorará la organización y mantenibilidad del código en proyectos ASP.NET.

### Dudas
que pedo con los controllers aqui, son mas bien como una clase donde se pasan clases, vistas, actions
que pedo con los modelos, son como pues si igual como una clase pero de la que se crea una instancia, no de la que , ok no


### Tipos de validaciones asp.net core mvc

- validando el formulario  
se hace con anotaciones de datos en el modelo
```csharp
[Required(ErrorMessage = "El campo {0} es requerido")]
[StringLength(maximunLength: 50, minimumLength = 3, ErrorMessage = "La longitud del campo {0} debe estar entre {2} y {1}")]
public string Nombre { get; set; }
```
como podemos ver le podemos pasar un mensaje de error  
esto no evita que la accion se ejecute si el modelo es invalido, lo que tenemos que hacer es usar `ModelState` para saber si el modelo es valido o no
```csharp
if (!ModelState.IsValid)
{
    return View(tipoCuenta);
}
```

- visualizando los errores de validacion  
esto lo logramos con un tag helper llamado `asp-validation-summary`, el cual se añade como propiedad a un div donde se mostraran los errores dependiendo el valor de esta (All o ModelOnly)
```csharp
<div asp-validation-summary="All"></div>
```
- tag helpers para los campos
- otras validaciones por defecto
- ???

- validaciones personalizadas por atributo
- validaciones personalizadas por modelo
- validaciones personalizadas a nivel de controlador
- Validaciones personalizadas con javascript utilizando remote


atributos
- asp-for
- asp-validation-for
- asp-action

### Dapper

`FirstOrDefaultAsync` significa, traime lo primero que encuentres o un valor por defecto del tipo de dato que especifique
```csharp
var query = connection.Query("SELECT 1").FirstOrDefault();
// mas bien 👇
var existe = await connection.QueryFirstOrDefaultAsync<int>($"SELECT 1 FROM TiposCuentas WHERE Nombre = @Nombre AND UsuarioId = @UsuarioId;", new { nombre, usuarioId });
//checar bien
```

`QuerySingle` permite hacer un query que va a traer un solo resultado
```csharp
var connection = new SqlConnection(connectionString);
var id = connection.QuerySingle<int>(@"INSERT INTO TiposCuentas (Nombre, UsuarioId, Orden) Values (@Nombre, @UsuarioId, 0); SELECT SCOPE_IDENTITY();", tipoCuenta);
```

`QueryAsync` permite hacer un select y trae un conjunto de resultados y los mapea a un tipo de dato especifico
```csharp
// en este ejemplo mapeara el resultado en un IEnumerable de tipo TipoCuenta
return await connection.QueryAsync<TipoCuenta>("");
```

`Execute` permite ejecutar un query que no va a retornar nada
```csharp
return await connection.ExecuteAsync(@"UPDATE TiposCuentas SET Nombre = @Nombre WHERE Id = @Id", tipoCuenta)
```

## Hacer peticiones desde un formulario
se debe agregar a la etiqueta form la propiedad asp-action y asp-controller
```csharp
<form asp-controller="TiposCuentas" asp-action="Crear">
</form>
```
si ya estamos debajo del controller, no es necesario especificarlo (como cuando tenemos la vista en la carpeta de nombre del controller)

## Recibir data del controller
para recibir data del controller en la vista, se debe definir un modelo para que la vista sepa que tipo de dato es el dato que se le paso y posteriormente accedemos en cada campo