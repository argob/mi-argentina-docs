---
layout: docs
title: Autenticación
---

Si la persona no inició sesión en **Mi Argentina**, se le pedirá que lo haga antes de pasar al inicio de sesión en la aplicación, si no está registrado podrá hacerlo y para luego continuar con el flujo.

Esto se detecta automáticamente, de modo que no tienes que hacer nada para activar este comportamiento.


### Invocar la pantalla de inicio de sesión y configurar la URL de redireccionamiento

La aplicación debe iniciar el redireccionamiento a una URL que mostrará el cuadro de diálogo de inicio de sesión:

```
https://id.argentina.gob.ar/authorize/
    ?client_id={client-id}
    &redirect_uri={redirect-uri}
    &response_type=code
    &scope=openid+profile+email+optional
```

Esta URL tiene los siguientes parámetros obligatorios:

- `client_id`: REQUERIDO. Es el identificador de la aplicación.
- `redirect_uri`: REQUERIDO. Es la URL a la que quieres redirigir a la persona que inicia sesión. Esta URL captura la respuesta dada en la pantalla de inicio de sesión.
- `response_type`: REQUERIDO. Determina el flujo de procesamiento de autorización que se utilizará, incluidos los parámetros que se devuelven desde los puntos finales utilizados.

| "response_type" value | Flow |
| - | - |
| code | Authorization Code Flow |
| id_token | Implicit Flow |
| id_token token | Implicit Flow |
{: class="table"}

- `scope`: REQUERIDO. Las solicitudes de OpenID Connect DEBEN contener el scope `openid` como valor. [Ver scopes disponibles](https://argob.github.io/mi-argentina/doc/permisos.html).


### Intercambiar código por un token de acceso

Como este proceso de redireccionamiento envía al navegador a direcciones URL de tu aplicación desde la pantalla de inicio de sesión, alguien podría acceder directamente a estas URL mediante fragmentos o parámetros falsos. Por tanto, la aplicación debe confirmar que la persona que usa la aplicación es la misma persona de la que tienes datos de respuesta antes de generar un token de acceso.

Luego del primer paso, se recibe un parámetro `code` que hay que intercambiarlo por un token de acceso mediante un extremo. La llamada debe ser de servidor a servidor, ya que involucra la clave secreta de la aplicación (la clave secreta de la aplicación no debe aparecer nunca en el código del cliente).

```
https://id.argentina.gob.ar/token/
    ?client_id={client-id}
    &client_secret={client-secret}
    &redirect_uri={redirect-uri}
    &code={code}
    &grant_type=authorization_code
```

Esta URL tiene los siguientes parámetros obligatorios:

- `code`: el parámetro recibido del redireccionamiento desde la pantalla de inicio de sesión.
- `client_secret`: la clave secreta exclusiva de tu aplicación. Es extremadamente importante que permanezca en secreto, es el núcleo de la seguridad de la aplicación y de todas las personas que la usan.


Una respuesta válida a esta petición contiene los siguientes campos en un objeto JSON:

| Campo | Descripción |
| - | - |
| `access_token` | Token para acceder a las APIs. |
| `token_type` | Identifica el tipo de token que se entrega. Debe ser igual a `Bearer`. |
| `expires_in` | El tiempo de expiración del token. |
| `refresh_token` | Hash que se utiliza para obtener otro access_token cuando se vence. |
| `id_token` | JWT firmado que contiene información acerca de la identidad del usuario. |
{: class="table"}
