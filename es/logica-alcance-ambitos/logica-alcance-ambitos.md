# Manipulación de lógica de ciclo de vida de una variable en JavaScript

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
    - [¿Qué es el ámbito en JavaScript?](#qué-es-el-ámbito-en-javascript)
    - [Importancia del control de alcance](#importancia-del-control-de-alcance)
    - [Tipos de ámbito en JavaScript](#tipos-de-ámbito-en-javascript)

---

## Introducción:

### ¿Qué es el ámbito en JavaScript?

el ámbito (scope) en el motor de JavaScript define la accesibilidad y visibilidad de variables dentro de nuestro programa. Básicamente, establece dónde se pueden usar las variables y quién puede acceder a ellas.
Cuando una de nuestras variables es declarada dentro de un ámbito específico, solo puede ser accedida desde dentro de ese mismo ámbito o desde ámbitos internos (anidados).
Veamos un ejemplo:

```Javascript
var variableGlobal = "Hola, soy global.";

function mostrarVariables(){
  let variableLocal = "Hola, soy local";

  console.log(variableGlobal);
  console.log(variableLocal);
}

mostrarVatiables(); // salida 1 : Hola, soy global , salida 2 : Hola, soy local

console.log(variableGlobal); // salida Hola, soy global
console.log(variableLocal); // salida ReferenceError : variableLocal is no defined

```

### Importancia del control de alcance

Un mal manejo del ámbito nos puede provocar problemas de sobreescritura de variables, fugas de memoria y fallos en la seguridad del código. Algunas razones por las que debemos de poder controlar nuestros ámbitos son:
**Evita conflictos de nombres**: si dos de nuestras variables tienen el mismo nombre en distintos ámbitos, la incorrecta administración del alcance puede causar errores difíciles de depurar.
**optimización del uso de la memoria**: Mantener nuestras variables dentro del ámbito más reducido posible permite liberar memoria cuando ya no las necesitemos.
**Mejor mantenimiento y escalabilidad**: un código con nuestras variables bien definidas y con alcance limitado es más fácil de entender y modificar.
**Prevencion de acceso involuntario a datos**: evita que partes no autorizadas del código modifiquen o accedan a valores sensibles.

```javascript
var mensaje = "hola, desde global";

function mostrarVariable() {
    var mensaje = "hola, desde funcion";
    console.log(mensaje);
}

mostrarVariable(); // salida Hola, desde funcion
console.log(mensaje); // salida Hola, desde global
```

Si no manejamos bien los ámbitos, podríamos accidentalmente modificar variables que no deberíamos, lo que puede ocasionar errores que no esperaríamos.

### Tipos de ámbito en JavaScript

En el motor de JavaScrpit existen distintos niveles de ámbitos que nos definirán cómo se manejan nuestras variables, los principales son:
**Ámbito global:** las variables son accesibles desde cualquier parte del código.
**Ámbito de función:** las variables declaradas en una función solo son accesibles solo desde dentro de esa función.
**Ámbito de bloque:** las variables definidas dentro de bloque `{}` con let y const solo existen dentro de ese mismo bloque.
**Ámbito léxico:** las funciones en JavaScript recuerdan el ámbito en el que fueron creadas, lo que permite el uso de closures.
