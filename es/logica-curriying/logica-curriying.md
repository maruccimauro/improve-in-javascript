# Manipulacion de logica currying en funciones Javascript

<img src="/resources/logo.png">
<hr />
<b>¡Antes de comenzar!</b>

¡Antes de querer resolver todas las incógnitas del universo posible (como nos sucede a muchos), ten en cuenta que nuestro cerebro, con cada cosa que aprendemos día a día, necesita tiempo, alimentación y descanso para generar las conexiones neuronales físicas. Este no es un proceso instantáneo, sino progresivo, permitiendo que podamos retener, aprender y relacionar la información en el futuro, tanto cercano como lejano.
Por ello, es fundamental aplicar lo que aprendes en tu día a día, reforzando esas conexiones de manera continua. Más importante que desear una mente capaz de memorizar todo al instante, es comprender que nuestro cerebro no funciona de esa manera. En cambio, es mejor desarrollar una **mente resolutiva, capaz de entender la abstracción del problema y canalizar el camino hacia una solución.**!

Te deseo lo mejor en este camino en el que buscas mejorar tu box de conocimientos.❤️

Con cariño, Mauro.

<hr />

**Índice de la Guía**

1. [Introducción](#introducción)
    - [¿Qué es el currying?](#qué-es-el-currying)
    - [Importancia del currying en la programación funcional](#importancia-del-currying-en-la-programación-funcional)

---

## Introducción

El curriying es una técnica en programación funcional que nos permitirá transformar nuestra función con múltiples parámetros en una serie de funciones anidadas, donde cada una espera recibir una parte de los argumentos antes de retornar una nueva función o el resultado final. La clave del curriying es no necesariamente cada función recibe 1 solo argumento si n o que cada una puede recibir todos los argumentos necesarios para ejecutar su lógica.
veamos un ejemplo!

```javascript
function sumar(a) {
    return (b) => {
        return a + b;
    };
}

console.log(sumar(5)(3)); // salida 8
```

en este caso `sumar(a)` devuelve un función anónima que espera un argumento `b` para al final realizar y retornar la suma.

sin embargo una función currificada podría aceptar más de un argumento en cada llamada disponible, siempre que se respete el orden de los parámetros a recibirse.

```javascript
function sumar(a) {
    return (b, c) => {
        return a + b + c;
    };
}
console.log(sumar(5)(3, 2)); // salida 10
```

en este otro caso `sumar(a)` devuelve una función anónima que espera 2 argumentos `b` y `c` para al final realizar y retornar la suma.

### Importancia del currying en la programación funcional

El currying es una técnica clave en la programación funcional porque nos permite:

**Reutilización de código:** Podemos crear funciones más específicas a partir de nuestra función general.
**Composición de funciones:** Nos permite combinar funciones más fácilmente, lo que nos lleva a un código más modular y declarativo.
**Evitar el uso de argumentos redundantes:** En lugar de repetir valores en múltiples llamadas, podemos fijar ciertos valores y reutilizar la función resultante.
**Mayor claridad y legibilidad:** En muchos casos, el código se vuelve más expresivo y fácil de entender.
**Aplicación parcial:** Podemos usar el currying para generar versiones especializadas de nuestras funciones con parámetros predefinidos.
