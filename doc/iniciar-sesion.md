---
layout: docs
title: Autenticación
---

Si la persona no inició sesión en **Mi Argentina**, se le pedirá que lo haga antes de pasar al inicio de sesión en la aplicación, si no está registrado podrá hacerlo y para luego continuar con el flujo.

Esto se detecta automáticamente, de modo que no tienes que hacer nada para activar este comportamiento.


### Invocar la pantalla de inicio de sesión y configurar la URL de redireccionamiento

La aplicación debe iniciar el redireccionamiento a una URL que mostrará el inicio de sesión:

```
https://id.argentina.gob.ar/authorize/
    ?client_id=651462
    &redirect_uri=https://clienteopenid.com
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

- `scope`: REQUERIDO. Las solicitudes de OpenID Connect DEBEN contener el scope `openid` como valor. [Ver scopes disponibles](https://argob.github.io/mi-argentina-docs/doc/permisos.html).


### Intercambiar código por un token de acceso

Como este proceso de redireccionamiento envía al navegador a direcciones URL de tu aplicación desde la pantalla de inicio de sesión, alguien podría acceder directamente a estas URL mediante fragmentos o parámetros falsos. Por tanto, la aplicación debe confirmar que la persona que usa la aplicación es la misma persona de la que tienes datos de respuesta antes de generar un token de acceso.

Luego del primer paso, se recibe un parámetro `code` que hay que intercambiarlo por un token de acceso mediante un extremo. La llamada debe ser de servidor a servidor, ya que involucra la clave secreta de la aplicación (la clave secreta de la aplicación no debe aparecer nunca en el código del cliente).

```
https://id.argentina.gob.ar/?code=b9cedb346ee04f15ab1d3ac13da92002&state=123123
```

Usamos el parámetro `code` para obtener el `access_token` y el `refresh_token`:

```
curl -X POST \
    -H "Cache-Control: no-cache" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    "https://id.argentina.gob.ar/token/" \
    -d "client_id=651462" \
    -d "client_secret=37b1c4ff826f8d78bd45e25bad75a2c0" \
    -d "code=b9cedb346ee04f15ab1d3ac13da92002" \
    -d "redirect_uri=https://clienteopenid.com/" \
    -d "grant_type=authorization_code"
```

Esta URL tiene los siguientes parámetros obligatorios:

- `client_id`: REQUERIDO. Se vuelve a enviar el CLIENT_ID
- `client_secret`: REQUERIDO. La clave secreta exclusiva de tu aplicación. Es extremadamente importante que permanezca en secreto, es el núcleo de la seguridad de la aplicación y de todas las personas que la usan
- `redirect_uri`: REQUERIDO. Se vuelve a enviar la REDIRECT_URI
- `code`: REQUERIDO. El parámetro recibido del redireccionamiento desde la pantalla de inicio de sesión


Una respuesta válida a esta petición contiene los siguientes campos en un objeto JSON:

```
{
    "access_token": "82b35f3d810f4cf49dd7a52d4b22a594",
    "token_type": "bearer",
    "expires_in": 3600,
    "refresh_token": "0bac2d80d75d46658b0b31d3778039bb",
    "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6..."
}
```

| Campo | Descripción |
| - | - |
| `access_token` | Token para acceder a las APIs. |
| `token_type` | Identifica el tipo de token que se entrega. Debe ser igual a `Bearer`. |
| `expires_in` | El tiempo de expiración del token. |
| `refresh_token` | Hash que se utiliza para obtener otro access_token cuando se vence. |
| `id_token` | JWT firmado que contiene información acerca de la identidad del usuario. |
{: class="table"}


### Solicitar la información del usuario con UserInfo:

```
curl -X POST \
    -H "Authorization: Bearer 82b35f3d810f4cf49dd7a52d4b22a594"
    "https://id.argentina.gob.ar/userinfo/"
```

### Expiración y Refresh Tokens

Si se recibe el código de error `401 Unauthorized` en el uso del access token, es probable que el access token haya expirado.

El cliente OpenID (RP) puede pedir un nuevo access token usando el refresh token. Se tiene que enviar una petición **POST** al endpoint `/token` con los siguientes parámetros:

The RP application can request a new access token by using the refresh token. Send a POST request to the /token endpoint with the following request parameters:

```
curl -X POST \
    -H "Cache-Control: no-cache" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    "https://id.argentina.gob.ar/token/" \
    -d "client_id=651462" \
    -d "client_secret=37b1c4ff826f8d78bd45e25bad75a2c0" \
    -d "grant_type=refresh_token" \
    -d "refresh_token=0bac2d80d75d46658b0b31d3778039bb"
```
