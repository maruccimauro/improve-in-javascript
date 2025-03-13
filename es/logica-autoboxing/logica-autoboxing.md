# Manipulación de lógica de autoboxing y sus implicacias en JavaScript

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
    - [¿Qué es el autoboxing en JavaScript?](#qué-es-el-autoboxing-en-javascript)
    - [Contextos en los que ocurre](#contextos-en-los-que-ocurre)
    - [Datos primitivos vs objetos](#datos-primitivos-vs-objetos)
    - [Desempaquetado implícito (unboxing)](#desempaquetado-implícito-unboxing)
    - [Diferencia entre valueOf y toString en unboxing](#diferencia-entre-valueof-y-tostring-en-unboxing)
2. [Interacción con Prototipos y Métodos Nativos](#interacción-con-prototipos-y-métodos-nativos)
    - [Prototipo en JavaScript y su relación con el autoboxing](#prototipo-en-javascript-y-su-relación-con-el-autoboxing)
    - [Modificación de prototipos y sus efectos](#modificación-de-prototipos-y-sus-efectos)
3. [Buenas Prácticas](#buenas-prácticas)
4. [Efectos de Autoboxing en Rendimiento a gran escala](#efectos-de-autoboxing-en-rendimiento-a-gran-escala)

---

## Introducción

Primero debemos saber que JavaScript es un lenguaje que internamente maneja la conversión entre tipos primitivos y objetos a través de un mecanismo conocido como autoboxing. Este proceso nos permite hacer que los valores primitivos, como números, cadenas de texto o booleanos, accedan temporalmente a métodos y propiedades como si fueran objetos.

### ¿Qué es el autoboxing en JavaScript?

El **autoboxing** lo conoceremos como el proceso mediante el cual Javascript convierte implícitamente un tipo primitivo (como un número , cadena de texto o booleano) en su objeto correspondiente cuando se intenta acceder a métodos o propiedades.

El motor de JavaScript tiene tres tipos primitivos (de un total de 6) que pueden ser envueltos automáticamente en objetos de esta manera para generar el autoboxing:
Cadenas de texto : new String(string)
Numeros : new Number(number)
Valores Booleanos: new Boolean(boolean)

Veamos un ejemplo para comprenderlo mejor.

```javascript
console.log("Hola!".toUpperCase()); // "HOLA!"
```

Ahora veamos los pasos que sucedieron implícitamente:

1. El motor de JavaScript detecta que "Hola!" es un valor primitivo del tipo string.
2. Crea un objeto temporal: new String("Hola!").
3. Accede al método .toUpperCase() de ese objeto que no creo anteriormente.
4. Nos devuelve "HOLA!".
5. Elimina el objeto temporal para liberar memoria.

¡Esto nos permite que nuestros valores primitivos tengan acceso a métodos sin necesidad de ser explícitamente convertidos en objetos!

### Contextos en los que ocurre

El autoboxing ocurre automáticamente en estos contextos:

**Cuando llamamos a un método encadenado.**

```javascript
console.log((42).toFixed(2)); // 42.00
console.log("Hola".toUpperCase()); // "HOLA"
console.log(true.toString().toUpperCase()); // "TRUE"
```

**Cuando intentamos acceder a sus propiedades.**

```javascript
console.log("evaluacion"["length"]);
```

**En Iteraciones sobre cadenas de texto**
El motor de JavaScript trata al string primitivo como un objeto temporal cuando usamos for...of:

```javascript
for (const char of "cadena") {
    console.log(char);
}
```

```javascript
for (const char of "cadena") {
    console.log(char);
}
```

### Datos primitivos vs objetos

**Dato primitivos**
Para que podamos comprender correctamente el autoboxing en JavaScript, es fundamental que diferenciemos entre tipos de datos primitivos y objetos, ya que el autoboxing ocurre cuando JavaScript necesita convertir nuestro dato primitivo en un objeto temporalmente.
Los tipos de datos primitivos son aquellos que no son objetos y no tienen métodos ni propiedades propias, esto incluye a :

| Tipo      | Ejemplo             | Descripción                                  |
| --------- | ------------------- | -------------------------------------------- |
| string    | `"Hola"`            | Secuencia de caracteres                      |
| number    | `42`                | Números enteros y de punto flotante          |
| bigint    | `9007199254740991n` | Números grandes (introducido en ES11)        |
| boolean   | `true`, `false`     | Valores lógicos                              |
| undefined | `undefined`         | Valor asignado a variables no inicializadas  |
| null      | `null`              | Representa la ausencia intencionada de valor |
| symbol    | `Symbol("id")`      | Identificadores únicos                       |

Estos datos tienen la propiedad de ser inmutables y se almacenan por valor, lo que significa que cualquier operación sobre ellos crea un nuevo valor en lugar de modificar el original.

```javascript
let x = "Hola";
let y = x.toUppperCase(); // se crea un una nueva cadena "HOLA", x seguira siendo "Hola".
console.log(x); //"Hola"
console.log(y); //"HOLA"
```

**Objetos en JavaScript**
A diferencia de los primitivos, nuestros objetos en JavaScript son estructuras más complejas que pueden almacenar múltiples valores y métodos. Algunos ejemplos de objetos incluyen instancias de clases, arrays, funciones, objetos literales, etc.
Los objetos se almacenan por referencia, lo que significa que dos de nuestras variables pueden apuntar al mismo objeto en memoria, veamos un ejemplo de esto:

```JavaScript
let obj1 = { saludos: "Hola" };
let obj2 = obj1;

obj2.saludos = "Hola Mundo!";

console.log(obj1.saludos); // "Hola Mundo!", el obj1 y el obj2 hacen referencia a la misma dirección en memoria.
```

**diferencias principales**
veamos una tabla de diferencias entre tipos de datos primitivos y objetos.

| Característica        | Tipos Primitivos                                                       | Objetos                                              |
| --------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------- |
| Tipos                 | `string`, `number`, `bigint`, `boolean`, `undefined`, `null`, `symbol` | `Object`, `Array`, `Function`, `Date`, etc.          |
| Inmutabilidad         | **Inmutables**: no se pueden modificar, solo reemplazar                | **Mutables**: sus propiedades pueden cambiar         |
| Asignación            | Se asignan y comparan por **valor**                                    | Se asignan y comparan por **referencia**             |
| Almacenamiento        | Se guardan en la **pila (stack)**                                      | Se guardan en el **heap** y la referencia en la pila |
| Copia                 | Se copia el **valor** directamente                                     | Se copia la **referencia**, no el contenido          |
| Comparación (`===`)   | Compara los **valores** directamente                                   | Compara las **referencias**, no el contenido         |
| Métodos y propiedades | No tienen métodos ni propiedades propios                               | Pueden tener métodos y propiedades definidas         |

### Desempaquetado implícito (unboxing)

podríamos decir que el **unboxing** es el proceso inverso al **autoboxing**,consiste en convertir un objeto envolvente (String, Number, Boolean) de vuelta en su valor primitivo cuando necesitamos operar con él en un contexto donde no se aceptan objetos. Este proceso ocurre de manera automática dentro del motor de JavaScript y se basa en los métodos `valueOf()` y `toString()`.

**Como ocurre el unboxing**
podremos observar el desempaquetado en estos casos:

Cuando usamos un objeto envolvente en operaciones matemáticas o de concatenación.
Ej.

```JavaScript
let numObj = new Number(10);
let resultado = numObj + 5; //se realizara el unboxing implícito de numObj

console.log(resultado) // 15
console.log(typeOf numObj) // "object"
console.log(typeOf resultado) // "number"
```

Cuando realizamos una comparación de igualdad no estricta (==) entre un objeto envolvente y un valor primitivo.

```Javascript
let boolObj = new Boolean(false)
resultado = boolObj == false // se realiza el unboxing implicito boolObj
console.log(resultado) // true
console.log(typeof boolObj) // Object
console.log(typeof resultado) //boolean
```

En estos casos JavaScript intentara convertir el objeto en un primitivo utilizando este orden de prioridad:
**valueOf()** , se llama primero si está disponible y devuelve el valor primitivo.
**toString()**, si `valueOf()` no nos devuelve un primitivo , se intenta con toString().

¡atención aquí! ¡Cuando evaluamos un objeto envolvente en un contexto booleano como if, while , etc debemos desempaquetarlo nosotros mismos!

```javascript
let boolObj = new Boolean(false);

if (boolObj) {
    console.log("Condicion Verdadera"); // Condicion Verdadera
} else {
    console.log("Condicion Falsa");
}
```

podemos observar que aunque nuestro objeto booleano contenga el valor false, sigue siendo un objeto y para los contextos booleanos todo objeto pertenece al conjunto de valores truthy y esto nos puede llevar a resultados inesperados.

¡así que desempaquetémoslo nosotros mismo!

```javascript
let boolObj = new Boolean(false);

if (boolObj.valueOf()) {
    console.log("Condiciona verdadera");
} else {
    console.log("Ahora sí se evalúa correctamente"); // Ahora sí se evalúa correctamente
}
```

### Diferencia entre valueOf y toString en unboxing

| Método       | Propósito                              | Ejemplo                                |
| ------------ | -------------------------------------- | -------------------------------------- |
| `valueOf()`  | Devuelve el valor primitivo del objeto | `new Number(123).valueOf()` → `123`    |
| `toString()` | Devuelve una representación en cadena  | `new Number(123).toString()` → `"123"` |

## Interacción con Prototipos y Métodos Nativos

### Prototipo en JavaScript y su relación con el autoboxing

En el motor de JavaScript, todos nuestros objetos tienen un prototipo. Este prototipo es un objeto que actúa como plantilla para los ellos, proporcionando propiedades y métodos que pueden ser compartidos por todos nuestros objetos de este método.

**¿Que es un prototipo?**
El prototipo de nuestros objetos es simplemente otro objeto que contiene propiedades y métodos que pueden ser heredado por nuestro objeto original. Por ejemplo, cuando creamos un objeto String, ese objeto va a heredar las propiedades y métodos de String.prototype.

```javascript
let cadena = String("HOLA");
console.log(cadena.toLowerCase()); //"hola"
// accedemos al metodo toUpperCase del prototipo String.prototype.
```

**relación entre prototipos y autoboxing**
El autoboxing ocurre cuando uno de nuestros valores primitivos es tratado temporalmente como un objeto para que pueda acceder a métodos y propiedades de su prototipo heredado, el motor de JavaScript hace esto de manera implícita y no es visible para nosotros.

### Modificación de prototipos y sus efectos

tengamos Cuidado! porque JavaScript nos permite modificar los prototipos de los objetos envolventes (Number.prototype , String.Prototype , Boolean.Prototype , etc), Sin embargo, como los valores primitivos se convierten temporalmente en objetos a través del autoboxing, nuestros cambios en los prototipos pueden generar comportamientos impredecibles a nivel global.

```javascript
String.prototype.toLowerCase = function () {
    return "Algo diferente a lo esperado.";
};

let cadena = "Hola!";
console.log(cadena.toLowerCase()); //salida: "Algo diferente a lo esperado."
```

¡Es sumamente importante que conocer este concepto para evitar esto ya que, puede darnos un dolor de cabeza gigante!

## Buenas Prácticas

**Evitar autoboxing.**
No dependamos siempre del autoboxing para convertir nuestros primitivos a objetos implícitamente. Es mejor Realicemos conversiones explícitas usando new Number(), new String(), etc., cuando lo necesitemos.

**Usar operador de comparación estricta (===) siempre que podamos.**
Evitemos usar ==, en escenarios que no lo necesitemos es bueno ya que este realiza coerción implícita. ¡Usemos === para comparar de manera estricta y evitar resultados inesperados!

**Normalizar tipos antes de comparar**
Convirtamos explícitamente siempre que podamos los objetos a valores primitivos antes de compararlos. Por ejemplo, usemos valueOf() para convertir nuestros objetos Boolean a un valor primitivo.

**Prevenir efectos secundarios en segmentos criticos**
Evitemos depender de conversiones implícitas en segmentos críticos, ya que pueden generarnos efectos secundarios difíciles de rastrear.

## Efectos de Autoboxing en Rendimiento a gran escala

El autoboxing es una herramienta poderosa que nos provee el motor de JavaScript para la manipulación de nuestros datos primitivos, pero puede tener efectos significativos en el rendimiento en aplicaciones de gran escala, ciclos repetitivos o en infraestructuras antiguas de bajos recursos.

Al crear objetos envolventes explícitamente (como new String(), new Number(), new Boolean()) en lugar de confiar y desarrollar una buena lógica en nuestra estructura de código para poder confiar en el autoboxing puede ser menos eficiente en términos de uso de memoria y recursos.

Cuando usamos un objeto envolvente, este va a permanecer en la memoria hasta que el recolecto de basura del motor de JavaScript lo elimine. Este objeto va a ocupar más memoria que un valor primitivo porque contiene no solo el valor, sí no también propiedades y métodos adicionales que son parte del objeto.
En cambio el autoboxing se usa de manera temporal para realizar operaciones sobre un valor primitivo (como cuando invocamos el método .toUpperCase, .toString, etc).
El motor de JavaScript Crea internamente un objeto envolvente temporal solo durante la ejecución de esta operación, y una vez que la operación termina, el objeto es destruido liberando memoria rápidamente y no la retiene a largo plazo relativo.
