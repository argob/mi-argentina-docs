---
layout: docs
title: Manejo de sesiones
---

# Cierre de sesión iniciado por un RP

Un RP puede notificar al OP que el usuario final ha cerrado sesión en el sitio y que también podría querer cerrar sesión en el OP. En este caso, el RP, después de haber cerrado la sesión del usuario final del RP, redirige al usuario final al endpoint de cierre de sesión del OP.

Parámetros que se pasan como parámetros de consulta en la solicitud de cierre de sesión:

* `id_token_hint`: El token de identificación emitido anteriormente se pasa al endpoint de cierre de sesión como una pista sobre la sesión autenticada actual del usuario final con el cliente.

* `post_logout_redirect_uri`: URL a la que el RP solicita que se redirija el agente de usuario del usuario final después de realizar un cierre de sesión.

* `state`: **OPCIONAL**. Valor opaco utilizado por el RP para mantener el estado entre la solicitud de cierre de sesión y la devolución de llamada al endpoint especificado por el parámetro de consulta `post_logout_redirect_uri`.

Ejemplo:

```
http://localhost:8000/end-session/?id_token_hint=eyJhbGciOiJSUzI1NiIsImtpZCI6ImQwM...&post_logout_redirect_uri=http://rp.example.com/logged-out/&state=c91c03ea6c46a86
```
