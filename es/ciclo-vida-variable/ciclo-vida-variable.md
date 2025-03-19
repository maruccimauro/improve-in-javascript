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
    - [Ciclo de vida de una variable en JavaScript](#ciclo-de-vida-de-una-variable-en-javascript)
2. [Tipos de Variables](#tipos-de-variables)
    - [Variables no declaradas (undeclared)](#variables-no-declaradas-undeclared)
    - [Variables indefinidas (undefined)](#variables-indefinidas-undefined)
    - [Comparación con null con undefined](#comparación-con-null-con-undefined)
3. [Inicialización de Variables](#inicialización-de-variables)
    - [Proceso de inicialización](#proceso-de-inicialización)
4. [Reasignación de Variables](#reasignación-de-variables)
    - [Modificación del valor de una variable](#modificación-del-valor-de-una-variable)
    - [Efectos de la reasignación](#efectos-de-la-reasignación)
5. [Recolección de Basura (Garbage Collection)](#recolección-de-basura-garbage-collection)
    - [Qué es y cómo funciona en JavaScript](#qué-es-y-cómo-funciona-en-javascript)
6. [Eliminación de Variables](#eliminación-de-variables)
    - [Uso de `delete`](#uso-de-delete)
7. [Buenas Prácticas](#buenas-prácticas-y-errores-comunes)
8. [Conclusión](#conclusión)

---

## Introducción

### Ciclo de vida de una variable en JavaScript

El ciclo de vida de una variable en JavaScript se describe por las etapas que pasa una variable desde su creación hasta su destruccion. Entender este ciclo nos sera fundamental para que entendamos cómo funcionan las variables dentro del contexto de ejecucion de nuestro programa y cómo la memoria se maneja en JavaScript. Las variables en JavaScript pueden tener diferentes estados y, dependiendo de su manipulación pueden experimentar comportamientos especificos como la inicializacion, reasignacion, recoleccion de basura(garbage collection) y eliminacion.

## Tipos de Variables

Variables no declaradas (undeclared)
En JavaScript, una variable no declarada es aquella que utilizamos sin haber sido declarada previamente con var, let o const.
Esto puede ocurrir de dos maneras:
Uso implícito:
si asignamos un valor a un nombre que no hayamos declarado, el motor de JavaScript creara automáticamente una variable global con ese nombre. Por Ejemplo:

```javascript
function example() {
    y = 20; // Se crea como variable global
}
example();

console.log(y); // 20
console.log(window.y); // 20 (en el navegador)
```

En este caso creamos una variable global que puede llevar a comportamientos inesperados y difíciles de depurar.

Por otra parte, si intentamos acceder a una variable no declarada sin haber asignado ningún valor (sin que el motor de JavaScript la haya creado implícitamente en el ámbito global) obtendremos un error `ReferenceError`

```javascript
console.log(variable_no_asignada);
```

### Variables indefinidas (undefined)

Las variables indefinidas son aquellas que hemos declarado pero todavía no las inicializamos asignándoles ningún valor, Es decir las definimos en el código pero no tienen ningún valor asignado en el momento de su creación, y el motor de JavaScript automáticamente le asignara un valor `undefined`.

```javascript
let x; // hemos declarado a x , pero nunca le asignamos ningún valor.
console.log(x); // salida : undefined
```

### Comparación con null con undefined

Es importante que notemos que undefined y null son dos tipos diferentes en JavaScript, aunque ambos se utilizan para indicar la ausencia de un valor y pertenecen a los valores nullish, undefine se asigna automáticamente cuando una variable no tiene valor, mientras que null es un valor explicito que asignamos para indicar la ausencia intencional de un valor.

```Javascript
console.log(null === undefined) // false
```

aquí podemos observar que null y undefined son diferentes.

## Inicialización de Variables

La inicialización de una variable en JavaScript es el proceso por el cual le asigna un valor después de haber sido declarada.

### Proceso de Inicialización

**inicialización implícita** : Nuestra variable se crea en memoria pero no le asignamos ningún valor definido aún, se le asigna automáticamente undefined si es var o let, const por otra parte nos obliga a asignarle un valor en el momento de la declaración.

```javascript
let x; //undefined
var y; //undefined
```

**inicialización explicita** : declaramos la variable y le asignamos un valor en ese mismo momento.

```javascript
let x = 10; // 10
var y = 5; // 5
```

## Reasignación de Variables

La reasignación de una variable en JavaScript ocurre cuando le asignamos un nuevo valor después de haberla declarado e inicializado. Dependiendo del tipo de variable (var, let, const), la posibilidad de reasignación y sus efectos varían.

### Modificación del Valor de una Variable

Cuando manipulamos declaraciones del tipo var y let, es posible modificar el valor de la variable en cualquier momento después de su declaración, con const no se permite reasignar un nuevo valor después de la declaración, Aunque const no nos permite reasignar un nuevo valor, en el caso de objetos y arreglos sí es posible modificar su contenido interno.

```javascript
let x = 10;
console.log(x); // 10
x = 20; // Se reasigna el valor
console.log(x); // 20

const y = 30;
y = 40; // TypeError: Assignment to constant variable

const obj = { edad: 30 };
obj.edad = 34;
console.log(obj.edad); // 34
```

### Efectos de la Reasignación.

Para variables de tipos primitivos (números, cadenas, booleanos), la reasignación reemplaza el valor anterior en nuestra variable.
Para tipos de referencia (objetos, arreglos, funciones), la reasignación cambia la referencia almacenada en la variable, apuntando a un nuevo objeto en memoria.

## Recolección de Basura (Garbage Collection)

La recolección de basura (garbage collection) es un proceso automático del motor de JavaScript que gestiona la memoria del programa.Su objetivo principal es liberar espacio en la memoria eliminando nuestros objetos y variables que ya no son accesibles, evitando así fugas de memoria.

### Qué es y cómo funciona en JavaScript

En JavaScript, la recolección de basura se realiza de manera automática y está basada en el algoritmo de referencias contadas y marcado y barrido.

**Referencias contadas:** Cada objeto tiene un contador de referencias que indica cuántas variables o estructuras de datos lo están utilizando. Cuando este contador llega a cero, el objeto es candidato para ser eliminado.

**Marcado y barrido (Mark-and-sweep):** El motor de JavaScript recorre el grafo de objetos, marcando aquellos que están accesibles y limpiando los que no tienen referencias vivas. El proceso de barrido elimina nuestros objetos marcados como inalcanzables.

## Eliminación de Variables:

La eliminación de nuestras variables en JavaScript es un aspecto importante de la gestión de memoria. Aunque JavaScript tiene un recolector de basura automático, entender cómo y cuando las variables son eliminadas puede ayudarnos a escribir código más eficiente y evitar posibles problemas.
Podemos utilizar el operador delete para eliminar propiedades de un objeto. Sin embargo, su comportamiento es diferente cuando se aplica a variables.

### Uso de `delete`

**Eliminación de propiedades de objetos**
Cuando usamos delete en la propiedad de un objeto la propiedad es eliminada y el objeto modificado.

```javascript
let miObj = { nombre: "Mauro", edad: "34" };

console.log(miObj.nombre); // Mauro

delete miObj.edad;

console.log(miObj.nombre); // Mauro
```

**Eliminacion de variables globales**
En el contexto global, si hemos declarado una variable implícitamente (sin var, let, const), delete puede eliminarla.

```javascript
function func() {
    x = 10;
}

y = 5;
func();

delete x;
delete y;

console.log(x); // ReferenceError
console.log(y); // ReferenceError
```

**Eliminación de variables declaradas con var, let o const**
No podemos eliminar variables declaradas con var, let o const usando delete. Estas variables tienen atributos internos que lo evitan.

```javascript
var x = 15;
var y = 10;
var z = 5;

delete x;
delete y;
delete z;

console.log(x); // 15
console.log(y); // 10
console.log(z); // 5
```

## Buenas Prácticas

**Utilizar let y const en lugar de var** : tanto let como const tienen ámbito de bloque, lo que nos ayuda a evitar comportamientos inesperados y errores comunes asociados con el ámbito de var.

**Declarar variables antes de usarlas**: siempre debemos declarar nuestras variables antes de usarlas. Esto nos evitara errores de `ReferenceError` y mejorara la claridad de nuestro código.

**Inicializar variables explícitamente**: debemos asignar valores a nuestras variables tan proto como sea posible después de la declaración.

**Usar null y undefined cuando corresponda**: utilicemos null para indicar la ausencia intencional de valor y undefined para indicar que una variable no fue inicializada.

## Conclusión

Dominar el ciclo de vida de nuestras variables en JavaScript es esencial para cualquier de nosotros como desarrolladores, sobre todo en aquello que busquen escribir código limpio, eficiente y libre de errores. Desde la declaración hasta la recolección de basura, cada etapa tiene implicaciones importantes para la gestión de la memoria y el comportamiento de nuestro programa.

---

Muchas Gracias por leerme!
Marucci Mauro
[www.linkedin.com/in/mauro-marucci/](https://www.linkedin.com/in/mauro-marucci/)
[https://github.com/maruccimauro](https://github.com/maruccimauro)

---
