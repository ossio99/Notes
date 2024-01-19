### Tipos de referencia
En C#, los tipos de referencia son un tipo de datos que almacena una referencia a un objeto en memoria en lugar de los datos reales. Estos tipos de datos almacenan la dirección de memoria donde se encuentra el objeto, en lugar de almacenar los datos directamente. Como resultado, cuando se trabaja con tipos de referencia, se manipula la referencia al objeto, no el objeto en sí.

En C#, los tipos de referencia se definen mediante el uso de clases, interfaces, delegados y arreglos. Algunos ejemplos de tipos de referencia en C# incluyen:

1. Clases: Son estructuras de datos que definen propiedades y métodos que representan objetos. Cuando se crea una instancia de una clase, se crea en la memoria y se obtiene una referencia a ella.

    ```csharp
    class MiClase
    {
        // Propiedades y métodos
    }

    MiClase objetoReferenciado = new MiClase(); // Creación de una instancia de MiClase
    ```

2. Interfaces: Son contratos que especifican un conjunto de miembros que deben ser implementados por las clases que las heredan. Las interfaces también son tipos de referencia.

    ```csharp
    interface IMiInterface
    {
        void MetodoInterface();
    }

    class MiClase : IMiInterface
    {
        public void MetodoInterface()
        {
            // Implementación del método de la interfaz
        }
    }

    IMiInterface referenciaInterface = new MiClase(); // Referencia a través de la interfaz
    ```

3. Delegados: Son tipos que representan referencias a métodos con una lista de parámetros y un tipo de retorno específico. Los delegados permiten la creación de invocaciones indirectas de métodos.

    ```csharp
    delegate void MiDelegado(string mensaje);

    void MetodoDelegado(string mensaje)
    {
        Console.WriteLine(mensaje);
    }

    MiDelegado referenciaDelegado = MetodoDelegado; // Asignación del método al delegado
    ```

4. Arreglos: Los arreglos en C# también son tipos de referencia, ya que contienen una referencia a una secuencia de elementos del mismo tipo.

    ```csharp
    int[] arregloReferenciado = new int[] { 1, 2, 3, 4 };
    ```

En contraste, los tipos de valor, como int, float, char, etc., almacenan directamente los datos dentro de la variable, y su manipulación se realiza directamente en el valor almacenado. Los tipos de valor se definen usando `struct` en C#.

## Sintaxis

### Sintaxis de una clase que hereda de otra
```csharp
public class nombre: clasePadre
{}
```

### Clases
En C#, las clases son elementos fundamentales de la programación orientada a objetos (POO). Permiten definir estructuras que encapsulan datos y comportamientos relacionados en un solo bloque, lo que facilita la organización y reutilización del código. Para crear una clase en C#, sigue estos pasos:

1. Declaración de la clase: Para declarar una clase, se utiliza la palabra clave `class`, seguida del nombre de la clase y las llaves para delimitar el cuerpo de la clase.

2. Atributos (campos): Los atributos son variables que representan los datos que la clase puede almacenar. Se declaran dentro de la clase, generalmente al principio, y se pueden establecer diferentes niveles de acceso (público, privado, protegido) para controlar su visibilidad desde fuera de la clase.

3. Métodos: Los métodos son funciones que definen el comportamiento de la clase. También se declaran dentro de la clase y pueden tener diferentes niveles de acceso. Los métodos pueden utilizar los atributos de la clase para realizar operaciones y manipular los datos.

4. Constructores: Los constructores son métodos especiales que se utilizan para inicializar objetos de la clase. Un constructor tiene el mismo nombre que la clase y no devuelve ningún valor. Se invoca automáticamente cuando se crea un nuevo objeto.

5. Propiedades: Las propiedades proporcionan una forma de acceder y modificar los atributos de la clase. Se definen mediante bloques `get` y `set`, que permiten obtener y establecer los valores de los atributos, respectivamente.

Aquí tienes un ejemplo sencillo de una clase en C#:

```csharp
using System;

class Persona
{
    // Atributos
    public string Nombre;
    public int Edad;

    // Constructor
    public Persona(string nombre, int edad)
    {
        Nombre = nombre;
        Edad = edad;
    }

    // Método
    public void Saludar()
    {
        Console.WriteLine($"Hola, soy {Nombre} y tengo {Edad} años.");
    }
}

class Program
{
    static void Main()
    {
        // Crear un objeto de la clase Persona
        Persona persona1 = new Persona("Juan", 30);

        // Acceder a los atributos y llamar a un método
        Console.WriteLine(persona1.Nombre); // Salida: Juan
        Console.WriteLine(persona1.Edad);   // Salida: 30
        persona1.Saludar();                 // Salida: Hola, soy Juan y tengo 30 años.
    }
}
```

En este ejemplo, creamos una clase `Persona` con atributos `Nombre` y `Edad`, un constructor para inicializar esos atributos y un método `Saludar` para mostrar un mensaje en la consola. Luego, en el método `Main`, creamos un objeto de la clase `Persona` y accedemos a sus atributos y métodos.

