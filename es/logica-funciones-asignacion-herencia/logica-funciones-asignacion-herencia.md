# Manipulacion de logica de funciones: asignacion y herencia en JavaScript

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
    - [¿Qué es la asignación de funciones en JavaScript?](#qué-es-la-asignación-de-funciones-en-javascript)
    - [Importancia de la herencia en JavaScript](#importancia-de-la-herencia-en-javascript)
2. [Tipos de Asignación de Funciones](#tipos-de-asignación-de-funciones)
    - [Funciones declaradas](#funciones-declaradas)
    - [Funciones expresadas](#funciones-expresadas)
    - [Funciones asignadas a objetos](#funciones-asignadas-a-objetos)

---

## Introducción

En JavaScript, nuestras funciones son ciudadanos de primera clase, lo que significa que podremos asignarlas a variables, pasarlas como argumentos y devolverlas desde otras funciones. Además, el motor de JavaScript utiliza un modelo de herencia basado en prototipos en lugar de la herencia clásica de clases de otros lenguajes. Comprender cómo se asignan nuestras funciones y cómo opera la herencia será crucial para que podamos estructurar código reutilizable y eficiente.

### ¿Qué es la asignación de funciones en JavaScript?

Esto se refiere a la manera en que podemos almacenar nuestras funciones en variables, objetos o estructuras de datos. Dependiendo de cómo se definan, las funciones pueden comportarse de manera diferente, los principales tipos de asignación son funciones declaradas, funciones expresadas, funciones flecha y funciones en objetos.

### Importancia de la herencia en JavaScript

La herencia es un mecanismo que nos permite hacer que un objeto o función reutilice propiedades y métodos de otro. El motor de JavaScript basa la herencia en el sistema de prototipos, lo que significa que los objetos pueden heredar de otros a través de su cadena de prototipos (`prototype chain`), esto nos permite la reutilización de código , permitiendo compartir funcionalidades entre objetos, mejorar la eficiencia en memoria ya que los métodos compartidos se almacenan en un solo lugar en el prototipo en lugar de cada instancia y generar una organización estructurada donde se facilita la creación de modelos jerárquicos para organizar el código.

## Tipos de Asignación de Funciones

Javascript nos permite definir nuestras funciones de diferentes maneras , y cada una implica diferencias sutiles en el ámbito léxico, el comportamiento del `this`, el hosting, y en cómo interactúan con el entorno de ejecución.

### Funciones declaradas

Las funciones declaradas son las que creamos cuando utilizamos la palabra reservada función en una sentencia completa, no como parte de una expresión. en este caso capturan el entorno léxico en el que fueron creadas, su `this` será dinámico , es decir que dependerá del contexto de invocación y respecto al hoisting, este se encargara de elevar la función al principio del contexto de ejecución , lo que nos permitirá usarla antes de la línea donde es definida en el código.

veamos un ejemplo simple:

```javascript
function sumar5(value) {
    return value + 5;
}
```

### Funciones expresadas

las funciones expresadas son las funciones que definimos como parte de una expresión, como al asignarlas a una de nuestras variables o pasarlas como argumentos. en este caso `this` también es dinámico a menos que se utilice una función flecha y el hoisting solo elevara la declaración pero no el cuerpo de la función , es por eso que no podremos utilizarla antes de su inicialización en el código.

veamos un ejemplo:

```javascript
const sumar5 = function (value) {
    return value + 5;
};
```

### Funciones asignadas a objetos

Cuando asignamos una función como propiedad a un objeto, pasara a considerarse un método. Este tipo de asignación afecta directamente al valor `this`, ya que en este contexto hará referencia al objeto que posee el método, no posee intervención directa del hoisting.
veamos un ejemplo:

```javascript
const persona = {
    nombre: "Mauro",
    hablar() {
        console.log("Hola, soy " + this.nombre);
    },
};
```

<hr>
... Seccion bajo construcción ...
<hr>
