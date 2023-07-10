# Logica autenticacion del proyecto pacientes de veterinaria
- se declara cargando como true y auth como un objeto vacío y se ejecuta el efecto del auth provider el cual intenta obtener el token del local storage para hacer petición al endpoint perfil pero como no hay token se setea cargando como false y se ejecuta un return, es importante el seteo de cargando ya que si se queda como true cuando se intente loguear no se renderizara el contenido por el condicional del RutaProtegida component
- en la vista de login, al hacer submit se hace una petición al endpoint de login
- este endpoint, si las credenciales son correctas, responde con la data del veterinario traída de la db y le agrega un jwt el cual tendrá una codificación del id del usuario de la db
- el front recibe esta data, almacena el token en local storage y setea el estado global auth con la data del response, este seteo es importante para que no marque error en el componente RutaProtegida, ya que este solo renderizara el contenido si auth tiene algo de lo contrario redireccionara a login
- el front setea el estado global auth con la data del res
   
## Redundancia en controller perfil y autenticar  
parece redundante ya que ambos controllers devuelven lo mismo (un objeto con la data del veterinario) pero autenticar ejecuta ciertas validaciones de login y perfil no, perfil, además, autenticar solo se ejecuta cuando se hace una petición al endpoint de login y el otro cada que se recarga la app y se ejecuta el use effect

## Se crea una sesión nueva en el req.veterinario cada que se hace una peticion a un endpoint privado  
Podría parecer un problema esto pero en realidad no afecta, solo es un poco innecesario (debe haber una mejor forma de hacerlo) pero de momento es la única forma que tengo para implementar validación, de lo contrario tendría que separar las tareas en 2 middlewares, uno que solo autentique y otro que cree esta sesión y de esta forma esta segunda tarea solo la realizaria cuando se hace peticion al endpoint que ejecuta el controller perfil  

## Sesión almacenada en el request innesesaria??
pues si se usa, aunque solo lo usa el controller actualizarPassword y perfil

## Cargando state  
al recargar el componente provider, se vuelve a declarar el estado auth como un estado vacio, so, en el componente ruta protegida redirige a login si auth esta vacio, por lo tanto necesitamos renderizar condicionalmente con el state cargando
