# Manipulación de Lógica de Evaluación de Truthy y Falsy en JavaScript

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
    - [Importancia de la manipulación de objetos y arrays en JavaScript](#importancia-de-la-manipulación-de-objetos-y-arrays-en-javascript)
    - [Diferencia entre shallow copy y deep copy](#diferencia-entre-shallow-copy-y-deep-copy)

---

## Introducción

Que podamos comprender la manipulación de datos en JavaScript, particularmente de objetos y arrays, es un aspecto fundamental cuando trabajemos con aplicaciones dinámicas. Cuando gestionamos datos en este lenguaje, es esencial entender cómo las operaciones de copia afectan la mutabilidad y el comportamiento de nuestros datos.

### Importancia de la manipulación de objetos y arrays en JavaScript

En JavaScript, nuestros objetos y arrays son estructuras de datos fundamentales que se utilizan para representar informacion compleja. Sin embargo, a diferencia de los tipos de datos primitivos (como números, cadenas de texto , etc), los objetos y arrays son mutable y se pasan por referencia. Esto implica que, cuando modifiquemos una de estas estructuras, cualquier otra referencia al mismo objeto o array también verá reflejados esos cambios. Comprender esto nos permitira evitar efectos inesperados.

```javascript
let persona1 = { nombre: "Juan", edad: "30" };
let persona2 = persona1;
persona2.nombre = "Mauro";

console.log(persona1.nombre); // "Mauro"
```

como podemos observar el cambio en la propiedad nombre de `persona2` se ve reflejada en `persona1` tambien.

### Diferencia entre shallow copy y deep copy

Las copias de nuestros objetos y arrays pueden clasificarse en dos tipos principales : shallow copy (copia superficial) y deep copy(copia profunda)

**Shallow Copy:**
Este tipo de copia nos crea un nuevo objeto o array, pero las referencia a los elementos internos del objeto o array original no se copia, si no que se comparten. Es decir, si el objeto o array original contiene otros objetos o arrays anidados, esos elementos siguen siendo referenciados directamente desde la copia. Por otra parte los datos primitivos que contenga el objeto o array , seran copias directas de los valores contenidos , es decir que no se veran afectados por el objeto o array copia.

```javascript
let persona1 = {
    nombre: "Mauro",
    direccion: { calle: "Mi Linda Calle", numeracion: "1234" },
};
let persona2 = { ...persona1 };

persona2.nombre = "Juan";
persona2.direccion.calle = "Otra Calle";
persona2.direccion.numeracion = "5678";

console.log(persona1.nombre, persona1.direccion); // Mauro {calle: 'Otra Calle', numeracion: '5678'}
console.log(persona2.nombre, persona2.direccion); // Juan {calle: 'Otra Calle', numeracion: '5678'}
```

Aqui podemos observar como el nombre no se ve afectado por referencias asociadas ya que son datos primitivos , y en contra parte , el objeto `direccion` si afecta tanto a `persona1` como a `persona2` ya que comparten la misma referencia.

**Deep Copy:**
A diferencia de la shallow copy, la deep copy nos creara una nueva estructura completamente independiente, copiando solo nuestro objeto o array original, si no también todos los elementos internos (y sus subelementos).

```javascript
let persona1 = {
    nombre: "Mauro",
    direccion: { calle: "Mi Linda Calle", numeracion: "1234" },
};
let persona2 = JSON.parse(JSON.stringify(persona1));

persona2.nombre = "Juan";
persona2.direccion.calle = "Otra Calle";
persona2.direccion.numeracion = "5678";

console.log(persona1.nombre, persona1.direccion); // Mauro {calle: 'Mi Linda Calle', numeracion: '1234'}
console.log(persona2.nombre, persona2.direccion); // Juan {calle: 'Otra Calle', numeracion: '5678'}
```

Podemos observar que al utilizar `JSON.parse(JSON.stringify())` hemos realizado una copia profunda de todos los elementos de persona1 , sin enlazar sus referencias a persona2, donde cada uno es afectado solo por sus propios cambios.
