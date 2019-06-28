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

| Campo | Descripción | Tipo de dato |
| - | - | - |
| `name` | Nombre y apellido | String |
| `given_name` | Nombre | String |
| `family_name` | Apellido | String |
| `gender` | Género | String (`M` o `F`) |
| `birthdate` | Fecha de nacimiento | Date |
{: class="table"}


### Scope: `email`

| Campo | Descripción | Tipo de dato |
| - | - | - |
| `email` | Correo electrónico | String |
{: class="table"}


### Scope: `optional`

| Campo | Descripción | Tipo de dato |
| - | - | - |
| `dni_type`                 | Tipo de documento                                        | String |
| `dni_number`               | Número de documento                                      | String |
| `nationality`              | Nacionalidad                                             | String |
| `country`                  | País                                                     | String |
| `locality`                 | Localidad                                                | String |
| `street_name`              | Domicilio                                                | String |
| `street_number`            | Número de domicilio                                      | String |
| `postal_code`              | Código postal                                            | String |
| `appartment_number`        | Número de departamento                                   | String |
| `appartment_floor`         | Piso de departamento                                     | String |
| `phone_number`             | Teléfono móvil                                           | String |
| `email_verified`           | Correo electrónico verificado (`true`/`false`)           | Boolean |
| `level`                    | Nivel (`deprecado`)                                      | Integer |
| `vehicles`                 | Vehículos                                                | Array |
| `dependants`               | Personas a cargo                                         | Array |
| `verify_options`           | Tipo de validación                                       | Array |
| `cuil`                     | CUIL                                                     | String |
| `validation_level`         | Nivel de validación obtenido                             | Integer |
| `validation_date`          | Fecha de la validación obtenida                          | DateTime |
| `validation_origin`        | Origen de la validación obtenida                         | String |
| `do_dni_match_cuil`        | Verifica si el DNI coincide con el CUIL (`true`/`false`) | Boolean |
{: class="table"}
