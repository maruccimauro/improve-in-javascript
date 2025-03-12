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
5. [Escape y Seguridad en Interpolación](#escape-y-seguridad-en-interpolación)
    - [Escape de caracteres en template literals](#escape-de-caracteres-en-template-literals)
    - [Manejo de inyección de código malicioso (XSS)](#manejo-de-inyección-de-código-malicioso-xss)
6. [Casos de Uso y Aplicaciones Prácticas](#casos-de-uso-y-aplicaciones-prácticas)
    - [Generación dinámica de HTML con template literals](#generación-dinámica-de-html-con-template-literals)
    - [Generación de consultas SQL](#generación-de-consultas-sql-y-json-dinámicos)
7. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Errores Comunes que debemos evitar](#Errores-Comunes-que-debemos-evitar)
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

En este ejemplo nuestra función obtenerUsuario es llamada desde dentro de la interpolación y su resultado se incluye en la construcción del string de salida, esto nos permite hacer lo que queramos antes de devolver un resultado a la cadena.

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

## Funciones de Plantilla (Tagged Templates)

### ¿Qué son los tagged templates?

Los tagged templates son una característica avanzada de los templates literals en JavaScript. Nos permiten "etiquetar" un template literal con una función que puede procesar los contenidos del literal antes de que nos devuelvan el resultado final. básicamente, un tagged template permite manipular o transformar el resultado de un tempate literal de manera personalizada por nosotros.

la sintaxis basica de un tagged template es:

```javascript
tagFunction`string template ${expresion}`;
```

donde seccionándolo podremos identificar que, tagFunction es el nombre de la función que recibirá el template literal. , string template es la cadena de texto entre los backticks y ${expresion} es una o más expresiones que se interpolan dentro del template literal.

```javascript
function saludo(literal, nombre, apellido) {
    //prettier-ignore
    return `${literal[0]}${nombre.toUpperCase()} ${apellido.toUpperCase()}${literal[2]}`;
}

let mensaje = saludo`Hola, ${"Mauro"} ${"Marucci"}!`;
console.log(mensaje); // "Hola, MAURO MARUCCI!"
```

en el ejemplo que vemos arriba vemos como la función saludo transforma el nombre a mayúscula y podemos dos partes importantes:
**literal:** es una array de las partes estáticas del template como `["Hola ", " ", "!"]`, este argumento es pasado automáticamente por el motor de JavaScript a la función `saludo`.
**nombre** es la expresion interpolada `"Mauro"`.
**apellido** es la expresion interpolada `"Marucci"`

también podemos usar el concepto de `rest parameter` para obtener los argumentos que fueron pasados después de `literal` en un solo array (¡son aquellos que interpolamos!).

```javascript
function saludo(literal, ...valores) {
    //prettier-ignore
    return `${literal[0]}${valores[0].toUpperCase()} ${valores[1].toUpperCase()}${literal[2]}`;
}

let mensaje = saludo`Hola, ${"Mauro"} ${"Marucci"}!`;
console.log(mensaje); // "Hola, MAURO MARUCCI!"
```

### Creación de funciones personalizadas de interpolación

Nuestras funciones personalizadas de interpolación (tagged functions) las podremos crear de manera que tengamos la capacidad de manipular tanto las partes literales como las expresiones dentro del template literal. Cuando usamos un tagged template, la función que elijamos recibe al menos dos parámetros:

**literal**: Un array que contiene las partes fijas del template (es decir, las partes del string que no contienen ninguna interpolación).
**valores**: Una lista de todas las expresiones que están dentro de ${}.

Con estos dos parámetros, podemos hacer lo que deseemos con los valores, como transformarlos, combinarlos, hacer cálculos, etc.
Por ejemplo:

```javascript
function formatear(literal, ...valores) {
    let resultado = literal[0].toLowerCase();
    for (let i = 0; i < valores.length; i++) {
        resultado += valores[i].toUpperCase(); // Convierte las expresiones a mayúsculas
        resultado += literal[i + 1].toLowerCase(); //convierte los literales a minuscula
    }
    return resultado;
}

let nombre = "Mauro";
let mensaje = formatear`Hola, ${nombre}, ¿cómo estás?`;
console.log(mensaje); // "hola, MAURO, ¿cómo estás?"
```

aquí, nuestra función formatear recibe tanto las partes literales como las expresiones y transforma todas las expresiones a mayúscula y los literales a minúscula antes de combinarlos. La ventaja de que usemos tagged template es que podemos aplicar una lógica personalizada en cada interpolación y literal por separado.

## Escape y Seguridad en Interpolación

Cuando trabajamos con template literals y realizamos interpolación de valores, es esencial tener en cuenta la seguridad de la aplicación. especialmente cuando se manipulan entradas de usuarios o datos que puedan ser interpretados de manera no deseada. Esto incluye protegerse contra ataques como la inyección de codigo o Cross-Site Scripting (XSS).
Es importante ver cómo escapar caracteres, prevenir vulnerabilidades y garantizar que la interpolacion se realice de manera seguro en la estructura de nuestro codigo.

### Escape de caracteres en template literals

Cuando hablamos de escape de caracteres hacemos referencia al proceso de convertir ciertos caracteres especiales en su representación segura para que evitemos que se interpreten de manera incorrecta o peligrosa. En el Motor de JavaScript, algunos caracteres tienen significado especial dentro de cadenas de texto o expresiones, como el caracter de comillas (" y '), la barra invertida (\\) entre otros.
Cuando interpolamos variables dentro de template literals, nos exponemos a estos casos , los valores insertados podrían contener caracteres peligrosos si no se escapan correctamente. Estos es especialmnete relevante en contextos donde los datos podrian incluir codigo HTML, SQL, o cualquier otro lenguaje susceptible de ejecución.

veamos un ejemplo simple de como puede afectarnos !:

ingresa este segmento de texto en ambos input `<div style="background-color: red; color: white">ATAQUE XSS</div>` para asi poder evaluar los resultados

```javascript
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Demostración de Ataque XSS</title>
    </head>
    <body>
        <h2>Ejemplo de vulnerabilidad XSS</h2>
        <hr />
        <h3>Comentario sin proteccion:</h3>
        <input style="width: 400px" type="text" id="inputBox1" />
        <button onclick="procesarComentario(1)">sin escape</button>
        <div id="salida1"></div>
        <hr />

        <h3>Comentario con proteccion</h3>
        <input style="width: 400px" type="text" id="inputBox2" />
        <button onclick="procesarComentario(2)">con escape</button>
        <div id="salida2"></div>
        <hr />

        <script>
            function escaparHTML(str) {
                return str.replace(/[&<>"']/g, (match) => {
                    const escapeMap = {
                        "&": "&amp;",
                        "<": "&lt;",
                        ">": "&gt;",
                        '"': "&quot;",
                        "'": "&#39;",
                    };
                    return escapeMap[match];
                });
            }

            function procesarComentario(id) {
                let comentario = document.getElementById(`inputBox${id}`).value;
                if (id === 2) {
                    comentario = escaparHTML(comentario);
                }
                let mensajeHTML = `<p>${comentario}</p>`;
                document.getElementById(`salida${id}`).innerHTML += mensajeHTML;
            }
        </script>
    </body>
</html>

```

En en ejemplo de arriba vemos como al no reemplazar los caracteres especiales (aquellos que tienen insidencia de ser interpretados) antes de ser insertados al DOM podemos incurrir en el error de modificar la estructura de nuestro sitio web de una manera que no queremos, esto tambien puede suceder con ejecucion de codigo javascript , consultas SQL en las bases de datos, y demas contextos que permitan que la cadena evaluada pueda ser interpetrada.

## Manejo de inyección de código malicioso (XSS)

El XXS (Cross-Site Scripting) es una de las vulnerabilidades de seguridad potencialmente mas comunes en nuestras aplicaciones web. Se produce cuando un atacante inserta codigo Javascript malicioso en una pagina web que luegeo es ejecutada en el navegador de otro usuario.
un ejemplo ejemplo tipico es cuando el atacante envia un comentario o una cadena de texto atravéz de un formulario, que luego se muestra en nuestra pagina sin validación o escape adecuado. Si el contenido del comentario contiene etiquetas del tipo \<script\> \</script\>, el codigo malicioso se ejecuta en el navegador de los usuarios que visiten la pagina.
Una forma comun de prevenir xss es escapar cualquier dato de entrada del usuario antes de que lo insertemos en HTML. Ya vemos un ejemplo anterior de como podemos escapar los caracteres peligrosos en el caso de comentarios, pero esto es aplicable a cualquier entrada que provenga de un usuario o una fuente externa no confiable.
Cuando manipulemos HTML con JavaScript y no confiemos en el contenido que se está insertando, podemos usar las API del navegador como textContent en lugar de innerHTML, ya que textContent automáticamente nos va a prevenir de la ejecucion de cualquier codigo HTML o JavaScript.
En el ejemplo anterior el texto

```javascript
document.getElementById(`salida${id}`).innerHTML;
```

reemplazalo por

```javascript
document.getElementById(`salida${id}`).textContent`
```

y mira los resultados.

## Casos de Uso y Aplicaciones Prácticas

Los template literals en JavaScript tienen múltiples aplicaciones prácticas para ofrecernos que nos ayudaran a simplificar las tareas que, de otro modo, nos requerirían más código y mayor complejidad. Desde la creación de HTML dinámico hasta la manipulación de consultas SQL, su uso nos resultara muy útil en una amplia variedad de escenarios. ¡veamos como podemos aprovecharlo al máximo!

### Generación dinámica de HTML con template literals

Muchas veces necesitamos insertar o modificar contenido HTML de manera dinámica sin tener que manipular el DOM manualmente a través de métodos como `document.createElement` o `appendChild`. Los templates literals nos facilitaran la creación de bloques HTML de forma más legibles y comprensible, evitando la necesidad de concatenaciones largas.

```javascript
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Demostración de Ataque XSS</title>
    </head>
    <body>
        <div id="listaProductos"></div>

        <script>
            const productos = [
                { nombre: "Camiseta", precio: 20 },
                { nombre: "Pantalones", precio: 30 },
                { nombre: "Zapatos", precio: 50 },
            ];

            const lista = productos
                .map((producto) => {
                    return `
                <div class="producto">
                    <h2>Nombre : ${producto.nombre}.</h2>
                    <p>Precio : $${producto.precio}.</p>
                </div>
                `;
                })
                .join("");

            document.getElementById("listaProductos").innerHTML = lista;
        </script>
    </body>
</html>
```

En este ejemplo utilizamos un template literals para crear un bloque de HTML que describe los productos de nuestra lista, con `map()` generamos una lista deonde recorremos todos los elementos y unimos el resultado de las cadenas generadas con `.join()`, finalmente por medio de .innerHTML insertamos el contenido a nuestro DOM en el elemento con id listaProductos, esto nos permitió generar nuestro objetivo de una manera eficiente , limpia y fácil de leer.

### Generación de consultas SQL

Los template literals nos son también muy útiles cuando necesitamos generar consultas SQL o estructuras JSON dinámicamente, especialmente cuando los valores que insertaremos en esas consultas provienen de entradas del usuario, de una base de datos o de algún otro origen de datos.

```javascript
const nombre = "Mauro";
const direccion = "Mihogar 123";
const query = `
    SELECT * FROM usuarios
    WHERE nombre = '${nombre}'
    AND direccion = '${direccion}'
`;

console.log(query);
```

aquí generamos una consulta SQL que busca un registro cuyo nombre es Mauro y su dirección es Mihogar 123.
¡Recuerda que es necesario escapar siempre los caracteres especiales que puedan ser interpretados en contextos no deseados, te recomiendo profundizar en la inyección SQL para utilizar técnicas de protección para estas situaciones!

## Errores Comunes y Buenas Prácticas

Aunque los tamplate literals son muy buenas herramientas, su uso indebido puede llevar a errores y malas prácticas.

### Errores Comunes que debemos evitar

**Errores al olvidar los backticks**
Olvidarnos de usarlos backticks , aunque parezca mentira , muchas veces no nos percatamos que los necesitamos, por eso es bueno que analicemos siempre su uso antes de comenzar a trabajar con una cadena compleja.

**Mal uso de interpolación con `null` y `undefined`**
Otro error común que podríamos cometer es no manejar adecuadamente los valores nullish (null y undefined) en las interpolaciones, ya que el motor de JavaScript convierte estos valores en cadenas vacías (""), lo que nos puede llevar a casos que realmente no esperábamos con salidas confusas y errores lógicos en nuestra aplicación.

```javascript
const nombre = null;
const edad = undefined;

const mensaje = `Mi nombre es ${nombre} y tengo ${edad} años.`;
console.log(mensaje); // "Mi nombre es  y tengo  años."
```

para evitar esto debemos usar el operador logico OR (||) o el operador de coalescencia nula (??).

```javascript
const nombre = null;
const edad = undefined;

const mensaje = `Mi nombre es ${nombre || "Desconocido"} y tengo ${
    edad ?? "desconocida"
} años.`;
console.log(mensaje); // "Mi nombre es Desconocido y tengo desconocida años."
```

**Abusar de las comillas**
otras veces intentamos colocar ya sea por costumbre o cual fuese el motivo template literals donde no son necesarias.

```javascript
const nombre = "Mauro";
const edad = 34;

const personaJSON = JSON.stringify({
    nombre: `${nombre}`,
    edad: `${edad}`,
});

console.log(personaJSON);
// salida {"nombre":"Mauro","edad":"34"}
```

### Mejores prácticas para escribir código más limpio

**Usa template literals para la interpolación de variables**
Siempre que necesitemos insertar valores dinámicos dentro de una cadena, es importante usar template literals.

Es preferible esto:

```javascript
const mensaje = `Mi nombre es ${nombre} y tengo ${edad} años.`;
console.log(mensaje);
```

a esto:

```javascript
const mensaje = "Mi nombre es " + nombre + " y tengo " + edad + " años.";
console.log(mensaje);
```

**Evita interpolaciones complejas dentro de los template literals:**
Si bien las template literals nos permiten realizar operaciones complejas dentro de las interpolaciones, en muchos casos es importante generar los calculo fuera del template e incorporar los resultados directamente para así quede más limpio y sea más fácil el mantenimiento del código.
Es preferible mantener la simpleza dentro del template literals

```javascript
const precio = 100;
const descuento = 0.2;
const precioFinal = precio - precio * descuento;

const mensaje = `El precio final con descuento es $${precioFinal}.`;
console.log(mensaje);
```

en vezde de mantener la complejidad dentro del template literals

```javascript
const mensaje = `El precio final con descuento es $${precio - precio * 0.2}.`;
console.log(mensaje);`
```

imaginemos un template de mayor tamaño y cálculos más complejos...

**Utiliza template literals para múltiples líneas**
los template literals son ideales cuando necesitamos cadenas de texto que ocupan varias líneas. No solo es más limpio, sino que evitamos la necesidad de concatenar múltiples cadenas o usar saltos de línea manualmente.

```javascript
const mensaje = `
  Hola ${nombre},
  Te informamos que tu solicitud ha sido procesada con éxito.
  Muchas gracias por tu confianza.
`;
console.log(mensaje);
```

**Limpia los datos cuando uses datos externos:**
Si usamos datos que provienen de entradas de usuario o fuentes externas ¡siempre asegurémonos de limpiar esos datos antes de insertarlos en un template literal!
