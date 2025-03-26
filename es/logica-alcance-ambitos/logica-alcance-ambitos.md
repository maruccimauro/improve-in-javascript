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
2. [Ámbito en JavaScript](#ámbito-en-javascript)
    - [Ámbito global](#ámbito-global)
    - [Ámbito de función](#ámbito-de-función)
    - [Ámbito de bloque (let y const)](#ámbito-de-bloque-let-y-const)
    - [Ámbito léxico y closure](#ámbito-léxico-y-closure)

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

## Ámbito global

El ámbito global es el nivel más externo del ámbito en un programa de JavaScript. Las Variables declaradas fuera de cualquier función o bloque tienen ámbito global y son accesibles desde cualquier parte del código, incluyendo dentro de las funciones y bloques, el uso excesivo de variables globales puede dar lugar a problemas como la sobreescritura de valores y la dificultad de depurar el código. En un entorno de navegador, las variables globals se añaden al objeto windows. en node.js , se añaden al objeto global. Las declaraciones con `var` dentro de bloques que no estén dentro de funciones son levantadas al contexto global.

veamos unos ejemplos:

```javascript
let variableGLobal = "Variable global";

function miFuncion() {
    console.log(gvariableGLobal);
}

miFuncion(); // salida Variable global
console.log(variableGLobal); // salida Variable global
```

Aquí podemos apreciar como definimos una variable global que es accedida dentro de una función y también desde el contexto global.

```javascript
if (true) {
    var variableGLobal = "Variable global";
}

console.log(variableGLobal); //salida Variable global
```

En este caso vemos como `variableGlobal` que pertenece a un ámbito de bloque fue ascendida por el uso de `var`.

### Ámbito de función

El ámbito de función es un ámbito que se crea cuando declaramos una función. Las variables que definimos ahí dentro solo son accesibles dentro de la misma función, es decir, son local a la función misma y no afectan a las variables fuera de ella, lo que nos ayuda a encapsular lógica y evitar efectos secundarios no deseados.

Veamos un ejemplo

```javascript
function mostrarVariable() {
    var variableLocal = "soy una variable local";
    console.log(variableLocal);
}
mostrarVariable(); // salida soy una variable local
console.log(variableLocal); // salida ReferenceError: variableLocal is not defined
```

Aquí vemos como definimos una variable que es completamente accesible desde la función y su ámbito local, pero una vez salimos al ámbito global la variable en cuestión ya no es accesible por lo cual recibiremos un error de definición.

### Ámbito de bloque (let y const)

El ámbito de bloque se refiere al alcance de las variables declaradas dentro de bloques de código, como los definidos por estructuras como if, for , while o funciones. En estos casos nuestras variables declaradas serán solo accesibles dentro del mismo bloque donde fueron declaradas.
veamos un ejemplo

```javascript
if (true) {
    let variableLocal = "soy una variable local";
    console.log(variableLocal); // salida soy una variable local
}

console.log(variableLocal); // salida ReferenceError: variableLocal is not defined
```

Aqui podemos observar como ``variableLocal` es perfectamente accesible desde dentro del ámbito del bloque `{}` pero una vez terminado este ámbito y haber accedido al ámbito superior del mismo ya no podemos acceder a ella , recibiendo un error de definición.

### Ámbito léxico y closure

El ámbito léxico se refiere al hecho de que una función tiene acceso a las variables del ámbito en el que fue creada, no donde se ejecuta. Esto significa que una función tiene acceso a las variables de su contexto de creación, incluso si se ejecuta fuera de ese contexto.
Un closure es una función que "recuerda" el entorno, es decir variables y parámetros, en el que fue creada incluso después de que el contexto externo a ella haya terminado de ejecutarse. esto se debe a que la función mantiene una referencia a las variables de su ámbito léxico.

Veamos un ejemplo sencillo

```javascript
function crearContador() {
    let conteo = 0;
    return () => {
        conteo++;
        console.log(conteo);
    };
}

const contador1 = crearContador();
contador1(); // salida 1
contador1(); // salida 2
const contador2 = crearContador();
contador2(); // salida 1
```

En este caso tenemos a la función `crearContador` que devuelve una función interna que mantendrá el acceso a la variable conteo, a pesar de que la ejecución de `crearContador` ya haya finalizado. Aunque la ejecución de la función de retorno es ejecutada en otro ámbito al de su creación , tiene la capacidad de mantener su propio recuerdo de `conteo` debido a las capacidades de los closures de recordar su contexto de léxico de creación.

## Hoisting y su Impacto en el Ámbito

### ¿Qué es el hoisting?

El hoisting es un comportamiento del motor de JavaScript que implica la "elevación" de las declaraciones de variables y funciones a la parte superior de su contexto de ejecución antes de que el código sea ejecutado, cabe aclarar que en el caso de las variables solo las declaraciones son elevadas, no su inicialización(su valor asignado explícitamente) y en el caso de las funciones son movidas completamente incluyendo tanto su declaración como su cuerpo, lo que nos permitirá llamarlas antes de su declaración explicita en nuestro código.

### Hoisting en `var`, `let` y `const`

**Hoisting en var**
Las variables declaradas con `var` son elevadas, pero solo se elevará su declaración. no su valor explicito. Esto significa que podremos hacer referencia a ella antes de su asignación. pero su valor será undefined.

Veamos un ejemplo de esto:

```javascript
console.log(variableElevada); // salida undefined
var variableElevada = "variable elevada";
console.log(variableElevada); // salida variable elevada
```

Aqui vemos como en el primer llamado a la salida obtenemos undefined ya que solo la definicion de la variable fue elevada por el hoisting, y no su valor.

**Hoisting con let y const**
Nuestras variables creadas con let y const también serán elevadas, pero tienen un comportamiento distinto. Aunque la declaración se eleve, no podremos acceder a ellas antes de su inicialización explicita, intentar acceder a ellas antes de esto nos devolverá un error de referencia. A este concepto se le atribuye la denominación de que las variables estarán en TDZ (The Dead Zone) o la zona muerta.

```javascript
console.log(b); // salida ReferenceError: Cannot access 'b' before initialization

let b = "valor de b";
```

En este caso vemos como `b` es elevada gracias al hosting , pero no podemos acceder a ella.

### Hoisting en funciones

El hosting también aplica a las funciones, pero su comportamiento es ligeramente diferente si se declaran como definición de función o expresión de función.

**Hosting con declaración de funcion:**
Las declaraciones de función son completamente elevadas, lo que significa que puedes llamar a una función antes de su declaración con el código.

```javascript
mostrarMensaje();

function mostrarMensaje() {
    console.log("mensaje");
}
```

Arriba podemos observar como la función es ejecutada correctamente pese a que su llamada esta antes de su definición explicita dentro del código.

**Hoisting con expresión de función:**
Las expresiones de función no son elevadas como las declaraciones. si intentamos llamar a una expresión de función antes de su definición, obtendremos un error, ya que solo se eleva la declaración de la variable y no la asignación de la función.

```Javascript
mostrarMensaje(); //salida mostrarMensaje is not a function

var mostrarMensaje = function () {
  console.log("mensaje")
}
```

Vemos como en este caso la declaración de la variable es elevada, pero no el contenido de la función , por lo que podemos acceder a la variable pero no al cuerpo de la función.
