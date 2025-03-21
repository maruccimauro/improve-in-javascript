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
2. [Fundamentos del Currying](#fundamentos-del-currying)
    - [Diferencia entre currying y funciones normales](#diferencia-entre-currying-y-funciones-normales)
    - [Cómo transformar una función en su versión currificada](#cómo-transformar-una-función-en-su-versión-currificada)
3. [Manipulación Avanzada con Currying](#manipulación-avanzada-con-currying)
    - [Parcialización](#parcialización)
    - [Composición de funciones currificadas](#composición-de-funciones-currificadas)

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

## Fundamentos del Currying

### Diferencia entre currying y funciones normales

Para entender el curriying, es importante compararlo con las funciones tradicionales. en una función normal, todos los argumentos se pasan en una sola llamada y la función devuelve el resultado de forma directa. En cambio, en una función currificada, los argumentos se reciben en diferentes llamadas hasta completas los parámetros necesarios.

```javascript
function multiplicar(a, b, c) {
    return a * b * c;
}

console.log(multiplicar(5, 3, 2)); // salida 30
```

en este caso multiplicar recibe todos los argumentos juntos y resuelve directamente el retorno.

```javascript
function multiplicarCurrificada(a) {
    return (b) => {
        return (c) => {
            return a * b * c;
        };
    };
}

console.log(multiplicarCurrificada(5)(3)(2)); // salida 30
```

En este otro caso `multiplicarCurrificada()` recibe `a` como argumento y retorna una función que espera recibir `b` que a su vez retorna una función que espera recibir `c` y esta retorna `a * b * c`, solo cuando se ha pasado el ultimo argumento la multiplicación es evaluada y retornada.

veamos cuáles son sus diferencias más significativas:
| Característica | Función Normal | Currying |
|---------------------------|------------------------------------|-----------------------------------------------|
| **Recepción de parámetros** | Todos en una sola llamada | En múltiples llamadas anidadas |
| **Reutilización de lógica** | Menos flexible | Se pueden preconfigurar valores intermedios |
| **Composición de funciones** | Más difícil de combinar | Facilita la composición funcional |
| **Expresividad** | Directa y concisa | Puede mejorar la claridad en código funcional |

### Cómo transformar una función en su versión currificada

Para que podamos convertir nuestra función normal en una función currificada, debemos reestructurar su forma de recibir los argumentos.

**Transformacion manual de una funcion**

```javascript
function sumar(a, b, c) {
    return a + b + c;
}

console.log(sumar(1, 2, 3)); // salida  6
```

Para transformarla en su versión currificada, podemos reescribirla de la siguiente manera:

```javascript
function sumarCurrificada(a) {
    return function (b) {
        return function (c) {
            return a + b + c;
        };
    };
}

console.log(sumarCurrificada(1)(2)(3)); // salida 6
```

**Implementación genérica de currying**
En lugar de escribir manualmente nuestras funciones currificadas, podemos crear una función que convierta automáticamente cualquier función en nuestra versión currificada.

```javascript
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        } else {
            return (...nextArgs) => curried(...args, ...nextArgs);
        }
    };
}

function sumar(a, b, c) {
    return a + b + c;
}

const sumarCurriado = curry(sumar);
console.log(sumar.length);
console.log(sumarCurriado(1)(2)(3)); // 6
console.log(sumarCurriado(1, 2)(3)); // 6
console.log(sumarCurriado(1)(2, 3)); // 6

const sumarCurriyingParcial1 = sumarCurriado(100);
const sumarCurriyingParcial2 = sumarCurriyingParcial1(50);
console.log(sumarCurriyingParcial2(10)); // salida 160
```

## Manipulación Avanzada con Currying

### Parcialización

la parcialización se da cuando "congelamos" algunos argumentos de una función , creando una nueva función que necesita menos argumentos, este proceso lo podemos aplicar a cualquier función , no solo a aquellas que están currificadas.

podemos pasar de una función simple de multiplicación

```javascript
function multiplicar(a, b) {
    return a * b;
}
```

a parcializar nuestra función para fijar uno de los argumentos.

```javascript
function parcializar(funcion, argumento) {
    return (b) => {
        return funcion(argumento, b);
    };
}

function multiplicar(a, b) {
    return a * b;
}

multiplicarX5 = parcializar(multiplicar, 5);
console.log(multiplicarX5(10));
```

### Composición de funciones currificadas

El curriying nos facilitara la composición de funciones enormemente. La composición de funciones se refiere a la capacidad de combinar múltiples funciones pequeñas en una sola función que realiza todas las operaciones.
con las funciones currificada, es mucho más sencillo que compongamos funciones, ya que el curriying hace que cada función devuelva otra función, lo que nos facilita la secuenciación de operaciones.
veamos un ejemplo de una composición de función

```javascript
function sumar5(a) {
    return a + 5;
}

function multiplicarX10(b) {
    return b * 10;
}

function componer(funcion1, funcion2) {
    return function (x) {
        return funcion2(funcion1(x));
    };
}

console.log(componer(sumar5, multiplicarX10)(3)); // (3 + 5) * 10 = 80
console.log(componer(multiplicarX10, sumar5)(3)); // 3 * 10 + 5 = 35
```

Aquí la función componer toma dos funciones currificadas y las podemos componer como queramos!
