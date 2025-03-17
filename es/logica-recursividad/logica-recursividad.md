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
