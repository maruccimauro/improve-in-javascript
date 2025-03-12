# Manipulación de lógica de interpolacion de cadenas backticks

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
    - [¿Qué es la interpolación de cadenas?](#qué-es-la-interpolación-de-cadenas)
    - [Ventajas sobre la concatenación tradicional](#ventajas-sobre-la-concatenación-tradicional)
    - [Casos de uso comunes](#casos-de-uso-comunes)
2. [Fundamentos de los Template Literals](#fundamentos-de-los-template-literals)
    - [Expresiones dentro de signos de interpolacion](#expresiones-dentro-de-signos-de-interpolacion)
    - [Manejo de saltos de línea y formato](#manejo-de-saltos-de-línea-y-formato)
3. [Manipulación Avanzada con Template Literals](#manipulación-avanzada-con-template-literals)
    - [Interpolación con condicionales ternarios](#interpolación-con-condicionales-ternarios)
    - [Uso de funciones dentro de template literals](#uso-de-funciones-dentro-de-template-literals)
    - [Interpolación con arrays y objetos](#interpolación-con-arrays-y-objetos)
4. [Funciones de Plantilla (Tagged Templates)](#funciones-de-plantilla-tagged-templates)
    - [¿Qué son los tagged templates?](#qué-son-los-tagged-templates)
    - [Creación de funciones personalizadas de interpolación](#creación-de-funciones-personalizadas-de-interpolación)
    - [Ejemplo práctico de un tagged template](#ejemplo-práctico-de-un-tagged-template)
5. [Escape y Seguridad en Interpolación](#escape-y-seguridad-en-interpolación)
    - [Escape de caracteres en template literals](#escape-de-caracteres-en-template-literals)
    - [Manejo de inyección de código malicioso (XSS)](#manejo-de-inyección-de-código-malicioso-xss)
    - [Interpolación segura en aplicaciones web](#interpolación-segura-en-aplicaciones-web)
6. [Casos de Uso y Aplicaciones Prácticas](#casos-de-uso-y-aplicaciones-prácticas)
    - [Generación dinámica de HTML con template literals](#generación-dinámica-de-html-con-template-literals)
    - [Uso en internacionalización y localización](#uso-en-internacionalización-y-localización)
    - [Generación de consultas SQL y JSON dinámicos](#generación-de-consultas-sql-y-json-dinámicos)
7. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Errores al olvidar los backticks](#errores-al-olvidar-los-backticks)
    - [Mal uso de interpolación con `null` y `undefined`](#mal-uso-de-interpolación-con-null-y-undefined)
    - [Mejores prácticas para escribir código más limpio](#mejores-prácticas-para-escribir-código-más-limpio)
8. [Comparación con Otros Métodos de Concatenación](#comparación-con-otros-métodos-de-concatenación)
    - [Diferencias con `+` y `concat()`](#diferencias-con-y-concat)
    - [Compatibilidad con versiones antiguas de JavaScript](#compatibilidad-con-versiones-antiguas-de-javascript)
    - [Uso en TypeScript y otros lenguajes](#uso-en-typescript-y-otros-lenguajes)
9. [Conclusión y Recursos Adicionales](#conclusión-y-recursos-adicionales)
    - [Resumen de los conceptos clave](#resumen-de-los-conceptos-clave)
    - [Ejercicios y desafíos prácticos](#ejercicios-y-desafíos-prácticos)
    - [Enlaces y documentación recomendada](#enlaces-y-documentación-recomendada)

---

## Introducción

La interpolación de cadenas es una característica clave en muchos lenguajes de programación que no permite construir cadenas de texto de manera más legible y eficiente en comparación con la concatenación tradicional. El motor de JavaScript, implementa esta funcionalidad mediante los **template literals (literales de plantilla)**, introducidos en ES6.

### ¿Qué es la interpolación de cadenas?

La interpolación de cadenas es el proceso de insertar nuestras variables y expresiones dentro de una cadena de texto sin necesidad de concatenarlas manualmente con métodos tradicionales. Esto lo lograremos utilizando los template literals, los cuales emplean **backtick (\`\`)** en lugar de comillas simples (' ') o dobles (" ").

¡Veamos un ejemplo!

```javascript
const nombre = "Mauro";
const edad = 34;
console.log(`¡Hola, mi nombre es ${nombre} y tengo ${edad} años!`);
//la salida sera "¡Hola, mi nombre es Mauro y tengo 34 años!""
```

Aqui tanto la constante nombre como la constante edad la hemos concatenado directamente en la cadena sin necesidad de usar el operador + ni el metodo .concat().

## Ventajas sobre la concatenación tradicional

Antes del ECMAScript 6, la forma en la que construyamos cadenas dinámicas en JavaScript era mediane la concatenación con el operador +. Pero esta técnica puede volver poco legible y propenso a errores nuestro código cuando trabajamos con múltiples variables o expresiones.

**Mayor legibilidad:** Evitamos el uso excesivo del operador +, haciendo que nuestro código sea más claro y fácil de entender.
**Menos errores de sintaxis:** Al no depender de la concatenación manual, reducimos nuestros posibles errores al manejar espacios y comillas repetidamente.
**Compatibilidad con expresiones:** ¡podemos incluir operaciones matemáticas, llamadas a funciones y más dentro de la interpolación!
**Soporte para saltos de línea:** Permite que escribamos cadenas de múltiples líneas sin necesidad de hacer un salto de línea manualmente con \n.

## Casos de uso comunes

La interpolación de cadenas nos será útil en una amplia variedad de escenarios, algunos incluyen:
Con mensajes dinámicos en nuestra UI:

```javascript
const usuario = "María";
console.log(`Bienvenida, ${usuario}!`);
```

Cuando queramos generar HTML dinámico:

```javascript
const producto = "Laptop";
const precio = 1200;
const html = `<h1>Producto: ${producto}</h1><p>Precio: $${precio}</p>`;
```

Al trabajar con plantillas de correos electrónicos o mensajes:

```javascript
function generarMensaje(nombre, pedido) {
    return `Hola ${nombre}, tu pedido ${pedido} está en camino.`;
}
console.log(generarMensaje("Luis", "#12345"));
```

Consultas SQL dinámicas:

```javascript
const id = 42;
const query = `SELECT * FROM usuarios WHERE id = ${id};`;
console.log(query);
// Salida: SELECT * FROM usuarios WHERE id = 42;
```

Estos son solo algunos ejemplos de cómo en nuestro dia a dia la interpolación de cadenas puede hacer que nuestro código sea más limpio y eficiente.

## Fundamentos de los Template Literals

Los Template Literals (también llamados Template Strings) son una característica introducida en ES6 (ECMAScript 2015) que nos brindan una forma más flexible y legible de manejar nuestras cadenas de texto. Se diferencian por no usar las comillas simples (') y dobles (") en cambio usan backticks (acento grave, `), lo que nos permite interpolar variables, expresiones, saltos de línea y más.

### Expresiones dentro de signos de interpolación

La interpolación de expresiones en nuestros template literals lo realizaremos utilizando la sintaxis **${expresion}**, lo que nos permite incluir variables, operaciones matemáticas, llamadas a funciones, acceder a objetos y mas , sin necesidad de concatenar con el operador + ni el metodo .concat().
Ya iremos profundizando más en el tema a medida que avancemos.

### Manejo de saltos de línea y formato

Una de las características más útiles que nos brindan los témplate literals es la posibilidad de escribir cadenas de varias líneas sin necesidad de usar \n ni concatenaciones.

Ejemplo sin Template Literals (concatenación tradicional)

```javascript
const mensaje =
    "Esta es una linea\n" +
    "Esta es otra linea\n" +
    "Y esta es la ultima linea.";

console.log(mensaje);
/* salida :
Esta es una linea
Esta es otra linea
Y esta es la ultima linea.
*/
```

Pero podríamos hacer lo mismo más simple, legible y ordenado.

```javascript
const mensaje = `Esta es una linea
Esta es otra linea
Y esta es la ultima linea.`;

console.log(mensaje);
/* salida :
Esta es una linea
Esta es otra linea
Y esta es la ultima linea.
*/
```

## Manipulación Avanzada con Template Literals

### Interpolación con condicionales ternarios

Una de las características más poderosas que nos proveerán los template literals es la posibilidad de incluir condicionales dentro de ellos. El condicional ternario en JavaScript tiene la forma: `condición ? valor_si_true : valor_si_false`, sabiendo esto, podemos utilizarlo directamente dentro de nuestra interpolación para evaluar expresiones y elegir entre diferentes valores.
Veamos un ejemplo para poder visibilizarlo mejor.

```javascript
let edad = 20;
console.log(`la persona es ${edad < 18 ? "menor" : "mayor"} de edad.`);
//salida "la persona es mayor de edad."
```

Como observamos en este ejemplo la condición `edad < 18` se evalúa dentro de nuestra interpolación ${} y dependiendo del resultado booleano devuelto , se elegirá entre uno de los dos valores "menor" y "mayor."

function obtenerSaludo(nombre) {
return `¡Hola, ${nombre}!`;
}

let nombre = "Carlos";
let mensaje = `El saludo es: ${obtenerSaludo(nombre)}`;
console.log(mensaje); // "El saludo es: ¡Hola, Carlos!"

### Uso de Funciones Dentro de Template Literals

Otra característica avanzada que nos proveen los template literals es la de poder ejecutar funciones dentro de nuestras interpolaciones. Esto permite que realicemos llamadas a funcione complejas directamente dentro de la construcción del string.
Ejemplo:

```javascript
function obtenerUsuario() {
    return "Mauro";
}

console.log(`Bienvenido ${obtenerUsuario()}!`);
// salida Bienvenido Mauro!
```

En este ejemplo la nuestra función obtenerUsuario es llamada desde dentro de la interpolación y su resultado se incluye en la construcción del string de salida, esto nos permite hacer lo que queramos antes de devolver un resultado a la cadena.

### Interpolación con Arrays y Objetos

Los templates literals también nos permitirán realizar interpolaciones con arrays y objetos, lo cual es muy útil cuando necesitamos representar de manera legible datos complejos dentro de nuestra cadena.
Veámoslo con un ejemplo.

```javascript
let frutas = ["manzana", "pera", "uva", "naranja"];

//prettier-ignore
console.log(`descuento en las siguientes frutas de nuestro almacen : ${frutas.join(", ")}.`);
//salida "descuento en las siguientes frutas de nuestro almacen : manzana, pera, uva, naranja."
```

¡En este caso no solo usamos un array completo, sino que también su método .join() para crear nuestra lista de descuentos desde el segmento de interpolación!

Cuando trabajamos con objetos, podemos acceder a sus propiedades desde dentro de la interpolación ${}:

```javascript
let persona = {
    nombre: "Mauro",
    edad: 34,
};

let mensaje = `Mi nombre es ${persona.nombre} y tengo ${persona.edad} años.`;
console.log(mensaje); // "Mi nombre es Mauro y tengo 34 años."
```