### Metodos
En C#, los métodos son bloques de código que contienen instrucciones y permiten realizar tareas específicas. Los métodos son fundamentales para estructurar el código en funciones reutilizables y para dividir la lógica del programa en unidades más manejables. Un método puede recibir argumentos, realizar cálculos, acceder a variables locales y devolver un valor o realizar una acción.

La sintaxis básica para declarar un método en C# es la siguiente:

```csharp
[modificadorAcceso] [tipoRetorno] NombreMetodo([parametros])
{
    // Cuerpo del método: Instrucciones a ejecutar
    // Puede incluir declaración de variables locales, operaciones, etc.
    return [valorRetorno]; // Opcional, si el método devuelve un valor
}
```

Donde:
- `modificadorAcceso`: Especifica la visibilidad del método y puede ser `public`, `private`, `protected`, etc. Indica desde dónde se puede acceder al método.
- `tipoRetorno`: Es el tipo de dato que devuelve el método. Puede ser cualquier tipo de datos válido en C# o `void` si el método no devuelve nada.
- `NombreMetodo`: Es el nombre que se le da al método, y debe seguir las reglas de nomenclatura de C#.
- `parametros`: Son los datos que se pasan al método para que pueda trabajar con ellos. Los parámetros son opcionales y se especifican entre paréntesis, separados por comas.
- `return [valorRetorno]`: Es opcional y se utiliza para devolver un valor del método. El tipo de valor de retorno debe coincidir con el tipo especificado en `tipoRetorno`. Si el método no devuelve nada, se utiliza `return;` o simplemente se omite.

Aquí tienes un ejemplo de un método simple en C#:

```csharp
private List<Proyecto> ObtenerProyectos()
{
    return new List<Proyecto>()
    {
        new Proyecto
        {
            Titulo = "Amazon",
            Descripcion = "E-Commerce realizado en ASP.NET Core",
        },
        // Puedes agregar más objetos Proyecto aquí, si lo deseas
    };
}
```

1. `private List<Proyecto> ObtenerProyectos()`: Esta línea define un método privado llamado `ObtenerProyectos` que devuelve una lista de objetos de tipo `Proyecto`. El modificador de acceso `private` indica que este método solo es accesible desde dentro de la clase en la que está definido.

2. `return new List<Proyecto>()`: Aquí se crea una nueva instancia de la clase `List<Proyecto>`, que es una lista genérica que almacenará objetos del tipo `Proyecto`. La lista se inicializa con una sintaxis de inicialización de colección que permite agregar elementos directamente en el momento de su creación.

3. `new Proyecto { Titulo = "Amazon", Descripcion = "E-Commerce realizado en ASP.NET Core" }`: Esta parte crea un objeto de tipo `Proyecto` y lo inicializa utilizando una sintaxis de inicialización de objeto. El objeto tiene dos propiedades: `Titulo` y `Descripcion`, y se le asignan valores directamente en la declaración.

4. La sintaxis `new List<Proyecto> { ... }` junto con `new Proyecto { ... }` permite crear una lista con un solo elemento, que es el objeto `Proyecto` que se ha inicializado con el título "Amazon" y la descripción "E-Commerce realizado en ASP.NET Core".

En resumen, el método `ObtenerProyectos()` devuelve una lista de proyectos con un único elemento que tiene el título "Amazon" y la descripción "E-Commerce realizado en ASP.NET Core". Si se deseara agregar más objetos `Proyecto` a la lista, simplemente se agregarían separados por comas dentro del bloque de inicialización de la lista, como se muestra en el comentario dentro del código.

### Interfaces
En C#, una interfaz es una estructura que define un conjunto de métodos y propiedades que una clase puede implementar. Una interfaz no proporciona una implementación concreta de estos métodos y propiedades; en cambio, solo especifica qué métodos y propiedades deben estar presentes en cualquier clase que implemente la interfaz.

Las interfaces en C# son útiles para definir contratos y establecer una comunicación clara entre diferentes partes de un programa. Cuando una clase implementa una interfaz, está acordando seguir el contrato definido por esa interfaz, lo que significa que debe proporcionar una implementación para todos los miembros declarados en la interfaz.

Las interfaces se declaran utilizando la palabra clave `interface` seguida del nombre de la interfaz y su contenido entre llaves. Un ejemplo simple de una interfaz en C# es el siguiente:

```csharp
public interface IAnimal
{
    void EmitSound();
    string Species { get; set; }
}
```

En este ejemplo, hemos definido una interfaz llamada `IAnimal`. Esta interfaz tiene dos miembros: un método llamado `EmitSound()` y una propiedad llamada `Species`. Cualquier clase que quiera implementar esta interfaz deberá proporcionar una implementación para el método `EmitSound()` y la propiedad `Species`.

Una clase puede implementar múltiples interfaces, lo que permite que una clase tenga diferentes comportamientos según los contratos definidos por las interfaces que implementa. Para implementar una interfaz en una clase, se utiliza la palabra clave `class`, seguida del nombre de la clase, seguido de dos puntos y el nombre de la interfaz:

