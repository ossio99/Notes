# csurf

Necesita que ejecútenos el middleware cookie parser

```jsx
app.use(cookieParser())

```

También debemos habilitar el middleware csrf

```jsx
app.use(csrf({cookie: true}))
```

Lo anterior nos proporciona de manera global el método csrfToken()

```jsx
req.csrfToken()
```

Este método nos genera un token que debemos pasar al client por la response y en el formulario usamos esta variable como propiedad

```jsx
res.render(...,{
    ...,
    csrfToken: req.csrfToken()
})
```

En el front tenemos que usar un input con esta estructura para que reciba y envié el token con el formulario:

```jsx
name='_csrf' value=csrf
```

**Doubts**  
el middleware estara interceptando solo los formularios que se envien que tengan un token o tambien las peticiones ajax??
el csrfToken se manda a traves del body y no de cookies???
