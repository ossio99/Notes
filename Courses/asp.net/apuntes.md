@modelo x
tipo de dato del modelo

@Modelo
objeto como tal, que se le paso por el controlador (o su padre si es una vista parcial, al parecer)

si declaramos que el tipo de dato del modelo en el parcial es de otro tipo de dato (ejemplo, el tipo de dato en la vista es la clase pero en el parcial el tipo de dato es IEnumerable el cual tiene una lista de objetos tipo Proyeco), entonces desde la etiqueta partial lo definimos con la propiedad model

se hace así porque como el parcial debe ser reutilizable

si quiero utilizar este parcial en otra vista que no sea index, que es la unica que va a recibir el tipo de dato HomeIndexViewModel como modelo

entonces para usar el parcial en otra vista, solo tendríamos que crear otro modelo (clase) que tenga como propiedad un IEnumerable que sea una lista con objetos Proyectos


- Principio de responsabilidad unica  
Nos dice que cada clase debe tener un solo motivo para cambiar

- repositorio es basicamente una clase que se encarga de servir datos, tipicamente una clase repositorio lo que hace es que se conecta a una db para conseguir los datos o realizar cualquier operacion en la db


