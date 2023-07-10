# Lógica implementación csurf en bienes raíces node
- Ejecutamos el middleware en el index de nuestro servidor, ¿así estará escuchando todas las rutas?
- En el controller mandamos el token ejecutando la función x que csurf puso en el request gracias al anterior middleware
- En el front, seguimos la sig. estructura para que envié el formulario el token
- Y vuala, el middleware validara que el token recibido coincida con el que se envió
- galletas???
