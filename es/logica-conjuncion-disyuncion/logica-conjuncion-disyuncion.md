# Manipulación de Lógica de Evaluación de Conjunción y Disyunción

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
    - [¿Qué es la conjunción (AND) y la disyunción (OR)?](#qué-es-la-conjunción-and-y-la-disyunción-or)
    - [Importancia en la lógica de programación](#importancia-en-la-lógica-de-programación)
2. [Conceptos Fundamentales](#conceptos-fundamentales)
    - [El operador `&&` (AND) en profundidad](#el-operador--and-en-profundidad)
    - [El operador `||` (OR) en profundidad](#el-operador--or-en-profundidad)
    - [Valores truthy y falsy en la evaluación lógica](#valores-truthy-y-falsy-en-la-evaluación-lógica)
    - [Diferencias clave en la evaluación de AND y OR](#diferencias-clave-en-la-evaluación-de-and-y-or)
3. [Evaluación de Expresiones Booleanas](#evaluación-de-expresiones-booleanas)
    - [Cómo evalúa JavaScript los operadores AND y OR](#cómo-evalúa-javascript-los-operadores-and-y-or)
    - [Precedencia y asociatividad de los operadores lógicos](#precedencia-y-asociatividad-de-los-operadores-lógicos)
    - [Combinación de AND y OR en expresiones complejas](#combinación-de-and-y-or-en-expresiones-complejas)
4. [Evaluación de Cortocircuito](#evaluación-de-cortocircuito)
    - [Cómo funciona el cortocircuito con `&&`](#cómo-funciona-el-cortocircuito-con-)
    - [Cómo funciona el cortocircuito con `||`](#cómo-funciona-el-cortocircuito-con-)
    - [Casos prácticos de evaluación de cortocircuito](#casos-prácticos-de-evaluación-de-cortocircuito)
5. [Uso Avanzado y Manipulación](#uso-avanzado-y-manipulación)
    - [Uso de `&&` y `||` en asignaciones predeterminadas](#uso-de--y--en-asignaciones-predeterminadas)
    - [Doble negación (`!!`) y coerción explícita](#doble-negación--y-coerción-explícita)
    - [Operadores lógicos en combinación con nullish coalescing (`??`)](#operadores-lógicos-en-combinación-con-nullish-coalescing-)
    - [Uso de operadores lógicos en funciones y retorno de valores](#uso-de-operadores-lógicos-en-funciones-y-retorno-de-valores)
6. [Casos de Uso en la Práctica](#casos-de-uso-en-la-práctica)
    - [Validaciones de entrada de usuario](#validaciones-de-entrada-de-usuario)
    - [Condiciones en estructuras de control](#condiciones-en-estructuras-de-control)
    - [Filtrado y manipulación de arrays con AND y OR](#filtrado-y-manipulación-de-arrays-con-and-y-or)
    - [Optimización de código con operadores lógicos](#optimización-de-código-con-operadores-lógicos)
7. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Confusión entre `&&` y `||` en expresiones anidadas](#confusión-entre--y--en-expresiones-anidadas)
    - [Uso incorrecto de truthy y falsy en condiciones](#uso-incorrecto-de-truthy-y-falsy-en-condiciones)
    - [Manejo seguro de valores con operadores lógicos](#manejo-seguro-de-valores-con-operadores-lógicos)
8. [Comparación con Otros Lenguajes](#comparación-con-otros-lenguajes)
    - [Evaluación lógica en Python, Java y JavaScript](#evaluación-lógica-en-python-java-y-javascript)
    - [Diferencias de comportamiento en TypeScript](#diferencias-de-comportamiento-en-typescript)
9. [Conclusión y Recursos Adicionales](#conclusión-y-recursos-adicionales)
    - [Resumen de los conceptos clave](#resumen-de-los-conceptos-clave)
    - [Ejercicios y desafíos prácticos](#ejercicios-y-desafíos-prácticos)

---

## 1. Introducción

La manipulación de la lógica de conjunción (&&) y disyunción (||) es fundamental en la programación para relacionarnos de manera correcta con el motor de JavaScript. Estos conceptos nos permiten evaluar condiciones de una manera eficiente, nos facilitan redactar expresiones con toma de decisiones.

### ¿Qué es la conjunción (AND) y la disyunción (OR)?

En lógica booleana, la conjunción (&&) y la disyunción (||) son operadores binarios que nos permiten combinar expresiones booleanas.

**Conjunción lógica (&&) - AND:**
Nos devolverá true si todas nuestras condiciones son true. Si alguna es false, el resultado es false.

```javascript
console.log(true && true); // true
console.log(true && false); // false
console.log(false && false); // false
```

```javascript
let edad = 25;
let tieneLicencia = true;

if (edad >= 18 && tieneLicencia) {
    console.log("puedes conducir");
}
```

**Disyunción logica (||) OR:**
nos devolvera true si al menos una de todas nuestras condiciones es true, solo nos devolvera false si todas son false.

```javascript
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false
```

```javascript
let esAdmin = false;
let esModerador = true;

if (esAdmin || esModerador) {
    console.log("tienes acceso al panel.");
}
```

Ambos operadores nos son útiles para evaluar más de una condición y generar toma de decisiones dentro del Código.

### Importancia en la lógica de programación

La conjunción y la disyunción nos facilitan el control del flujo al permitirnos evaluar varias condiciones sin necesidad de múltiples if, definir valores predeterminados de forma segura y reducir el código redundante.

Cuando no usamos conjuncion :

```javascript
let temperatura = 30;
let tormenta = false;

if (tormetan == false) {
    if (temperatura > 15) {
        if (temperatura < 35) {
            console.log("El clima es agradable");
        }
    }
}
```

¡Cuando si usamos conjuncion!:

```javascript
let temperatura = 30;
if (!tormenta && temperatura > 15 && temperatura < 35) {
    console.log("El clima es agradable.");
}
```
