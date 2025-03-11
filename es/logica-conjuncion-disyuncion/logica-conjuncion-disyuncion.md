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
3. [Evaluación de Cortocircuito](#evaluación-de-cortocircuito)
    - [Cómo funciona el cortocircuito con `&&`](#cómo-funciona-el-cortocircuito-con-)
    - [Cómo funciona el cortocircuito con `||`](#cómo-funciona-el-cortocircuito-con-)
4. [Uso Avanzado y Manipulación](#uso-avanzado-y-manipulación)
    - [Uso de `&&` y `||` en asignaciones predeterminadas](#uso-de--y--en-asignaciones-predeterminadas)
    - [Doble negación (`!!`) y coerción explícita](#doble-negación--y-coerción-explícita)
    - [Operador lógico OR y nullish coalescing](#operador-lógico-or-y-nullish-coalescing)
    - [Uso de operadores lógicos en funciones y retorno de valores](#uso-de-operadores-lógicos-en-funciones-y-retorno-de-valores)
5. [Casos de Uso en la Práctica](#casos-de-uso-en-la-práctica)
    - [Validaciones de entrada de usuario](#validaciones-de-entrada-de-usuario)
    - [Condiciones en estructuras de control](#condiciones-en-estructuras-de-control)
    - [Filtrado y manipulación de arrays con AND y OR](#filtrado-y-manipulación-de-arrays-con-and-y-or)
    - [Optimización de código con operadores lógicos](#optimización-de-código-con-operadores-lógicos)
6. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Confusión entre `&&` y `||` en expresiones anidadas](#confusión-entre--y--en-expresiones-anidadas)
    - [Uso incorrecto de truthy y falsy en condiciones](#uso-incorrecto-de-truthy-y-falsy-en-condiciones)
    - [Manejo seguro de valores con operadores lógicos](#manejo-seguro-de-valores-con-operadores-lógicos)
7. [Comparación con Otros Lenguajes](#comparación-con-otros-lenguajes)
    - [Evaluación lógica en Python, Java y JavaScript](#evaluación-lógica-en-python-java-y-javascript)
    - [Diferencias de comportamiento en TypeScript](#diferencias-de-comportamiento-en-typescript)
8. [Conclusión y Recursos Adicionales](#conclusión-y-recursos-adicionales)
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

## Conceptos Fundamentales

### El operador `&&` (AND) en profundidad

El operador && (AND) en JavaScript es uno de los operadores lógicos más fundamentales. Lo utilizamos para evaluar dos o más condiciones booleanas y nos devolverá true solo cuando todas las condiciones de nuestra expresión sean true, si alguna de nuestras condiciones es false, el resultado será false. además, el operador && tiene la propiedad de evaluación por cortocircuito, una herramienta poderosa, esto significa que si la primera condición de nuestra expresión ya es false, no se evaluaran las siguientes condiciones por que el resultado de la expresión puede resolverse en ese mismo momento ya que la operación no puede ser true sin que todas las condiciones lo sean. Esta propiedad nos permitirá optimizar el rendimiento de nuestras aplicaciones ya que nos evita evaluaciones innecesarias. Este operador tiene una precedencia de nivel 5 y una asociatividad de derecha a izquierda.

Ejemplo con cortocircuito:

```javascript
function enviarMensaje() {
    console.Log("Mensaje enviado!.");
}

console.log(false && enviarMensaje());
```

cómo podemos observar, ¡nunca recibiremos el mensaje por consola ya que el operando con prioridad asociativa es false!

```javascript
function enviarMensaje() {
    console.Log("Mensaje enviado!.");
}

console.log(true && enviarMensaje());
```

aquí si veremos el mensaje por consola, ya que el operando izquierdo es true , permitiendo así que no se genere el cortocircuito y las evaluaciones sigan su curso.

**tabla de veracidad && (AND)**
aquí tenemos los comportamientos posibles en una operación binaria con el operador &&

| cuando A es | cuando B es | A && B devuelven |
| ----------- | ----------- | ---------------- |
| true        | true        | true             |
| true        | false       | false            |
| false       | true        | false            |
| false       | false       | false            |

### El operador `||` (OR) en profundidad

El operador || (OR) en JavaScript también es un operador lógico muy comúnmente usado, a diferencia de && , este operador lo usaremos para devolver true si al menos una de nuestras condiciones evaluadas es true. Solo nos devolverá false si todas nuestras condiciones son false. Al igual que el operador &&, el operador || también sigue el principio de evaluación de cortocircuito. Si nuestra primer condicional es true, el operador nos devolverá true inmediatamente sin evaluar el resto de nuestras condiciones restantes. ya que él sabe que la expresión completa será true. Este operador tiene una precedencia de nivel 4 y una asociatividad de derecha a izquierda.

```javascript
function enviarMensaje() {
    console.Log("Mensaje enviado!.");
}

console.log(false || enviarMensaje());
```

Observamos que el mensaje es enviado ya que el operador con prioridad asociativa es false, permitiendo así seguir verificando la expresión en búsqueda de un true.

```javascript
function enviarMensaje() {
    console.Log("Mensaje enviado!.");
}

console.log(true || enviarMensaje());
```

En este caso contrario, no recibiremos el mensaje ya que el operador || (OR) con el primer operando ya sabe que nuestro resultado será true.

**tabla de veracidad && (AND)**
aquí tenemos los comportamientos posibles en una operación binaria con el operador ||

| cuando A es | cuando B es | A \|\| B devuelven |
| ----------- | ----------- | ------------------ |
| false       | false       | false              |
| false       | true        | false              |
| true        | false       | false              |
| true        | true        | true               |

### Valores truthy y falsy en la evaluación lógica

El motor de JavaScript en relación con los operadores && y || no solo trabajan con valores booleanos explícitos (true o false), si no que también pueden operar con nuestros valores como pertenecientes al conjunto truthy o al conjunto falsy. un valor falsy es cualquier valor que se evaluara como false en un contexto booleano, mientras que un valor truthy será cualquier valor que se evalúe como true.

**Tabla de conjunto de valores falsy y truthy**
Esta tabla grafica muestra los conjuntos falsy y truthy con sus valores asociados.

| Valor                   | conjunto |
| ----------------------- | -------- |
| `false`                 | `falsy`  |
| `0`                     | `falsy`  |
| `-0`                    | `falsy`  |
| `0n` (BigInt)           | `falsy`  |
| `""` (cadena vacía)     | `falsy`  |
| `null`                  | `falsy`  |
| `undefined`             | `falsy`  |
| `NaN`                   | `falsy`  |
| `[]` (array vacío)      | `truthy` |
| `{}` (objeto vacío)     | `truthy` |
| `"0"` (cadena con cero) | `truthy` |
| `"hola!"` (cadena)      | `truthy` |

¡Veamos un ejemplo básico para entenderlo mejor!

```javascript
if ("Hola mundo!") {
    console.log("Esto es un valor de la categoria Truthy");
} else {
    console.log("Esto es un valor de la categoria Falsy");
}
```

En este caso la cadena "any text" es un valor que pertenece a la categoría Truthy por que no está vacía, y bajo coerción implícita, JavaScript lo transforma en true.

Pero... ¿qué sucede si evalúa una cadena que está vacía?

```javascript
if ("") {
    console.log("Esto es un valor de la categoria Truthy");
} else {
    console.log("Esto es un valor de la categoria Falsy");
}
```

## Evaluación de Cortocircuito

La evaluación de cortocircuito es una característica crucial en nuestros operadores lógicos && (AND) y || (OR). Esta evaluación nos permite que los operadores corten el proceso de evaluación tan pronto como se puede determinar el resultado final, optimizando el rendimiento y evitando la ejecución innecesaria de código.

### Cómo funciona el cortocircuito con && (AND)

Nuestros operadores && realizaran una evaluación de cortocircuito de izquierda a derecha. esto significa que si el primer operando es falso, no es necesario que nuestro segundo operando sea evaluado, porque para que una expresión con operador && de como resultado true, todos sus operandos deben ser verdaderos.

```javascript
let a = true;
let b = false;
let c = true;

function mensaje(mensaje, bool) {
    console.log(mensaje);
    return bool;
}

//prettier-ignore
console.log(mensaje("pos1", a) && mensaje("pos2", b) && mensaje("pos3", c))
/*
pos1  // perteneciente a mensaje("pos1", a) retorno : true
pos2  // perteneciente a mensaje("pos2", b) retorno : false
false // perteneciente al console.log() de mayor nivel al resolver la expresión por cortocircuito.
*/
```

cómo podemos observar `mensaje("pos3", c)` nunca es evaluado ya que el cortocircuito detecto que no tiene mayor sentido proseguir con la evaluación al momento de haber recibido el retorno false de `mensaje("pos2", b)`.

**Cómo funciona el cortocircuito con || (OR)**
En el caso de nuestros operadores ||, el cortocircuito se activa si el primer operando es verdadero, ya que no es necesario que evalúen el nuestro segundo operando ya que una expresión OR siempre será true si al menos uno de nuestros operandos es verdadero.

```javascript
let a = false;
let b = true;
let c = true;

function mensaje(mensaje, bool) {
    console.log(mensaje);
    return bool;
}

//prettier-ignore
console.log(mensaje("pos1", a) || mensaje("pos2", b) || mensaje("pos3", c))
/*
pos1  // perteneciente a mensaje("pos1", a) retorno : false
pos2  // perteneciente a mensaje("pos2", b) retorno : true
false // perteneciente al console.log() de mayor nivel al resolver la expresión por cortocircuito.
*/
```

aquí podemos observar que `mensaje("pos3", c)` nunca es evaluado ya que el cortocircuito determino que no tiene mayor sentido proseguir con la evaluación al momento de haber recibido el retorno true de `mensaje("pos2", b)`.

## Uso Avanzado y Manipulación

Los operadores && (AND) y || (OR) en JavaScript no solo los podemos utilizar para evaluar nuestras condiciones, si no también podemos emplearlos en asignaciones, conversiones de valores y optimización de código. ¡Veamos cómo aprovechar estas características!.

### Uso de && y || en asignaciones predeterminadas

Podemos usar || (OR) para establecer valores predeterminados en caso de que el operando izquierdo pertenezca al conjunto de valores falsy, por contrario podemos usar && (AND) en los casos donde queramos dar un valor predeterminado cuando el operando izquierdo pertenece al conjunto de valores truthy.

Veamos unos ejemplos con ambos operadores.

```javascript
let usuario = null;
let nombre = usuario || "Invitado";
console.log(`Bienvenido ${nombre}!`); // bienvenido Invitado
```

```javascript
let usuario = null;
let nombre = usuario || "Invitado";
console.log(`Bienvenido ${nombre}!`); // bienvenido Invitado
```

ya que usuario es pertenece al conjunto de valores falsy , el operador OR asignara el operando derecho.

```javascript
let usuario = { nombre: "Mauro" };
usuario && console.log(`Hola ${usuario.nombre}!`);
```

como usuario es un objeto el cual pertenece al conjunto de valores truthy, el operador && evaluara el operando derecho.

### Doble negación (!!) y coerción explícita

El operador !! (doble negación) se utiliza cuando necesitamos convertir un valor en su equivalente booleano de manera explícita. La primera negación (!) convierte el valor a su opuesto en el contexto booleano mediante coerción implícita. La segunda negación (!) revierte esta inversión, obteniendo así el valor booleano correspondiente del original.

```javascript
console.log(!!"Texto"); // true (una cadena no vacía es truthy)
console.log(!!0); // false (0 es falsy)
console.log(!!null); // false (null es falsy)
console.log(!![]); // true (un array vacío es truthy)
```

### Operador lógico OR y nullish coalescing

El operador ?? (Nullish Coalescing) es similar a ||, pero con una diferencia clave, y es que solo considera null y undefined(valores nullish) como valores falsy, mientras que || también considera 0, false y "" (cadena vacía).

comparemos a ambos con un ejemplo práctico:

```javascript
let valor = 0 || "valor por defecto";
console.log(valor); // "valor por defecto", porque 0 pertenece al conjunto falsy para el operador ||
```

```javascript
let valor = 0 ?? "valor por defecto";
console.log(valor); // 0, por que ?? solo evalúa valores nullish como tipo false.
```

### Uso de operadores lógicos en funciones y retorno de valores

Podemos utilizar los operadores lógicos en nuestras funciones para simplificar nuestro flujo de ejecución, retornando valores condicionales sin necesidad de utilizar estructuras if.

```javascript
function obtenerMensaje(mostrar) {
    return mostrar && "Hola Mundo!";
}

console.log(obtenerMensaje(true)); // "Hola Mundo!"
console.log(obtenerMensaje(false)); // false
```

```javascript
function obtenerNombre(usuario) {
    return usuario.nombre || "Desconocido";
}

console.log(obtenerNombre({ nombre: "Mauro" })); // "Mauro"
console.log(obtenerNombre({})); // "Desconocido"
```
