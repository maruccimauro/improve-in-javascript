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
3. [Hoisting y su Impacto en el Ámbito](#hoisting-y-su-impacto-en-el-ámbito)
    - [¿Qué es el hoisting?](#qué-es-el-hoisting)
    - [Hoisting en `var`, `let` y `const`](#hoisting-en-var-let-y-const)
    - [Hoisting en funciones](#hoisting-en-funciones)
4. [Manipulación Avanzada del Ámbito](#manipulación-avanzada-del-ámbito)
    - [Manipulación con `this`](#manipulación-con-this)
    - [Diferencias entre `var`, `let` y `const`](#diferencias-entre-var-let-y-const)
    - [El uso de `bind`, `call` y `apply`](#el-uso-de-bind-call-y-apply)
    - [Ámbitos en funciones flecha](#ámbitos-en-funciones-flecha)

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

## Manipulación Avanzada del Ámbito

### Manipulación con `this`

El valor de this se refiere al objeto en el que se ejecuta el código. Dependiendo de cómo se invoque, this puede referirse a diferentes objetos. El valor de this se determina e tiempo de ejecución, no en el momento de la declaración.

**Comportamiento de this en diferentes contextos:**
**En el contexto global:** en el contexto global(fuera de cualquier función) this hace referencia al objeto global, en un navegador, será el objeto windows.

```Javascript
console.log(this)
```

**En una funcion:** dentro de la función, el valor de this depende de si es invocada en modo estricto o no.

```javascript
"use strict";
function verThis() {
    console.log(this);
}
verThis(); // salida undefined
```

```javascript
function verThis() {
    console.log(this);
}
verThis(); //salida windows
```

**En métodos de objetos:** Cuando una función es llamada como un método de un objeto, this hace referencia a ese objeto.

```javascript
const miObj = {
    nombre: "mauro",
    saludar: function () {
        console.log(this.nombre);
    },
};

obj.saludar();
```

**Valor de this en función de flecha:** las funciones flecha `=>` no tienen su propio this. En su logar heredan el valor de this del contexto en el que fueron definidas (su ámbito léxico).

```javascript
const miObj = {
    nombre: "mauro",
    saludar: function () {
        setTimeout(() => {
            console.log(this);
        }, 1000);
    },
    verThis: () => this,
};

const miFuncionFlecha = () => {
    console.log(this);
};

miFuncionFlecha(); // windows,
console.log(miObj.verThis()); // windows aunque sea no intuitivo , el ambito en el
// que se declara verThis es el ambito global , quien es su ambito lexico.
miObj.saludar(); // miObj
```

**valor de this en clase:** en el contexto de las clases, this hace referencia a la instancia de clase.

```javascript
class Persona {
    constructor(nombre) {
        this.nombre = nombre;
    }
    getNombre() {
        console.log(this.nombre); // this hace referencia a la instancia de la clase.
    }
}

const persona = new Persona("Mauro");
persona.getNombre();
```

### Diferencias entre `var`, `let` y `const`

En el motor de JavaScript las palabras claves `var`,`let` y `const` la usaremos para declarar variables, pero tienen diferencias importantes en cuanto a su comportamiento dentro del ámbito.

**var:**
Ámbito de función: las variables declaradas con `var` tienen ámbito de función. esto significa que si se declaran dentro de una función solo son accesibles desde dentro de esa función, si se declaran fuera de una función son accesibles globalmente.
Hoisting: las declaraciones de nuestras variables con `var` son elevadas al principio de su contexto de ejecución, pero su inicialización no, por eso será accesibles pero con un valor undefined.
Redefinición: es posible que redeclaremos una variable con `var` dentro del mismo ámbito.

```javascript
var nombre = "Juan";
var nombre = "Mauro"; // esto no nos va a dar error
```

**let**:
Ámbito de bloque: Las variables que declaremos con `let` tienen un ámbito de bloque, lo que significa que solo están accesibles dentro del bloque (delimitado por {}) donde se declaran, ya sea una función o un bloque condicional.
Hoisting: al igual que var, las variables declaradas con let son elevadas, pero no se pueden acceder hasta que se alcanzan en nel flujo del código. Esto se llama "zona muerta temporal" (TDZ).
Re declaración: a diferencia de `var`, no es posible redeclarar una variable declarada con let en el mismo ámbito.

```javascript
let nombre = "Juan";
let nombre = "Mauro"; // esto nos dara error
```

const:
Ámbito de bloque: al igual que con `let`, nuestras variables declaradas con `const` tendrán ámbito de bloque.
Reasignación y redeclaración: una variable declarada con `const` no puede ser reasignada ni redeclarada despues de su declaración inicial.
Hoisting: al igual que con `let`, las variables declaradas `const` son elevadas al inicio del contexto de ejecución pero no pueden ser accedidas ya que se encontraran en la "zona muerta temporal" (TDZ).
inmutabilidad de referencia: si se declara un objeto con `const`, su referencia no puede ser cambiada, pero los contenidos del objeto pueden modificarse.

```javascript
const nombre = "Juan";
nombre = "Mauro"; // esto nos dara error

const obj = { nombre: "Juan" };
obj.nombre = "Mauro"; //esto NO dara error
```

### El uso de `bind`, `call` y `apply`

`bind` nos servirá para crear una nueva función que tiene su propio contexto (this). Esta nueva función la podremos llamar más tarde, y siempre tendrá el valor de this especificado.

```Javascript
const persona = { nombre : "Mauro"};
function crearSaludo(){
  console.log(`Hola, ${this.nombre}!`);
}

const saludo = crearSaludo.bind(persona);// salida Hola, Mauro!
```

`call` ejecutara nuestra función inmediatamente, pero le permitirá especificar el valor de this y pasar los argumentos de la función que deseemos. Los argumentos se pasan de manera separada uno por uno.

```javascript
const persona = { nombre: "Mauro" };
function saludar(arg1, arg2) {
    console.log(`${arg1} ${this.nombre}${arg2}`);
}

saludar.call(persona, "Hola", "!"); // salida Hola, Mauro!
```

`apply` es similar a `call`, pero los argumentos se pasan como un array, esto es útil cuando no sabemos cuántos argumentos tendrá la función.

```javascript
const persona = { nombre: "Mauro" };
function saludar(saludo, puntuacion) {
    console.log(saludo + ", " + this.nombre + puntuacion);
}
cuerpoSaludo = ["Hola", "!"];
saludar.apply(persona, cuerpoSaludo); // salida Hola, Mauro!
```

### Ámbitos en funciones flecha

En una función flecha, el valor de this será el mismo que el de su entorno léxico (es decir, el valor de `this` en el contexto donde la función fue definida, no donde fue llamada). Esto soluciona muchos problemas comunes con `this` en funciones tradicionales, especialmente en eventos y callbacks.

veamos un ejemplo

```Javascript

const obj = {
  nombre:"Mauro",
  saludar: function (){
    setTimeout(()=>{
      console.log(`Hola ${this.nombre}!`)
    },1000)
  }
}

obj.saludar()// saida Hola, Mauro!
```

En este ejemplo, el valor de `this` dentro de la función flecha es el mismo que el de `this` en la función `saludar`, que es el objeto `obj`. Esto es posible porque las funciones flecha no crean su propio `this`, sino que lo heredan del contexto en el que fueron definidas.
