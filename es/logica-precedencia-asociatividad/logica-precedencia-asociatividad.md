# Manipulación de Lógica de Precedencia y Asociatividad de Operadores en JavaScript

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
    - [¿Qué es la precedencia y asociatividad de operadores?](#qué-es-la-precedencia-y-asociatividad-de-operadores)
    - [Importancia de la precedencia y asociatividad en las expresiones](#importancia-de-la-precedencia-y-asociatividad-en-las-expresiones)
2. [Conceptos Fundamentales](#conceptos-fundamentales)
    - [Definición de precedencia de operadores](#definición-de-precedencia-de-operadores)
    - [Definición de asociatividad de operadores](#definición-de-asociatividad-de-operadores)
    - [Relación entre Precedencia y Asociatividad](#relación-entre-precedencia-y-asociatividad)
3. [Lista de operadores con mayor a menor precedencia](#lista-de-operadores-con-mayor-a-menor-precedencia)
4. [Uso de Paréntesis para Controlar la Evaluación](#uso-de-paréntesis-para-controlar-la-evaluación)
    - [La importancia de los paréntesis en las expresiones complejas](#la-importancia-de-los-paréntesis-en-las-expresiones-complejas)
    - [Cómo los paréntesis modifican la precedencia y asociatividad](#cómo-los-paréntesis-modifican-la-precedencia-y-asociatividad)
5. [Operadores Combinados y su Impacto](#operadores-combinados-y-su-impacto)
    - [Operadores aritméticos combinados (+=, -=, \*=, /=)](#operadores-aritméticos-combinados-+=-=--=-)
    - [Operadores de comparación y su interacción con otros operadores](#operadores-de-comparación-y-su-interacción-con-otros-operadores)
    - [Operadores lógicos combinados (&&, ||)](#operadores-lógicos-combinados--&&-)
6. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Confusión con la precedencia en expresiones complejas](#confusión-con-la-precedencia-en-expresiones-complejas)
    - [Evitar errores en la combinación de operadores](#evitar-errores-en-la-combinación-de-operadores)
    - [Uso de paréntesis para claridad](#uso-de-paréntesis-para-claridad)
7. [Comparación con otros Lenguajes](#comparación-con-otros-lenguajes)
    - [Diferencias de precedencia entre JavaScript y Python](#diferencias-de-precedencia-entre-javascript-y-python)
    - [Impacto de la precedencia en C++ y JavaScript](#impacto-de-la-precedencia-en-c-y-javascript)
8. [Conclusión y Recursos Adicionales](#conclusión-y-recursos-adicionales)
    - [Resumen de conceptos clave](#resumen-de-conceptos-clave)
    - [Ejercicios y desafíos prácticos](#ejercicios-y-desafíos-prácticos)

---

## Introducción

La manipulación de la lógica de precedencia y asociatividad de operadores es fundamental para comprender como el motor de JavaScript evalúa nuestras expresiones y en cual orden se ejecutan nuestras operaciones, siendo está, la clave para evitar errores lógicos y permitirnos escribir código más predecible, eficiente y limpio.

### ¿Qué es la precedencia y asociatividad de operadores?

En JavaScript pueden existir operaciones con muchos operadores y operandos, y el motor debe tomar decisiones tales como, en que orden se deben evaluar estos operandos y operadores, así es como entran en juego dos conceptos claves :

**Precedencia de operadores:** es la regla que rige cuando en una expresión tenemos múltiples operadores, donde los operadores con mayor precedencia se ejecutan antes que los operadores de menor precedencia.

**Asociatividad de operadores:** ¿qué sucede si dos operadores tienen la misma precedencia? ... la asociatividad se encarga de determinar la dirección en la que se evalúan, ya sea de izquierda a derecha (asociatividad izquierda) o de derecha a izquierda(asociatividad derecha)

Partamos de unos para intentar comprender mejor estos dos conceptos sumamente útiles a la hora de desarrollar nuestras aplicaciones.

```javascript
let resultado = 5 + 3 * 2;
console.log(resultado); // 11 ¿por qué no 16?
```

aquí, podemos observar que la multiplicación (_) tiene una mayor precedencia que el operador de suma (+), por lo tanto, la primer expresión a evaluarse será 3 _ 2 , resultando en 6, y luego se le suma 5, obteniendo así 11.

Pero si quisiéramos que la suma se evalúe primero , podríamos solucionarlo con el uso del operador paréntesis de agrupación ().

```javascript
let resultado = (5 + 3) * 2;
console.log(resultado); // 16 ¿por que no 11?
```

Vemos como en este caso los operadores paréntesis de agrupación alteran el orden natural de precedencia del restos de los operadores , ya que el nivel de precedencia que poseen es el más alto posible , con un nivel 19 (ya veremos esto en detalle más adelante).

### Importancia de la precedencia y asociatividad en las expresiones

Comprender el orden en que se ejecutan los operadores y como pueden afectar el resultado final de una expresión por su precedencia y asociatividad es fundamental para

**Evitar errores lógicos:** Si no entendemos bien una precedencia, una operación puede producirnos resultados que no esperamos.

**Mejora la legibilidad del código:** Si desarrollamos un código bien estructurado y con operadores correctamente aplicados nos permitirá facilidad a la hora de mantenerlo.

**Optimizar el rendimiento:** Al usar correctamente la lógica de precedencia y asociatividad podremos evitar que cálculos innecesarios y mejorar la eficiencia.

## Conceptos Fundamentales

Los operadores son parte de la columna vertebral del desarrollo en cualquier lenguaje de programación, ya que permiten realizar operaciones matemáticas, comparaciones lógicas y manipulación de datos. Dicho esto, cuando una expresión contiene múltiples operadores, es necesario establecer reglas que determinen el orden en que se evalúan tanto los operandos como los operadores.
Dos conceptos claves que gobiernan este comportamiento son la precedencia de operadores y la asociatividad de operadores. Estos principios aseguran que nuestras expresiones vayan a ser interpretadas siempre se hagan de manera predecible y correcta.

### Definición de Precedencia de Operadores

Como vimos anteriormente la precedencia de operadores es la jerarquía que define qué operador se evalúa primero cuando hay múltiples operadores en nuestra expresión. Los operadores con mayor precedencia se ejecutan antes que los operadores con menor precedencia

### Definición de Asociatividad de Operadores

La asociatividad de operadores es quien determina el orden de evaluación de una expresión cuando dos operadores tienen la misma jerarquía de precedencia. Existiendo dos tipos principales de asociatividad:
**Asociatividad de izquierda a derecha:** la expresión se evaluara de izquierda a derecha.
**Asociatividad de derecha a izquierda:** la expresión se evaluara de derecha a izquierda.
por ejemplo, en el motor de JavaScript la resta (-) tiene una asociatividad de izquierda a derecha:

```javascript
let resultado = 10 - 5 - 2;
console.log(resultado); // 3
```

aquí ya que 10 - 5 está a la izquierda y el operador resta tiene asociatividad de izquierda a derecha será la primera expresión a resolverse , luego continuará 5 - 2 dando 3 como resultado.

otro ejemplo, pero esta vez con asociatividad de derecha a izquierda podría ser el operador de asignación (=):

```javascript
let b, c, d;
b = c = d = 10;
console.log(b, c, d); // 10 10 10
```

aquí vemos como 10 tiende a asignarse a d por la asociatividad de derecha a izquierda que posee el operador de asignación (=), a posterior, se asignara d a c y finalmente c a b.

### Relación entre Precedencia y Asociatividad

La precedencia y la asociatividad trabajan juntas como un equipo para determinar el orden de evaluación de nuestras expresiones. Mientras que la precedencia toma decisiones como qué operador se ejecuta primero, la asociatividad se dedica a resolver situaciones en las que hay operadores de igual precedencia.

## lista de operadores con mayor a menor precedencia

A continuación podemos ver una lista donde detalla el nivel de precedencia y su asociatividad relativa con el que trabaja el motor de Javascript:

| Precedencia | Tipo de operador                                      | Asociatividad | Operadores individuales |
| ----------- | ----------------------------------------------------- | ------------- | ----------------------- |
| 19          | Agrupamiento                                          | n/a           | `( … )`                 |
| 18          | Acceso a propiedades (notación por punto)             | Izquierda     | `… . …`                 |
| 18          | Acceso a propiedades (notación por corchetes)         | Izquierda     | `… [ … ]`               |
| 18          | `new` (con lista de argumentos)                       | n/a           | `new … ( … )`           |
| 18          | Llamada a función                                     | Izquierda     | `… ( … )`               |
| 18          | Encadenamiento opcional                               | Izquierda     | `?.`                    |
| 17          | `new` (sin lista de argumentos)                       | Derecha       | `new …`                 |
| 16          | Incremento sufijo                                     | n/a           | `… ++`                  |
| 16          | Decremento sufijo                                     | n/a           | `… --`                  |
| 15          | NOT lógico                                            | Derecha       | `! …`                   |
| 15          | NOT a nivel de bits                                   | Derecha       | `~ …`                   |
| 15          | Suma unaria                                           | Derecha       | `+ …`                   |
| 15          | Negación unaria                                       | Derecha       | `- …`                   |
| 15          | Incremento prefijo                                    | Derecha       | `++ …`                  |
| 15          | Decremento prefijo                                    | Derecha       | `-- …`                  |
| 15          | `typeof`                                              | Derecha       | `typeof …`              |
| 15          | `void`                                                | Derecha       | `void …`                |
| 15          | `delete`                                              | Derecha       | `delete …`              |
| 15          | `await`                                               | Derecha       | `await …`               |
| 14          | Potenciación (`**`)                                   | Derecha       | `… ** …`                |
| 13          | Multiplicación (`*`)                                  | Izquierda     | `… * …`                 |
| 13          | División (`/`)                                        | Izquierda     | `… / …`                 |
| 13          | Resto (`%`)                                           | Izquierda     | `… % …`                 |
| 12          | Adición (`+`)                                         | Izquierda     | `… + …`                 |
| 12          | Sustracción (`-`)                                     | Izquierda     | `… - …`                 |
| 11          | Desplazamiento de bits a la izquierda (`<<`)          | Izquierda     | `… << …`                |
| 11          | Desplazamiento de bits a la derecha (`>>`)            | Izquierda     | `… >> …`                |
| 11          | Desplazamiento de bits a la derecha sin signo (`>>>`) | Izquierda     | `… >>> …`               |
| 10          | Menor a (`<`)                                         | Izquierda     | `… < …`                 |
| 10          | Menor o igual a (`<=`)                                | Izquierda     | `… <= …`                |
| 10          | Mayor a (`>`)                                         | Izquierda     | `… > …`                 |
| 10          | Mayor o igual a (`>=`)                                | Izquierda     | `… >= …`                |
| 10          | `in`                                                  | Izquierda     | `… in …`                |
| 10          | `instanceof`                                          | Izquierda     | `… instanceof …`        |
| 9           | Igualdad (`==`)                                       | Izquierda     | `… == …`                |
| 9           | Desigualdad (`!=`)                                    | Izquierda     | `… != …`                |
| 9           | Igualdad estricta (`===`)                             | Izquierda     | `… === …`               |
| 9           | Desigualdad estricta (`!==`)                          | Izquierda     | `… !== …`               |
| 8           | AND a nivel de bits (`&`)                             | Izquierda     | `… & …`                 |
| 7           | XOR a nivel de bits (`^`)                             | Izquierda     | `… ^ …`                 |
| 6           | OR a nivel de bits (`\|`)                             | Izquierda     | `… \| …`                |
| 5           | AND lógico (`&&`)                                     | Izquierda     | `… && …`                |
| 4           | OR lógico (`\|\|`)                                    | izquierda     | `… \|\| …`              |
| 4           | Operador de coalescencia nula (`??`)                  | Izquierda     | `… ?? …`                |
| 3           | Operador condicional (ternario)                       | Derecha       | `… ? … : …`             |
| 2           | Asignación simple                                     | Derecha       | `… = …`                 |
| 2           | Asignación con suma                                   | Derecha       | `… += …`                |
| 2           | Asignación con resta                                  | Derecha       | `… -= …`                |
| 2           | Asignación con exponenciación                         | Derecha       | `… **= …`               |
| 2           | Asignación con multiplicación                         | Derecha       | `… *= …`                |
| 2           | Asignación con división                               | Derecha       | `… /= …`                |
| 2           | Asignación con módulo                                 | Derecha       | `… %= …`                |
| 2           | Asignación con desplazamiento a la izquierda          | Derecha       | `… <<= …`               |
| 2           | Asignación con desplazamiento a la derecha            | Derecha       | `… >>= …`               |
| 2           | Asignación con desplazamiento sin signo a la derecha  | Derecha       | `… >>>= …`              |
| 2           | Asignación con AND bit a bit                          | Derecha       | `… &= …`                |
| 2           | Asignación con XOR bit a bit                          | Derecha       | `… ^= …`                |
| 2           | Asignación con OR bit a bit                           | Derecha       | `… \|= …`               |
| 2           | Asignación con AND lógico                             | Derecha       | `… &&= …`               |
| 2           | Asignación con OR lógico                              | Derecha       | `… \|\|= …`             |
| 2           | Asignación con operador de fusión nula                | Derecha       | `… ??= …`               |
| 2           | `yield`                                               | Derecha       | `yield …`               |
| 2           | `yield*`                                              | Derecha       | `yield* …`              |
| 1           | Operador coma                                         | Izquierda     | `… , …`                 |

## Uso de Paréntesis para Controlar la Evaluación

En JavaScript, los operadores de agrupación () (paréntesis) son fundamentales para gestionar como se evalúan nuestras expresiones, en especial cuando estamos trabajado sobre situaciones con alto grado de complejidad donde la precedencia y la asociatividad pueden no ser evidentes a simple vista o en casos donde necesitamos alterar la forma en la que se resuelven nuestras operaciones y asegurarnos que nuestras expresiones sean evaluadas en el orden deseado.

### La importancia de los paréntesis en las expresiones complejas

La precedencia y asociatividad de los operadores define el orden en que se evaluarán nuestras expresiones si no se usan paréntesis. sin embargo, los paréntesis permiten alterar este comportamiento natural gracias a su propiedad de contener el máximo grado de precedencia, asegurando que las subexpresiones se resuelvan primero , sin tener en cuenta la precedencia y asociatividad de los demás operadores involucrados.

### Cómo los paréntesis modifican la precedencia y asociatividad

**Precedencia y paréntesis:**

```javascript
let x = 3;
let y = 4;
let z = 5;
let resultado = x + y * z; // se evaluara la multiplicación antes de la suma : 3 + (4 * 5) = 23
console.log(resultado); // 23
```

Pero si incorporamos paréntesis agrupando la suma para alterar el orden de evaluación obtenemos los siguiente:

```javascript
let x = 3;
let y = 4;
let z = 5;
let resultado = (x + y) * z; // se evaluará la suma antes de la multiplicación: (3 + 4) * 5 = 35
console.log(resultado); // 35
```

**Asociatividad y paréntesis:**

los operadores de suma y resta tienen asociatividad izquierda a derecha.

```javascript
let resultado = 10 - 2 - 3; // se evaluará cada operador de izquierda a derecha uno a uno: 10 - 2 - 3 = 5
console.log(resultado); // 5
```

Al incorporar paréntesis veremos como alteramos el orden de asociatividad:

```javascript
let resultado = 10 - (2 - 3); // se evaluara como 10 menos el agrupamiento de 2 - 3 : 10 - (2 - 3) = 11
console.log(resultado); // 11
```