```csharp
public class Dog : IAnimal
{
    public void EmitSound()
    {
        Console.WriteLine("Woof woof!");
    }

    public string Species { get; set; }
}
```

En este caso, la clase `Dog` implementa la interfaz `IAnimal`, por lo que debe proporcionar una implementación para el método `EmitSound()` y la propiedad `Species`.

#### IEnumerable
`IEnumerable` es una interfaz en C# (C Sharp) que se encuentra en el espacio de nombres `System.Collections` y proporciona una forma de iterar a través de una colección de elementos. Es una de las interfaces más fundamentales para trabajar con colecciones en C#.

La interfaz `IEnumerable` define un solo método llamado `GetEnumerator()`, que devuelve un objeto `IEnumerator`. El `IEnumerator` se utiliza para recorrer la colección uno por uno y obtener cada elemento.

Aquí hay un ejemplo básico de cómo se podría usar `IEnumerable` en C#:

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Crear una colección de números enteros
        List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };

        // Utilizar la interfaz IEnumerable para recorrer la colección
        IEnumerable<int> coleccion = numeros;

        // Obtener un objeto IEnumerator para la colección
        IEnumerator<int> enumerador = coleccion.GetEnumerator();

        // Iterar a través de la colección usando el enumerador
        while (enumerador.MoveNext())
        {
            int numero = enumerador.Current;
            Console.WriteLine(numero);
        }
    }
}
```

En este ejemplo, primero creamos una lista de números enteros y luego la asignamos a una variable de tipo `IEnumerable<int>`. Luego, obtenemos un objeto `IEnumerator<int>` para esa colección y lo usamos para recorrer y mostrar los elementos uno por uno.

Cabe destacar que, a partir de C# 2.0, se introdujo el concepto de "inferencia de tipos" (`var`), lo que permite omitir explícitamente la declaración de la variable `IEnumerable<int>` y en su lugar utilizar simplemente `var`, haciendo que el código sea más conciso:

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };
        var coleccion = numeros;

        IEnumerator<int> enumerador = coleccion.GetEnumerator();
        while (enumerador.MoveNext())
        {
            int numero = enumerador.Current;
            Console.WriteLine(numero);
        }
    }
}
```

El uso de `IEnumerable` es común en C# cuando se trabaja con colecciones para facilitar la iteración y procesamiento de sus elementos de forma secuencial.

### Listas
En C#, una lista es una estructura de datos que te permite almacenar y manipular una colección de elementos del mismo tipo. La lista es una implementación de la interfaz genérica `List<T>` en el espacio de nombres `System.Collections.Generic`.

#### Crear una lista:

Para crear una lista, primero debes importar el espacio de nombres `System.Collections.Generic` y luego puedes declarar una lista del tipo que desees almacenar. Por ejemplo, si deseas una lista de enteros, puedes hacer lo siguiente:

```csharp
using System.Collections.Generic;

// Crear una lista de enteros
List<int> listaEnteros = new List<int>();
```

#### Agregar elementos a la lista:

Puedes agregar elementos a la lista utilizando el método `Add()`:

```csharp
// Agregar elementos a la lista
listaEnteros.Add(10);
listaEnteros.Add(20);
listaEnteros.Add(30);
```

#### Acceder a elementos de la lista:

Puedes acceder a los elementos de la lista utilizando el índice entre corchetes:

```csharp
int primerElemento = listaEnteros[0]; // Acceder al primer elemento (índice 0)
int segundoElemento = listaEnteros[1]; // Acceder al segundo elemento (índice 1)
// ...
```

#### Obtener el tamaño de la lista:

Puedes obtener el número de elementos en la lista utilizando la propiedad `Count`:

```csharp
int cantidadElementos = listaEnteros.Count;
```

#### Recorrer la lista:

Puedes recorrer todos los elementos de la lista utilizando un bucle `foreach`:

```csharp
foreach (int elemento in listaEnteros)
{
    Console.WriteLine(elemento);
}
```

#### Eliminar elementos de la lista:

Puedes eliminar elementos de la lista utilizando el método `Remove()`:

```csharp
listaEnteros.Remove(20); // Eliminar el elemento con valor 20
```

#### Verificar si un elemento existe en la lista:

Puedes verificar si un elemento existe en la lista utilizando el método `Contains()`:

```csharp
bool existeElemento = listaEnteros.Contains(30); // Devuelve true si el elemento 30 existe en la lista
```

Estos son solo algunos ejemplos de cómo trabajar con listas en C#. Las listas son muy útiles para almacenar y manipular colecciones de elementos de manera dinámica. Recuerda que puedes utilizar listas con cualquier tipo de dato, no solo con enteros.


## Notas
las propiedades de una clase deben tener un valor o ser declaradas como nullable antes de salir del constructor

los tipos de referencia no van a ser nulos a menos que se marquen como nullable con el operador ?, example:
```csharp
public class Persona
{
    public string? Nombre { get; set; }
}
```
otra forma de tener valores nulos sin el signo ? es yendo al archivo que se habre al hacer doble clic en el proyecto y setear como disable el <Nullable>