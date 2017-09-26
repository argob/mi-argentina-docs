---
layout: docs
title: Permisos
---

Los permisos te habilitan para realizar una petición de acceso a la información adicional del usuario.

Cuando se invoca la pantalla de inicio de sesión, se especifican los permisos mediante el parámetro `scope`.

Los mismos se definen separados por `+` o usando espacios. Ejemplo de petición:

```
https://id.argentina.gob.ar/authorize/
    ?client_id={client-id}
    &redirect_uri={redirect-uri}
    &response_type=code
    &scope=openid+profile+email+optional
```

A continuación se listarán los permisos válidos y la información del usuario que se obtiene por cada uno.

### Scope: `profile`

| Campo | Descripción |
| - | - |
| `name` | Nombre y apellido |
| `given_name` | Nombre |
| `family_name` | Apellido |
| `gender` | Género |
| `birthdate` | Fecha de nacimiento |
{: class="table"}


### Scope: `email`

| Campo | Descripción |
| - | - |
| `email` | Correo electrónico |
{: class="table"}


### Scope: `optional`

| Campo | Descripción |
| - | - |
| `dni_type` | Tipo de documento |
| `dni_number` | Número de documento |
| `nationality` | Nacionalidad |
| `country` | País |
| `locality` | Localidad |
| `street_name` | Domicilio |
| `street_number` | Número de domicilio |
| `postal_code` | Código postal |
| `appartment_number` | Número de departamento |
| `appartment_floor` | Piso de departamento |
| `phone_number` | Teléfono móvil |
| `email_verified` | Correo electrónico verificado (`true`/`false`) |
| `level` | Nivel de validación del usuario (`0`, `1`, `2`) |
{: class="table"}
