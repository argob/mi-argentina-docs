---
layout: docs
title: Seguridad del inicio de sesión
---

Las funciones del inicio de sesión con Mi Argentina, como los [tokens de acceso](access-token.md) y los [permisos](permissions.md), hacen que tanto personas como aplicaciones puedan usarlo de forma segura, aunque en el caso de las aplicaciones se deben implementar algunos pasos de seguridad.

- Lista de comprobación de seguridad
- Clave secreta de la aplicación

---

## Lista de comprobación de seguridad

En la siguiente lista se mencionan los requisitos mínimos que deben implementar todas las aplicaciones que usan el inicio de sesión con Mi Argentina. Probablemente, tu aplicación tendrá otras funciones propias, por lo que siempre debes pensar en cómo lograr que tu aplicación sea lo más segura posible.

- Nunca incluyas la clave secreta de la aplicación en código de cliente o código que se pueda descompilar.
- Firma todas las llamadas a la API Graph de servidor a servidor con la clave secreta de la aplicación.
- En los clientes, utiliza tokens de corta duración exclusivos.
- No presupongas que tu aplicación generó los tokens de acceso que utiliza.
- Cuando uses el cuadro de diálogo de inicio de sesión utiliza el parámetro de estado.
- Utiliza nuestros SDK oficiales siempre que sea posible.
- Reduce las áreas expuestas a ataques de tu aplicación bloqueando la configuración de aplicaciones de Mi Argentina.

---

### Clave secreta de la aplicación

La clave secreta de la aplicación se utiliza en algunos procesos de inicio de sesión para generar tokens de acceso. El objetivo es asegurar que solo personas de confianza usen la aplicación. La clave secreta de la aplicación permite crear fácilmente un token de acceso de aplicación que realice las llamadas a la API en nombre de cualquier usuario, por lo que resulta extremadamente importante que nunca se vea comprometida.

En vista de lo anterior, no debes incluir la clave secreta de la aplicación ni el token de acceso de aplicación en ningún código al que pueda acceder alguien que no sea un desarrollador de la aplicación. Esto incluye todos los métodos de código no protegidos, como el código de cliente (por ejemplo, HTML o JavaScript) o las aplicaciones nativas (como las aplicaciones para iOS o Android, o las aplicaciones para computadoras de Windows) que se puedan descompilar.

Para ofrecer la mejor seguridad posible, recomendamos utilizar los tokens de acceso de aplicación únicamente desde los servidores de la aplicación. En el caso de las aplicaciones nativas, recomendamos que la aplicación se comunique con tu propio servidor y que sea este quien realice las solicitudes de la API a Mi Argentina, mediante el token de acceso de aplicación.

Si la clave secreta de la aplicación se ve comprometida, debes restablecerla de inmediato.