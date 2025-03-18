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

3. [Transformaciones Funcionales con Funciones de Orden Superior](#transformaciones-funcionales-con-funciones-de-orden-superior)

    - [Uso de `map`, `filter` y `reduce`](#uso-de-map-filter-y-reduce)
    - [Creación de transformaciones personalizadas](#creación-de-transformaciones-personalizadas)

4. [Estrategias Avanzadas de Orden Superior](#estrategias-avanzadas-de-orden-superior)

    - [Currificación y aplicación parcial](#currificación-y-aplicación-parcial)
    - [Clausuras y su relación con funciones de orden superior](#clausuras-y-su-relación-con-funciones-de-orden-superior)
    - [Programación basada en composición y encadenamiento](#programación-basada-en-composición-y-encadenamiento)

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

const enfatizar = componer(agregarExclamacion, agregarMayuscula);
console.log(enfatizar("hola mundo")); //salida HOLA MUNDO!
```

## Transformaciones Funcionales con Funciones de Orden Superior

### Uso de `map`, `filter` y `reduce`

Las funciones `map`, `filter`, y `reduce` son métodos claves en la manipulación de arrays que operan de forma funcional, transformando y reduciendo nuestros datos sin la necesidad de modificar el estado global ni utilizar estructuras de control imperativas como bucles. Estas funciones se basan en el concepto de aplicar una operación a cada elemento de nuestra colección de manera declarativa.

`map`: aplica una función a cada elemento de nuestro array y nos devuelve un nuevo array con los resultados.

```javascript
const numeros = [1, 2, 3, 4, 5, 6];
const doblados = numeros.map((num) => num * 2);

console.log(doblados); // salida [2, 4, 6, 8, 10, 12]
```

`filter`: filtra los elementos de nuestro array según un criterio, devolviéndonos un nuevo array con los elementos que cumplen la condición.

```javascript
const numeros = [1, 2, 3, 4, 5, 6];
const mayoresQueCuatro = numeros.filter((num) => num > 4);
console.log(mayoresQueCuatro); // salida [5, 6]
```

`reduce`:reduce todos los elementos de nuestro array a un único valor, utilizando una función acumuladora que recibe el valor acumulado y el elemento actual.

```javascript
const numeros = [1, 2, 3, 4];
const suma = numeros.reduce((acumulado, valor) => acumulado + valor, 0);
console.log(suma); // salida 10
```

Cada uno de estos métodos sigue el principio de "inmutabilidad", donde el estado original no se modifica, y el resultado se obtiene mediane una transformación declarativa.

### Creación de transformaciones personalizadas

A menudo vamos a requerir transformaciones especificas o complejas. Podemos crear funciones personalizadas basadas en métodos como `map`, `filter`, `reduce` sin perder claridad ni la reutilización del código.

```javascript
function transformarDatos(datos, transformacion) {
    return datos.map(transformacion);
}

const nombres = ["mauro", "juan", "ana"];
const primeraMayuscula = (nombre) =>
    nombre.charAt(0).toUpperCase() + nombre.slice(1);

console.log(transformarDatos(nombres, primeraMayuscula)); // salida ['Mauro', 'Juan', 'Ana']
```

## Estrategias Avanzadas de Orden Superior

### Currificación y aplicación parcial

La currificacion transforma nuestra función que toma múltiples argumentos en una secuencia de funciones que reciben los argumentos en relación al orden de cómo fueron declarados los parámetros cada una y recibidos los argumentos al momento de la ejecución, esto permite una reutilización más flexible de funciones y facilita su composición

```javascript
let sumar = (a) => (b) => (c) => a + b + c;

console.log(sumar(10)(5)(3));
```

Por otro lado, la aplicación parcial a nuestras funciones curriying es similar, pero en lugar de transformar una función completamente, permite fijar algunos de sus parámetros y devolver una nueva función. Con esto podemos fijar valores y generar funciones especializadas sin necesidad de repetir lógica.

```javascript
let sumar = (a) => (b) => (c) => a + b + c;

sumaCon10ComoBase = sumar(10); // nos retornara una funcion que equivale a (b) => (c) => 10 + b + c

console.log(sumaCon10ComoBase(5)(3)); // salida 18

sumarCon10y5ComoBase = sumaCon10ComoBase(5); //nos retornara una funcion que equivale a (c) => 10 + 5 + c

console.log(sumaCon10y5ComoBase(3)); // salida 18
```

podemos lograr lo mismo utilizando el metodo `.bind`

```javascript
function multiplicar(a, b) {
    return a * b;
}

multiplicarPor5 = multiplicar.bind(null, 5);
multiplicarPor10 = multiplicar.bind(null, 10);

console.log(multiplicarPor5(3)); // salida 15
console.log(multiplicarPor10(8)); // salida 80
```

La aplicación parcial nos será útil cuando una de nuestras funciones la usamos frecuentemente con algunos argumentos fijos.

### Clausuras y su Relación con Funciones de Orden Superior

una clausura es una de nuestras funciones que "recuerda" el ámbito en el que fue creada, incluso cuando se ejecuta fuera de ese ámbito. Nos serán fundamentales para nuestras funciones de orden superior, ya que nos permiten encapsular valores y comportamientos sin necesidad de variables globales.

```javascript
function contador() {
    let conteo = 0;
    return () => ++conteo;
}

const incrementar = contador();

console.log(incrementar());
console.log(incrementar());
```

Aquí, contador nos devuelve una función que mantiene acceso a la variable count, aunque la función principal ya haya terminado su ejecución. Esto es útil para manejar estados sin exponer variables al ámbito global.

Las clausuras se combinan bien con funciones de orden superior para crear configuraciones dinámicas:

```javascript
function crearSaludo(prefijo) {
    return (nombre) => `${prefijo} ${nombre}`;
}

let saludarA = crearSaludo("Buen dia");
console.log(saludarA("Mauro")); // salida Buen dia Mauro
```

Esto nos permite reutilizar lógica sin reescribir funciones repetitivas.

### Programación Basada en Composición y Encadenamiento

La composición de funciones es una técnica clave en programación funcional que nos permite encadenar varias transformaciones en un flujo declarativo. En lugar de ejecutar funciones secuencialmente de manera imperativa, la composición nos permite construir funciones más complejas combinando otras más simples.

la composición puede ser manual :

```javascript
let agregarMayuscula = (str) => str.toUpperCase();
let agregarExclamacion = (str) => `${str} !`;
let enfatizarPalabra = (str) => agregarExclamacion(agregarMayuscula(str));

console.log(enfatizarPalabra("hola mundo")); //salida HOLA MUNDO!
```

o también puede ser dinámica

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

const enfatizar = componer(agregarExclamacion, agregarMayuscula);
console.log(enfatizar("hola mundo")); //salida HOLA MUNDO!
```
