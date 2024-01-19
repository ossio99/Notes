## Funciones de primera clase
Cuando un lenguaje de programación es considerado "de primera clase" significa que los elementos de ese lenguaje, como funciones o tipos de datos, tienen un estatus especial que les otorga ciertos privilegios y características adicionales. En esencia, esto permite que esos elementos sean tratados de manera más flexible y poderosa dentro del lenguaje.

Por ejemplo, en un lenguaje de programación con funciones de primera clase, las funciones pueden ser asignadas a variables, pasadas como argumentos a otras funciones y retornadas como resultados de funciones. Esto facilita la implementación de patrones avanzados y técnicas como programación funcional.

En resumen, un lenguaje de programación es considerado de primera clase cuando sus elementos fundamentales son tratados como ciudadanos de pleno derecho y pueden utilizarse de manera versátil y expresiva dentro del propio lenguaje.

Los lenguajes de programación que no son de primera clase pueden carecer de ciertas características que limitan el tratamiento de ciertos elementos de manera flexible. Algunas de las características que pueden hacer que un lenguaje no sea de primera clase son:

1. Funciones no pueden ser asignadas a variables: En algunos lenguajes, las funciones no pueden ser tratadas como valores que se puedan asignar a variables o pasar como argumentos a otras funciones.

2. Funciones no pueden ser retornadas como resultados de otras funciones: Si un lenguaje no permite retornar funciones como resultados de otras funciones, se dificulta la implementación de ciertos patrones de diseño y técnicas avanzadas.

3. No se pueden crear funciones anónimas o lambda: Las funciones anónimas o lambda son funciones sin un nombre explícito que se utilizan para tareas específicas. Si el lenguaje no permite definir funciones de esta manera, la flexibilidad se ve reducida.

4. Tipos de datos no pueden ser tratados como objetos: En algunos lenguajes, los tipos de datos básicos no pueden ser tratados como objetos con propiedades y métodos, lo que limita las operaciones que se pueden realizar sobre ellos.

5. Restricciones en la manipulación de estructuras de datos: Algunos lenguajes pueden tener limitaciones en la manipulación de estructuras de datos, lo que dificulta la implementación de ciertas operaciones o algoritmos.

Es importante tener en cuenta que el concepto de "lenguaje de primera clase" puede variar según el contexto y la funcionalidad específica que se esté evaluando. Algunos lenguajes pueden carecer de ciertas características mencionadas anteriormente, pero aún así, ofrecer poderosas herramientas para abordar diferentes problemas y tareas de programación.


## Java vs Javascript
El hecho de que en Java todo sea una clase y en JavaScript todo sea un objeto se conoce como el paradigma de programación orientada a objetos (POO) en Java y el paradigma orientado a objetos basado en prototipos en JavaScript.

1. Programación Orientada a Objetos (POO) en Java:
Java sigue el paradigma de programación orientada a objetos tradicional, donde todo se organiza en clases y objetos. El código se organiza en clases que actúan como plantillas para crear objetos con atributos (variables) y métodos (funciones). Los objetos son instancias de estas clases y se pueden crear múltiples instancias a partir de una sola clase. La herencia se utiliza para extender y reutilizar el comportamiento de las clases, y la encapsulación y el polimorfismo son conceptos clave en este enfoque.

2. Programación Orientada a Objetos basada en prototipos en JavaScript:
JavaScript utiliza un paradigma de programación orientada a objetos basado en prototipos. En lugar de clases, los objetos son fundamentales en JavaScript y pueden ser creados directamente o a través de funciones constructoras y clases (introducidas en ECMAScript 6). Cada objeto tiene un prototipo del que hereda propiedades y métodos. La herencia en JavaScript se logra mediante el enlace entre objetos prototipo, lo que permite compartir comportamientos entre diferentes objetos.

Ambos enfoques tienen sus ventajas y características distintivas, y el elegir uno u otro depende de las necesidades del proyecto y las preferencias del desarrollador. La programación orientada a objetos en Java es más estructurada y rígida, mientras que el enfoque basado en prototipos en JavaScript es más flexible y permite una mayor dinamicidad en la creación de objetos.