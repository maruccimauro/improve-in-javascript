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
    - [Importancia de la precedencia en las expresiones](#importancia-de-la-precedencia-en-las-expresiones)
2. [Conceptos Fundamentales](#conceptos-fundamentales)
    - [Definición de precedencia de operadores](#definición-de-precedencia-de-operadores)
    - [Definición de asociatividad de operadores](#definición-de-asociatividad-de-operadores)
3. [Precedencia de Operadores en JavaScript](#precedencia-de-operadores-en-javascript)
    - [Lista de operadores con mayor a menor precedencia](#lista-de-operadores-con-mayor-a-menor-precedencia)
    - [Agrupación de operadores con la misma precedencia](#agrupación-de-operadores-con-la-misma-precedencia)
    - [Impacto de la precedencia en el orden de evaluación](#impacto-de-la-precedencia-en-el-orden-de-evaluación)
4. [Asociatividad de Operadores en JavaScript](#asociatividad-de-operadores-en-javascript)
    - [Operadores con asociatividad izquierda a derecha](#operadores-con-asociatividad-izquierda-a-derecha)
    - [Operadores con asociatividad derecha a izquierda](#operadores-con-asociatividad-derecha-a-izquierda)
5. [Uso de Paréntesis para Controlar la Evaluación](#uso-de-paréntesis-para-controlar-la-evaluación)
    - [La importancia de los paréntesis en las expresiones complejas](#la-importancia-de-los-paréntesis-en-las-expresiones-complejas)
    - [Cómo los paréntesis modifican la precedencia y asociatividad](#cómo-los-paréntesis-modifican-la-precedencia-y-asociatividad)
6. [Operadores Combinados y su Impacto](#operadores-combinados-y-su-impacto)
    - [Operadores aritméticos combinados (+=, -=, \*=, /=)](#operadores-aritméticos-combinados-+=-=--=-)
    - [Operadores de comparación y su interacción con otros operadores](#operadores-de-comparación-y-su-interacción-con-otros-operadores)
    - [Operadores lógicos combinados (&&, ||)](#operadores-lógicos-combinados--&&-)
7. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Confusión con la precedencia en expresiones complejas](#confusión-con-la-precedencia-en-expresiones-complejas)
    - [Evitar errores en la combinación de operadores](#evitar-errores-en-la-combinación-de-operadores)
    - [Uso de paréntesis para claridad](#uso-de-paréntesis-para-claridad)
8. [Comparación con otros Lenguajes](#comparación-con-otros-lenguajes)
    - [Diferencias de precedencia entre JavaScript y Python](#diferencias-de-precedencia-entre-javascript-y-python)
    - [Impacto de la precedencia en C++ y JavaScript](#impacto-de-la-precedencia-en-c-y-javascript)
9. [Conclusión y Recursos Adicionales](#conclusión-y-recursos-adicionales)
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

Vemos como en este caos los operadores paréntesis de agrupación alteran el orden natural de precedencia del restos de los operadores , ya que el nivel de precedencia que poseen es el más alto posible , con un nivel 19 (ya veremos esto en detalle más adelante).

### Importancia de la precedencia en las expresiones

Comprender el orden en que se ejecutan los operadores y como pueden afectar el resultado final de una expresión por su precedencia y asociatividad es fundamental para

**Evitar errores lógicos:** Si no entendemos bien una precedencia, una operación puede producirnos resultados que no esperamos.

**Mejora la legibilidad del código:** Si desarrollamos un código bien estructurado y con operadores correctamente aplicados nos permitirá facilidad a la hora de mantenerlo.

**Optimizar el rendimiento:** Al usar correctamente la lógica de precedencia y asociatividad podremos evitar que cálculos innecesarios y mejorar la eficiencia.
