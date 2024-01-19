### Checar del segundo proyecto
- anotaciones de datos
- atributo display???
- secciones en razor
- model state
- tag helpers, validation-summary y los modos
- harcoding
- atributo remote
- objeto tipo Task
- string interpolation
- consulta SQL en formato verbatim (con el símbolo @ antes de las comillas)
. objetos anonimos en c#
- asp-route-id
- al parecer, cuando un controlador al cual se accede por medio de un link, requiere un parametro se le pasa desde la vista con el parametro asp-route-id y cuando accedemos al controller a traves de el envio de un formulario, mandamos el parametro en un input type hidden, con el parametro asp-for

### drapper
- Execute
permite ejecutar un query que no va a retornar nada
- QueryFirstOrDefaultAsync se vio en el metodo existe(), en evitando 

ef
- modelos compilados

### me quede en
- aplicando asincronismo


### Dudas general
- porque se tiene que crear un constructor del controlador para crear la propiedad, sera porque como es un servicio, de esta forma le decimos que el constructor depende de la interfaz (que en realidad es una instancia de la clase), pero que significa dependencia entonces, que no funciona si no se crea?? no se puede simplemente crear una propiedad que sea del tipo de la interfaz o la clase???
```csharp
public class TiposCuentasController : Controller
{
    private IRepositorioTiposCuentas repositorioTiposCuentas;

    public TiposCuentasController(IRepositorioTiposCuentas repositorioTiposCuentas)
    {
        this.repositorioTiposCuentas = repositorioTiposCuentas;
        }
}
```

- si el controller es una clase, quien la instancia?? ya que hasta tiene un constructor