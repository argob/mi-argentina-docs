---
layout: docs
title: Integración con Mi Argentina
---

Antes de que puedas integrar _Mi Argentina_ en tu sistema, tenés que solicitar las credenciales OAuth 2.0 (_ID de cliente_ y _clave secreta_) para autenticar usuarios y obtener acceso a nuestras APIs.

Para solicitar las credenciales tenes que seguir estos pasos:

<!-- 1. [Solicitar las credenciales.](platforms.md#1-solicitar-las-credenciales)
2. [Generar URI de redirección.](platforms.md#generar-uri-de-redireccion)
3. [Integrar Inicio de sesión Mi Argentina.](platforms.md#integrar-inicio-de-sesión-mi-argentina) -->

<!-- --- -->

1. **Generar URI de redirección**

    La URI de redirección determina dónde Mi Argentina envía las respuestas a tu petición de autorización. Éstas dan la seguridad que siempre los Token de Acceso volverán a tu sitio y no a otro.

    Con esta URI de redirección podrás solicitar las credenciales correspondientes.


2. **Solicitar las credenciales**

    La solicitud de credenciales (`ID de cliente` y `clave secreta`) se hace a través de GDE o por escrito siguiendo [este formato](https://docs.google.com/document/d/16-gB7qdzQXKlpDHoBQY0GNsK0DhAsn7NICV3zj3LUhI).


3. **Integrar Inicio de sesión Mi Argentina**

    Existen muchas bibliotecas para [distintas plataformas](plataformas.html) (web y móvil) para poder integrar _Mi Argentina_. 
