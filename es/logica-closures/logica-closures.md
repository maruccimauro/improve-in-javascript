# Manipulación de Lógica clausuras en JavaScript

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
    - [¿Qué es un closure?](#qué-es-un-closure)
    - [Importancia de los closures en JavaScript](#importancia-de-los-closures-en-javascript)
2. [Ámbito y Alcance de Variables](#ámbito-y-alcance-de-variables)
    - [Ámbito léxico](#ámbito-léxico)
    - [Diferencia entre ámbito local y global](#diferencia-entre-ámbito-local-y-global)

---

## Introducción

Las clausuras nos permitirán que nuestras funciones accedan a variable de su ámbito externo incluso después de que dicho ámbito haya finalizado su ejecución. Esto nos permitirá trabajar con encapsulamiento, gestión de estado y optimización.

### Qué es un closure

los closures en JavaScript son funciones que "recuerdan" el ámbito en el que fueron creadas, incluso si se ejecutan en otros contextos. Es decir, un closure es una función que cierra sobre su ámbito léxico, permitiendo acceder a variables externas aun cuando la ejecución de la función exterior haya finalizado.

Veamos un ejemplo!

```javascript
function generarContador() {
    let conteo = 0;

    return () => {
        return ++conteo;
    };
}

let contador = generarContador();
console.log(contador()); // salida 0
console.log(contador()); // salida 1
```

Aquí vemos como la función anónima sigue teniendo acceso a `conteo` después de que la función `generarContador` haya finalizado su ejecución, es decir que contador al llamar a la función anónima aumentara a `conteo` quien pertenece a su ámbito léxico manteniendo su estado entre llamadas.

### Importancia de los closures en JavaScript

Los closures nos será una herramienta sumamente beneficiosa en el motor de JavaScript porque nos permitirán:

**Encapsulación de datos y privacidad:**
-Al no exponer nuestras variables directamente, los closures nos permitirán la creación de datos privados dentro de la función.
-Esto nos será útil para evitar accesos indeseados y evitar modificaciones accidentales sobre nuestras variables.

```javascript
function usuario(nombre) {
    const clave = "magica123";

    return {
        obtenerNombre: function () {
            return nombre;
        },
        verificarClave: function (claveIngresada) {
            return clave === claveIngresada;
        },
    };
}
const usuario1 = usuario("Mauro");

console.log(usuario1.obtenerNombre()); // salida Mauro
console.log(usuario1.verificarClave("magica123")); // salida true
console.log(usuario1.clave); // salida undefined
```

**Manejo de estado:**
Nos permiten conservas datos sin necesidad de usar variables globales, lo cual es útil para contadores, caches y funciones que manejan configuraciones.

```javascript
function acumulador(valorInicial) {
    let total = valorInicial;

    return (valorIncremental) => {
        total += valorIncremental;
        return total;
    };
}

let agregar = acumulador(100);
console.log(agregar(20)); // salida 120
console.log(agregar(10)); // salida 130
```

**Callbacks y gestion de eventos**
Los closures permiten que nuestras funciones recuerden valores previos, lo cual es indispensable para que trabajemos con event listeners y callbacks en JavaScript.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body>
        <button id="boton">Evaluar</button>
        <script>
            function enviarMensaje(mensaje) {
                return () => {
                    console.log(mensaje);
                };
            }

            document
                .getElementById("boton")
                .addEventListener("click", enviarMensaje("Hola Mauro!"));
        </script>
    </body>
</html>
```

**Funciones fabrica (function factory):**

las function factory son nuestras funciones que retornan otras funciones con configuraciones predeterminadas mediante los closures.

```javascript
function multiplicador(a) {
    return (b) => {
        return a * b;
    };
}

const multiplicarX5 = multiplicador(5);
const multiplicarX10 = multiplicador(10);

console.log(multiplicarX5(8)); // salida 40
console.log(multiplicadorX10(8)); // salida 80
```

**Optimización de código y modularidad.**
Los closures nos permiten escribir código más modular y reutilizable sin depender de variables globales.

```javascript
function generarContador(valorInicial) {
    let total = valorInicial;

    return {
        incrementar: function () {
            return ++total;
        },
        decrementar: function () {
            return --total;
        },
        actual: function () {
            return total;
        },
    };
}

const contador = generarContador(100);
console.log(contador.actual()); // salida 100
console.log(contador.incrementar()); // salida 101
console.log(contador.decrementar()); // salida 100
```

## Ámbito y Alcance de Variables

El ámbito (scope) en el motor de JavaScript se refiere a la accesibilidad y visibilidad de las variables dentro del código en función de su ubicación. esto es esencial para que podamos comprender como los closures y las funciones interactúan con las variables.

### Ámbito léxico

el ámbito léxico en JavaScript se refiere a la forma en la que nuestras funciones se asocian con su entorno de ejecución en el momento de su definición, no cuando se ejecutan. El lugar donde definimos nuestra función en el código determina el acceso que tiene a las variables externas.
poniéndolo en otras palabras, podemos decir que el ámbito léxico significa que las funciones recuerdan el entorno(o las variables) en el cual fueron creadas, independientemente de donde o cómo se ejecuten.
Este será un concepto clave para nosotros ya que nos permite comprender que las funciones internas (closures) tienen acceso a las variables de sus funciones externas gracias a este vínculo léxico.
Veamos un claro ejemplo :

```javascript
function padre() {
    const mensaje = "mensaje de variable perteneciente a padre";

    function hijo() {
        console.log(mensaje);
    }

    hijo();
}

padre();
```

En este ejemplo, vemos como la función `hijo()` puede acceder a ala variable mensaje de su función contenedora padre(), a pesar de que hijo() se ejecuta dentro de padre(). Esto es posible debido a que el motor de JavaScript usa el ámbito léxico para determinar que `hijo()` tiene acceso a las variables definidas en su entorno de creación, no en su contexto de ejecución.

### Diferencia entre ámbito local y global

los ámbitos los podemos definir en local y global , esto afecta como y donde podemos acceder a nuestras variables.

**Ámbito global**
Las variables definidas en el ámbito global son accesibles desde cualquier parte del código, ya sea dentro de una función o fuera de ella. cuando declaramos una variable fuera de cualquier función, esta pertenece al ámbito global.

```javaScript
let variableGlobal= "Mauro";

function mostrarGlobal(){
  console.log(variableGlobal);
}

mostrarGlobal()
```

En este caso, nuestra variable `varaibleGlobal` está definida en el ámbito global y puede ser accedida dentro de nuestra función `mostrarGlobal`. Aunque se ejecuta dentro de una función. Aunque el código se ejecuta dentro de una función, no está limitado a un ámbito local, por lo que puede acceder a nuestra variable `variableGlobal`.

**ámbito Local**
Nuestras variables definidas dentro de una función o bloque de código tienen un ámbito local. lo que significa que sólo son accesibles dentro de ese bloque. Una vez que la ejecución de la función ha terminado, las variables locales dejan de existir, ya que son destruidas por el garbage collector.

```javascript
function ambitoLocal() {
    let localVariable = "soy una variable local";
    console.log(localVariable);
}

ambitoLocal(); // salida "soy una variable local"
console.log(localVariable); // salida Uncaught ReferenceError ReferenceError: localVariable is not defined
```

Vemos como en este caso nuestra variable `localVariable` solo está disponible dentro de la función `ambitoLocal`. Si intentamos acceder a ella fuera de esa función, recibiremos un error, ya que las variables locales no son accesibles fuera de su función de definición.
