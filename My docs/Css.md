## Propiedades
**display**  
inline-block  
agrega margin, padding, widths, etc etc pero no ocupa todo el ancho de la pantalla como si lo hace display block

```
a {
    background: #fff;
}
```

### position
La propiedad position de CSS especifica cómo un elemento es posicionado en el documento. Las propiedades top, right, bottom, y left determinan la ubicación final de los elementos posicionados.

#### Valores
##### static
El elemento es posicionado de acuerdo al flujo normal del documento. Las propiedades top, right, bottom, left, and z-index no tienen efecto. Este es el valor por defecto.

##### relative
El elemento es posicionado de acuerdo al flujo normal del documento, y luego es desplazado con relación a sí mismo, con base en los valores de top, right, bottom, and left. El desplazamiento no afecta la posición de ningún otro elemento; por lo que, el espacio que se le da al elemento en el esquema de la página es el mismo como si la posición fuera static. Este valor crea un nuevo contexto de apilamiento, donde el valor de z-index no es auto. El efecto que tiene relative sobre los elementos table-*-group, table-row, table-column, table-cell, y table-caption no está definido.

##### absolute
El elemento es removido del flujo normal del documento, sin crearse espacio alguno para el elemento en el esquema de la página. Es posicionado relativo a su ancestro posicionado más cercano, si lo hay; de lo contrario, se ubica relativo al bloque contenedor inicial. Su posición final está determinada por los valores de top, right, bottom, y left.

Este valor crea un nuevo contexto de apilamiento cuando el valor de z-index no es auto. Elementos absolutamente posicionados pueden tener margen, y no colapsan con ningún otro margen.

##### fixed
El elemento es removido del flujo normal del documento, sin crearse espacio alguno para el elemento en el esquema de la página. Es posicionado con relación al bloque contenedor inicial establecido por el viewport, excepto cuando uno de sus ancestros tiene una propiedad transform, perspective, o filter establecida en algo que no sea none, en cuyo caso ese ancestro se comporta como el bloque contenedor. (Notar que hay inconsistencias del navegador con perspective y filter contribuyendo a la formación del bloque contenedor.) Su posición final es determinada por los valores de top, right, bottom, y left.

Estos valores siempre crean un nuevo contexto de apilamiento. En documentos impresos, el elemento se coloca en la misma posición en cada página.

##### sticky
El elemento es posicionado de acuerdo al flujo normal del documento, y luego es desplazado con relación a su ancestro que se desplace más cercano y su bloque contenedor (ancestro en nivel de bloque más cercano) incluyendo elementos relacionados a tablas, basados en los valores de top, right, bottom, y left. El desplazamiento no afecta la posición de ningún otro elmento.

Estos valores siempre crean un nuevo contexto de apilamiento. Nótese que un elemento sticky se "adhiere" a su ancestro más cercano que tiene un "mecanismo de desplazamiento" (creado cuando el overflow es hidden, scroll, auto, o bien overlay), aún si ese ancestro no es el ancestro con desplazamiento más cercano. Esto inhibe efectivamente el comportamiento "sticky".

## Checar
- como se comportan varios elementos con position absolute, se posicionan uno arriba del otro? crean algun flujo solo de positions absolutos que estos repenten???