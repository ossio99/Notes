# csurf

Necesita que ejecútenos el middleware cookie parser antes

```jsx
app.use(cookieParser())

```

También debemos habilitar el middleware csrf. Este middleware añade una funcion `req.csrfToken()` para crear un token el cual debera ser añadido a las peticiones que mutan el estado, dentro de un campo de un formulario oculto, etc. Este token es validado contra la sesion del visitante o csrf cookie

## opcion cookie

determina si el secreto del token? para el usuario deberia ser almacenado en una `cookie` o en una `req.session`. Almacenar el secreto del token? en una cookie implementa el double submit cookie pattern. Por defecto es falso.  
Cuando es establecido como true (o un objeto de opciones para la cookie), entonces el modulo cambia su comportamiento y no usa mas `req.sessions`. Esto significa que no necesitas usar mas un session middleware. En lugar, necesitas usar el cookie-parser middelware en tu aplicacion antes de este middleware.

```jsx
app.use(csrf({cookie: true}))
```

Como se menciono antes, gracias al middleware `csrf()`, tenemos acceso al metodo `req.csrfToken()`. Este método nos genera un `token` que debemos pasar al client por la response y en el formulario usamos esta variable como propiedad

```jsx
res.render(...,{
    csrfToken: req.csrfToken()
})
```

En el front tenemos que usar un input con esta estructura para que reciba y envié el token con el formulario:

```jsx
<input type="hidden" name="_csrf" value="{{csrfToken}}">
```

**Doubts**  
el middleware estara interceptando solo los formularios que se envien que tengan un token o tambien las peticiones ajax??
el csrfToken se manda a traves del body y no de cookies???

yo creo que el flujo es asi:
- se envia el token como una variable desde el res
- en el front se almacena en un cookie y al mismo tiempo se envia en el form dada la estructura necesaria
- el middleware de cookie parser lo leera o mas bien el middleware de csrf


## Referencias
[documentacion](https://www.npmjs.com/package/csurf)
