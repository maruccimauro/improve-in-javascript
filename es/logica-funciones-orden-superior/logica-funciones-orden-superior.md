# Manipulacion de logica de orden superior en funciones

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

    - [¿Qué son las funciones de orden superior?](#qué-son-las-funciones-de-orden-superior)
    - [Ventajas de usar funciones de orden superior](#ventajas-de-usar-funciones-de-orden-superior)
    - [Comparación entre programación imperativa y funcional](#comparación-entre-programación-imperativa-y-funcional)

2. [Fundamentos de Funciones de Orden Superior](#fundamentos-de-funciones-de-orden-superior)
    - [Funciones que reciben funciones como argumentos](#funciones-que-reciben-funciones-como-argumentos)
    - [Funciones que retornan funciones](#funciones-que-retornan-funciones)
    - [Composición de funciones](#composición-de-funciones)

---

## Introducción

### ¿Qué son las funciones de orden superior?

Las funciones de orden superior son nuestras funciones que pueden recibir otras funciones como argumentos y/o devolver funciones como resultado. Son un concepto fundamental en la programación funcional y permiten escribir código más modular, reutilizable y expresivo.
En muchos lenguajes como en javscript , nuestras funciones son ciudadanos de primera clase, es decir, que pueden ser asignadas a variables, usadas como parámetros y retornadas desde otras funciones. Esto nos habilita el uso de funciones de orden superior.

```javascript
function operar(a, b, operacion) {
    return operacion(a, b);
}

const suma = (a, b) => a + b;
const resta = (a, b) => a - b;

console.log(operar(5, 3, suma)); // salida 8
console.log(operar(5, 3, resta)); // salida 2
```

En este ejemplo vemos como tanto la función `suma` y la función `resta` son pasadas como argumentos a la función `operar` sobre el parámetro `operacion`.

### Ventajas de usar funciones de orden superior

**Modularidad y reutilización**: nos permiten generar código más reutilizable al encapsular lógica en funciones genéricas.
**Mayor legibilidad y expresividad**: al delegar el comportamiento a funciones externas, el código se vuelve más declarativo y fácil de leer.
**Facilitan la programación funcional:** nos permiten trabajar con funciones como datos lo que es fundamental para el paradigma funcional.
**Reducción de código repetitivo:** nos permiten evitar la duplicación de código al proporcionar estructuras reutilizables para trabajar sobre colecciones de datos.
**Mejor mantenimiento:** separa la lógica en funciones pequeñas y reutilizables, lo que hace que el código sea más fácil de mantener y reutilizar.

**Comparación entre programación imperativa y funcional**
Existen dos enfoques principales para resolver problemas en programación.
**Programacion imperativa:** Se basan en instrucciones paso a paso que modifican el estado del programa, Usa estructuras de control como bucles `for` y `while`.
**Programación funcional:** Se basa en la evaluación de funciones sin modificar el estado global, usa funciones puras y evita efectos secundarios.

ejemplo con enfoque imperativo:

```javascript
const numeros = [1, 2, 3, 4, 5, 6];
let cuadrados = [];

for (let i = 0; i < numeros.length; i++) {
    cuadrados.push(numeros[i] * numeros[i]);
}
console.log(cuadrados); //  [1, 4, 9, 16, 25, 36]
```

ejemplo con enfoque funcional:

```javascript
const numeros = [1, 2, 3, 4, 5, 6];
const cuadrados = numeros.map((n) => n * n);
console.log(cuadrados); //  [1, 4, 9, 16, 25, 36]
```

nuestro ejemplo con enfoque funcional que utiliza el método `map` es más conciso y expresivo, ya que utiliza una función de orden superior en vez de un bucle explicito.

## Fundamentos de Funciones de Orden Superior.

### Funciones que reciben funciones como argumentos

Una de las características clave de las nuestras funciones de orden superior es su capacidad para recibir otras funciones como argumentos. Esto nos permite la abstracción de patrones de código repetitivos y la generalización de comportamientos.

```javascript
function operar(a, b, operacion) {
    return operacion(a, b);
}

const multiplicar = (a, b) => a * b;

console.log(operar(15, 5, multiplicar)); // salida 75
console.log(operar(60, 2, (a, b) => a / b)); // salida 30
```

Aquí, `operar` no necesita conocer los detalles de `multiplicar` o cualquier otra función. Solo se encarga de ejecutar la función que recibe como argumento con su propia lógica.

### Funciones que retornan funciones

Nuestras funciones de orden superior también pueden devolver otras funciones. Esto nos será útil para generar funciones especializadas o configurar comportamiento dinámicamente.

```javascript
function crearMultiplicador(factor) {
    return function (operando) {
        return operando * factor;
    };
}

const duplicar = crearMultiplicador(2);
const quintuplicar = crearMultiplicador(5);

console.log(duplicar(10)); // salida 20
console.log(quintuplicar(10)); // salida 50
```

Aquí, `crearMultiplicador` genera una nueva función que multiplica por un valor determinado, lo que nos permite la creación de funciones reutilizables con parámetros que nosotros predefinamos.

### Composición de funciones

La composición de nuestras funciones es una técnica fundamental en la programación funcional que consiste en combinar múltiples funciones en una sola, de manera en que la salida de una función se convierta en la entrada de la siguiente.

```javascript
let agregarMayuscula = (str) => str.toUpperCase();
let agregarExclamacion = (str) => `${str} !`;
let enfatizarPalabra = (str) => agregarExclamacion(agregarMayuscula(str));

console.log(enfatizarPalabra("hola mundo")); //salida HOLA MUNDO!
```

Para mejorar la legibilidad, podemos crear una función de composición genérica:

```javascript
let agregarMayuscula = (str) => str.toUpperCase();
let agregarExclamacion = (str) => `${str} !`;

const componer = (...funcs) => {
    return (valorInicial) => {
        return funcs.reduceRight((valorAcumulado, funcionActual) => {
            return funcionActual(valorAcumulado);
        }, valorInicial);
    };
};

const enfatizar2 = componer(agregarExclamacion, agregarMayuscula);
console.log(enfatizar2("hola mundo")); //salida HOLA MUNDO!
```
