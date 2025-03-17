# Manipulación de Lógica de shallow copy en JavaScript

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
    - [Concepto de recursividad](#concepto-de-recursividad)
    - [Diferencias entre recursión e iteración](#diferencias-entre-recursión-e-iteración)
2. [Patrones Comunes en Recursión](#patrones-comunes-en-recursión)
    - [Recursión simple vs. recursión múltiple](#recursión-simple-vs-recursión-múltiple)
    - [Recursión de cola (Tail Recursion)](#recursión-de-cola-tail-recursion)
    - [Recursión mutua (Recursión indirecta)](#recursión-mutua-recursión-indirecta)
3. [Optimización de Funciones Recursivas](#optimización-de-funciones-recursivas)
    - [Memoización y almacenamiento en caché](#memoización-y-almacenamiento-en-caché)
    - [Conversión de recursión a iteración (Recursion Unrolling)](#conversión-de-recursión-a-iteración-recursion-unrolling)
    - [Optimización con recursión de cola](#optimización-con-recursión-de-cola)

---

## Introducción

La recursividad es un concepto fundamental en la programación que nos permitirá llamar a una función a sí misma para resolver un problema. Esto nos será muy útil cuando tengamos que resolver problemas que se pueden descomponer en subproblemas más pequeños de la misma naturaleza.

### Concepto de recursividad

La recursividad ocurre cuando llamamos a una función dentro de sí misma dentro de su propia definición, para que nuestra función recursiva no se ejecute indefinidamente, debe cumplir con dos condiciones fundamentales:
**caso base** es la condición de salida que detiene una función cuando se ha alcanzado una solución.
**caso recursivo** Es la parte en la que la función se llama a sí misma con un subconjunto del problema original.

veamos un ejemplo:

```javascript
function factoria(n) {
    if (n == 0) {
        // caso base
        return 1;
    }
    return n * factorial(n - 1); // caso recursivo
}
factorial(5); // salida 120
```

En el ejemplo vemos como factorial se descompone en subproblemas de la misma naturaleza 5 \* factorial(4) , 4 factorial(3), y así hasta llegar a factorial(0) que retorna 1 y permite que finalice la acumulación de resultados en el call stack.

### Diferencias entre recursión e iteración

La recursividad y la interacción son técnicas que podemos utilizar para resolver problemas repetitivos, pero funcionan de manera diferente.

| Característica  | Recursión                                                                   | Iteración                                           |
| --------------- | --------------------------------------------------------------------------- | --------------------------------------------------- |
| **Definición**  | Una función que se llama a sí misma.                                        | Un ciclo que repite instrucciones.                  |
| **Caso base**   | Requiere un caso base para detenerse.                                       | Se detiene cuando una condición de bucle se cumple. |
| **Eficiencia**  | Puede generar sobrecarga de memoria por acumulación en la pila de llamadas. | Más eficiente en términos de uso de memoria.        |
| **Legibilidad** | Más intuitiva para problemas recursivos naturales como árboles y grafos.    | Más sencilla para problemas lineales.               |
| **Ejemplo**     | `factorial(n) = n * factorial(n-1)`                                         | `for (let i = 1; i <= n; i++) { result *= i; }`     |

veamos un ejemplo de factorial con iteración:

```javascript
function factorialConIteracion(n) {
    let resultado = 1;
    for (let i = 1; i <= n; i++) {
        resultado *= i;
    }
    return resultado;
}

console.log(factorialConIteracion); // salida 120
```

Vemos con este caso de iteración que no utilizamos la pila de llamadas siendo esto más eficiente en términos de memoria.

## Patrones Comunes en Recursión:

Nuestros algoritmos recursivos pueden estructurarse de diferentes maneras según la naturaleza del problema.

### Recursión simple vs. recursión múltiple

**Recursión simple**
En este tipo de recursión, nuestra función se llama a sí misma una sola vez en cada ejecución. es el patrón más común y podemos usarlo para problemas como el cálculo factorial o la suma de elementos de un array.

```javascript
function sumarArray(array, indice = null) {
    if (indice === null) {
        indice = Number(array.length) - 1;
    }
    // caso base
    if (indice === 0) {
        return array[indice];
    }

    return array[indice] + sumarArray(array, indice - 1); // descomposicion de problema en subproblemas
}

lista = [1, 2, 3, 4, 5];

console.log(sumarArray(lista));
```

**Recursión múltiple**
Aquí, una función recursiva se llama a sí misma más de una vez en cada ejecución, generando un crecimiento exponencial en llamadas. Se usa en estructuras como árboles y la serie de Fibonacci.

```javascript
function contarRamas(n) {
    if (n === 0) return 1; // caso base

    return contarRamas(n - 1) + contarRamas(n - 1); // cada nodo genera dos ramas
}

console.log(contarRamas(3)); // salida 8
```

Este ejemplo tiene una complejidad de O(2ⁿ), ya que cada llamada nos genera dos nuevas llamadas, para problemas grandes, es recomendable usar memoizacion o programación dinámica para optimizar el rendimiento.

### Recursión de cola (Tail Recursion)

En la recursión de cola, la última operación de nuestra función es la llamada recursiva, permitiendo que algunos compiladores optimicen la ejecución y reduzcan el uso de la pila de llamadas.

**Recursión Normal (No Optimizada)**
En la recursión normal, la llamada recursiva no es la última operación que se realiza, es decir, después de que nuestra función hace una llamada recursiva, debe realizar una operación adicional (como una suma, multiplicación, etc.) antes de devolver el resultado final.

En la recursión normal, la llamada recursiva no es la última operación que se realiza. Es decir, después de que la función hace una llamada recursiva, debe realizar una operación adicional (como una suma, multiplicación, etc.) antes de devolver el resultado final.

```javascript
function suma(n) {
    if (n === 0) return 0;

    return n + suma(n - 1); // llamada recursiva no optimizada.
}

console.log(suma(5)); // salida 15
```

En cada llamada recursiva, `n + suma(n - 1)` se evalúa después de que la función realiza la llamada recursiva. En cada nivel de la recursión, nuestra función tiene que esperar el resultado de la llamada recursiva y luego hacer una operación sobre ese valor (sumar n).

suma(5) llama a suma(4)
suma(4) llama a suma(3)
suma(3) llama a suma(2)
suma(2) llama a suma(1)
suma(1) llama a suma(0) (llega al caso base)

Una vez que llegamos al caso base, en cada nivel de la recursión comienza a sumar su valor respectivo donde la llamada a suma(n) se mantiene en la pila de llamadas hasta que la recursión se completa. La pila se acumula, lo que puede causar desbordamiento de pila si nuestro valor n es muy grande.

**Recursión de Cola (Tail Recursion)**
en la recursión de cola, nuestra llamada recursiva es la última operación que realiza la función antes de devolver el resultado. Esto nos permite que el compilador o el motor de JavaScript optimicen la ejecución para evitar que las llamadas recursivas acumulen espacio en la pila de llamadas, lo que se conoce como optimización de recursión de cola.

```javascript
function sumaTail(n, acumulador = 0) {
    if (n === 0) return acumulador;

    return sumaTail(n - 1, acumulador + n); // Última operación es la llamada recursiva
}

console.log(sumaTail(5)); // 15
`
```

En este caso, acumulador + n se pasa directamente como un argumento a nuestra llamada recursiva, la cual es la última operación en la función, no se necesita realizar ninguna operación extra después de nuestra llamada recursiva dentro de la función, ya que función simplemente pasa el valor acumulado hacia abajo en la recursión.

sumaTail(5, 0) pasa a sumaTail(4, 5)
sumaTail(4, 5) pasa a sumaTail(3, 9)
sumaTail(3, 9) pasa a sumaTail(2, 12)
sumaTail(2, 12) pasa a sumaTail(1, 14)
sumaTail(1, 14) pasa a sumaTail(0, 15) (llega al caso base)

Una vez que llega al caso base (n===0), la función devuelve directamente el valor del acumulador. Debido a que la última operación es nuestra llamada recursiva y no hay ninguna operación pendiente después de ella, algunos motores de JavaScript (como el mortor V8 en google Chrome) pueden optimizar la recursión de la cola para que no consuma espacio adicional en la pila. En su lugar, pueden reutilizar el marco de la pila actual para la siguiente llamada, lo que mejora la eficiencia.

### Recursión mutua (Recursión indirecta)

Este tipo de recursión es cuando dos o más de nuestras funciones se llaman entre sí en lugar de llamarse a sí mismas directamente. Es útil para modelar problemas con relaciones alternantes.

Ejemplo de recursión mutua:

```javascript
function esPar(n) {
    if (n === 0) return true;
    return esImpar(n - 1);
}

function esImpar(n) {
    if (n === 0) return false;
    return esPar(n - 1);
}

console.log(esPar(4)); // true
console.log(esImpar(7)); // true
```

## Optimización de Funciones Recursivas

Nuestras funciones recursivas a veces pueden ser ineficientes, especialmente cuando involucran cálculos redundantes o generan una gran cantidad de llamadas, por suerte, existen varias estrategias para optimizar nuestras funciones recursivas y mejorar su rendimiento.

### Memoización y almacenamiento en caché

La memoización es una técnica de optimización que almacena los resultados nuestras funciones en una "cache" para evitar recalcular los mismos valores varias veces. es estrategia es especialmente útil en problemas donde nuestra función recursiva repite cálculos para los mismos parámetros de entrada.

```javascript
let cache = {}; // Caché para guardar los resultados

function factorialMemo(n) {
    if (n === 0 || n === 1) return 1; // Caso base: 0! y 1! son 1
    if (cache[n]) {
        console.log(`Usando cache para ${n}! (${cache[n]})`);
        return cache[n]; // Si ya está calculado, lo usamos
    }

    console.log(`Calculando factorial de ${n}`);
    cache[n] = n * factorialMemo(n - 1); // Guardamos el resultado
    return cache[n];
}

console.log("resultado", factorialMemo(5));
console.log("resultado", factorialMemo(6));
```

Cuando ejecutamos el primer `factorialMemo(5)` se calcula recursivamente de 5 a 1 y se guarda en cache cada asociación índice y resultado, cuando ejecutamos `factorialMemo(6)` solo calculamos `6 * 5` , porque el factorial de 5 ya lo tenemos en la cache, ahorrándonos así de volver a realizar gran parte de los cálculos repetidos.

### Conversión de recursión a iteración (Recursion Unrolling)

la recursión unrolling es un enfoque donde consiste en que reemplacemos nuestra función recursiva por una versión iterativa. Esto nos permitirá mejorar el rendimiento y evitar el desbordamiento de pila (stack overflow) en varias situaciones, especialmente cuando la profundidad de nuestras llamadas sea alta.

funcion recursiva :

```javascript
function factorial(n) {
    if (n === 0) return 1;
    return n * factorial(n - 1);
}
```

version iterativa( sin recursion):

```javascript
function factorialIterativo(n) {
    let resultado = 1;
    for (let i = 1; i <= n; i++) {
        resultado *= i;
    }
    return resultado;
}
```

Aquí evitamos el stack overflow y evitamos utilizar la memoria de la misma manera que lo haría nuestra función recursiva.

### Optimización con recursión de cola

La recursión de cola es un tipo especial de recursión donde la llamada recursiva es la última operación que realiza nuestra función antes de devolver un valor. Esto nos permite que el compilador o el intérprete optimice la recursión, eliminando la necesidad de mantener el contexto de la función anterior en la pila de llamadas.
**version recursiva normal:**

```javascript
function factorial(n) {
    if (n === 0) return 1;
    return n * factorial(n - 1);
}
```

**version recursiva de cola:**

```javascript
function factorial(n, acumulador = 1) {
    if (n === 0) return acumulador;
    return factorial(n - 1, n * acumulador);
}

console.log(factorial(5));
```

En este ejemplo, la recursión de cola permite que el compilador o el entorno de ejecución reutilice el mismo marco de pila para cada llamada a nuestra función recursiva.
