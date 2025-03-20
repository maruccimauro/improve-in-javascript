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
3. [Manipulación de Closures](#manipulación-de-closures)
    - [Persistencia de datos con closures](#persistencia-de-datos-con-closures)
    - [Encapsulación y privacidad de variables](#encapsulación-y-privacidad-de-variables)
    - [Closures en bucles y problemas comunes](#closures-en-bucles-y-problemas-comunes)
4. [Optimización y Rendimiento](#optimización-y-rendimiento)

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

## Manipulación de Closures

### Persistencia de datos con closures

Uno de los usos más comunes de los closures es la retención de datos en memoria. como nuestras funciones anidadas pueden acceder a variables de su función externa, incluso después de que esta última ha finalizado su ejecución, podemos usar este mecanismo para guardar estados sin necesidad de variables globales.

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

const contador2 = crearContador(); // (es un nuevo closure independiente)
contador2(); //salida 1
contador2(); //salida 2
```

La función `crearContador` crea una variable `conteo` dentro de su ámbito y retorna una función que puede acceder y modificar `conteo`. cada vez que ejecutamos contador1(), la varaible `conteo` dentro de su closure sigue existiendo y se incrementa, al crear contador2. generamos un nuevo closure independiente con su propia variable `conteo`, mostrando que los closures pueden actuar como instancias separadas.

### Encapsulación y privacidad de variables

el motor de JavaScript no nos provee de un modificador de acceso como `private` en otros lenguajes. Sin embargo, los closures nos permiten lograr encapsulación, impidiendo que ciertas variables sean accesibles desde fuera de una función.

```javascript
function usuario(nombre) {
    let _nombre = nombre;

    return {
        getNombre: function () {
            return _nombre;
        },
        setNombre: function (nuevoNombre) {
            _nombre = nuevoNombre;
        },
    };
}

const usuario1 = usuario("Juan");
console.log(usuario1.getNombre()); // salida Juan
usuario1.setNombre("Mauro");
console.log(usuario1.getNombre()); // salida Mauro
console.log(usuario1._nombre); //salida undefined
```

\_nombre es nuestra variable privada dentro del closure y no puede ser modificada directamente desde afuera, `getNombre` y `setNombre` son métodos expuestos que permiten leer y modificar `_nombre` sin acceder directamente a ella. Intentar acceder a `_nombre` desde fuera (`usuario1._nombre`) nos devolver undefined, garantizándonos así privacidad.

### Closures en bucles y problemas comunes

El uso incorrecto de closures dentro de bucles puede generarnos comportamientos inesperados, debido a que las variables dentro del closure pueden quedar ligadas al estado final del bucle en lugar de capturar el valor en cada iteración.

```javascript
for (var i = 10; i <= 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 1000);
}

// salidas recibidas despues de 1 segundo:
// salida iteracion 1 : 3
// salida iteracion 2 : 3
// salida iteracion 3 : 3
```

vemos como `setTimeout` ejecuta su callback después de que el bucle ha terminado,`var i` es una variable global en este contexto, por lo que su valor final es 3 al momento de ejecutar el setTimeout.

para solucionar esto podemos usar `let` en lugar de `var` evitando así usar una variable de ámbito global y usar una variable de ámbito de bloque obteniendo el valor de `i` al momento de programar el `setTimeout`.

```javascript
for (let i = 1; i <= 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 1000);
}

// salidas recibidas despues de 1 segundo:
// salida iteracion 1 : 0
// salida iteracion 2 : 1
// salida iteracion 3 : 2
```

otra alternativa en caso de no poder usar `let` es usar un closure explicito para capturar el valor correcto.

```javascript
for (var i = 0; i < 3; i++) {
    (function (capturaI) {
        setTimeout(() => {
            console.log(capturaI);
        }, 1000);
    })(i);
}
// salidas recibidas despues de 1 segundo:
// salida iteracion 1 : 0
// salida iteracion 2 : 1
// salida iteracion 3 : 2
```

creamos un IIFE (inmediately invoke function expression) que recibirá `i` como argumento y la usa dentro del closure donde `captureI` mantendrá el valor correcto en cada iteración.

## Optimización y Rendimiento

Cuando creamos un closure, se mantiene una referencia a las variables de la función externa en la memoria, incluso después de que la función externa haya terminado su ejecución. Esto se debe a que las funciones anidadas (closures) siguen necesitando acceso a esas variables. Este comportamiento tiene un impacto directo en el uso de la memoria. Para manejar esto podemos evitar realizar closures innecesarios , es decir que cuando no tengamos un estado persistente que guardar no sera necesario crear un closure, por otro lado , podemos liberar las referencias a las variables que mantiene si un closure ya no es necesario.

```javascript
contador = null; /// Liberamos referencia al closure.
```

## Conclusión

En resumen, los closures son una característica en JavaScript que permite a nuestras las funciones acceder a variables fuera de su ámbito, lo que nos facilita la creación de funciones flexibles y persistentes. Sin embargo, su uso requiere cuidado para evitar problemas de rendimiento y consumo de memoria. Los closures nos permiten encapsular y mantener el estado, pero también exigen una gestión adecuada de las referencias a las variables para evitar fugas de memoria.

### Resumen de los conceptos clave

**Closure:** Es una función que tiene acceso a su propio ámbito, al ámbito externo y al ámbito global, incluso después de que la función externa haya finalizado su ejecución.

**Ámbito léxico:** Se refiere a la regla que determina el ámbito de las variables en función de la estructura de las funciones en el código, no en el momento de ejecución.

**Persistencia de datos:** Los closures pueden retener el estado de las variables de una función externa, lo que permite su persistencia más allá de la ejecución de la función original.

**Recolección de basura:** Los closures pueden interferir con la recolección de basura si mantienen referencias a objetos o variables que ya no son necesarias, causando fugas de memoria.

---

Muchas Gracias por leerme!
Marucci Mauro
[www.linkedin.com/in/mauro-marucci/](https://www.linkedin.com/in/mauro-marucci/)
[https://github.com/maruccimauro](https://github.com/maruccimauro)

---
