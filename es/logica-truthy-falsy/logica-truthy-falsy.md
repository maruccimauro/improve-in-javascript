# Manipulación de Lógica de Evaluación de Truthy y Falsy en JavaScript

---

**Índice de la Guía**

1. [Introducción](#introducción)
    - [¿Qué es truthy y falsy en JavaScript?](#qué-es-truthy-y-falsy-en-javascript)
    - [Importancia en la evaluación lógica](#importancia-en-la-evaluación-lógica)
    - [Diferencias con otros lenguajes](#diferencias-con-otros-lenguajes)
2. [Conceptos Fundamentales](#conceptos-fundamentales)
    - [Definición formal de truthy y falsy](#definición-formal-de-truthy-y-falsy)
    - [Valores falsy en JavaScript](#valores-falsy-en-javascript)
    - [Valores truthy en JavaScript](#valores-truthy-en-javascript)
3. [Evaluación de Expresiones Booleanas](#evaluación-de-expresiones-booleanas)
    - [Coerción implícita en operaciones booleanas](#coerción-implícita-en-operaciones-booleanas)
    - [Operadores de comparación y truthy/falsy](#operadores-de-comparación-y-truthyfalsy)
    - [== vs ===: impacto en truthy y falsy](#-vs--impacto-en-truthy-y-falsy)
4. [Operadores Lógicos y Evaluación de Cortocircuito](#operadores-lógicos-y-evaluación-de-cortocircuito)
    - [Operador lógico && (AND)](#operador-lógico--and)
    - [Operador lógico || (OR)](#operador-lógico--or)
    - [Operador lógico ! (NOT)](#operador-lógico--not)
    - [Evaluación de cortocircuito](#evaluación-de-cortocircuito)
5. [Manipulación Avanzada de Truthy y Falsy](#manipulación-avanzada-de-truthy-y-falsy)
    - [Uso en asignaciones predeterminadas (|| y ??)](#uso-en-asignaciones-predeterminadas--y-)
    - [Doble negación (!!) y coerción explícita](#doble-negación--y-coerción-explícita)
    - [Optional Chaining (?.) y falsy](#optional-chaining--y-falsy)
6. [Aplicaciones Prácticas y Casos de Uso](#aplicaciones-prácticas-y-casos-de-uso)
    - [Validaciones de datos](#validaciones-de-datos)
    - [Valores predeterminados en funciones](#valores-predeterminados-en-funciones)
    - [Uso en estructuras de control](#uso-en-estructuras-de-control)
    - [Filtros y limpieza de datos](#filtros-y-limpieza-de-datos)
7. [Errores Comunes y Buenas Prácticas](#errores-comunes-y-buenas-prácticas)
    - [Confusión entre null, undefined y false](#confusión-entre-null-undefined-y-false)
    - [Errores con 0, NaN y cadenas vacías](#errores-con-0-nan-y-cadenas-vacías)
    - [Manejo seguro de valores](#manejo-seguro-de-valores)
8. [Comparación con Otros Lenguajes](#comparación-con-otros-lenguajes)
    - [Diferencias de coerción en TypeScript](#diferencias-de-coerción-en-typescript)
9. [Conclusión y Recursos Adicionales](#conclusión-y-recursos-adicionales)
    - [Resumen de conceptos clave](#resumen-de-conceptos-clave)
    - [Recursos recomendados](#recursos-recomendados)
    - [Ejercicios y desafíos prácticos](#ejercicios-y-desafíos-prácticos)

---

## Introducción

### ¿Qué es truthy y falsy en JavaScript?

En Javascript , cuando hablamos de los términos truthy y falsy (verdad y falsedad) describen como se comportan cuando son evaluados en un contexto booleano , es decir, cuando se utilizan en expresiones condicionales como lo podrían ser if, while o en operadores lógicos tales como (&&, || ,!).

veamos las definiciones tanto de Truthy y falsy.
Falsy: Son todos aquellos valores que, cuando se convierten a booleano, resultaran en **false**.
Truthy: Son todos aquellos valores que, cuando se convierten a booleano, al contrario de Falsy, resultaran en **True**.

Dado que Javascript tiene la característica de ser un lenguaje con tipado dinámico (es decir, que las variables no tienen un tipo fijo y pueden cambiar de tipo en tiempo de ejecución.) y coerción implícita (es decir, que cada vez sea necesario JavaScript convertirá una variable de un tipo de dato a otro diferente, por ejemplo para hacer una evaluación) cualquier valor puede ser tratado como un booleano dependiendo del contexto en que se utilice. La conversión implícita de valores a true o false es lo que define su clasificación para pertenecer al grupo de valores Truthy o Falsy.

¡Veamos un ejemplo básico para entenderlo mejor!

```javascript
if ("any text") {
    console.log("Esto es un valor de la categoria Truthy");
} else {
    console.log("Esto es un valor de la categoria Falsy");
}
```

En este caso la cadena "any text" es un valor que pertenece a la categoría Truthy por que no está vacía, y bajo coerción implícita, JavaScript lo transforma en true.

Pero... ¿ qué sucede si evalúa una cadena que esta vacía ?

```javascript
if ("") {
    console.log("Esto es un valor de la categoria Truthy");
} else {
    console.log("Esto es un valor de la categoria Falsy");
}
```

En este caso la cadena "" es un valor Falsy , porque esta vacío y bajo coerción implícita, JavaScript lo transforma en false

Comprender esto es sumamente importante al momento de usar estructuras de control(if, while) , operadores lógicos(&&,||,!), coerción en comparaciones (\==,===) y demás escenarios.

### Importancia en la evaluación lógica

El concepto de truthy y falsy en JavaScript es fundamental para evaluar la lógica, afectando el comportamiento de expresiones condicionales, operadores lógicos y estructuras de control. Su comprensión permite escribir código más limpio, eficiente y robusto, evitando así que tengamos errores comunes relacionados con la coerción implícita de valores.

**¿Como afecta esto a los condicionales?**
Las estructuras condicionales (if, while, for) dependen de la evaluación de una expresión de tipo booleana. En JavaScript, cualquier valor que no sea estrictamente false (o Falsy) se considera true (o truthy).
Esto nos permitirá simplificar evaluaciones sin necesidad de comparación explicitas extendidas.

vayamos a un ejemplo conjunto para entenderlo mejor, haciendo dos comparaciones, una sin coerción implícita y otra con coerción implícita.

Ejemplo con coerción implícita:

```javascript
let nombre = "Juan";

if (nombre != "" && nombre != null && nombre != undefined) {
    console.log("el nombre es valido.");
}
```

Ahora, veamos el mismo resultado permitiendo que JavaScript aplique la coerción implícita:

```javascript
let nombre = "Juan";

if (nombre) {
    console.log("el nombre es valido.");
}
```

Si entendemos lo que sucede subyacentemente en el segundo ejemplo , nos permitirá escribir menor cantidad de código y mejorar la legibilidad sin afectar la funcionalidad.

**¿Cuál es el uso frente a los Operadores Lógicos?**
En tanto a los operadores lógicos (&&,||,!) dependen de que el valor se evalúe como truthy o falsy para asi poder determinar el flujo de ejecución y la asignación de valores.

**Operador OR (||)**
se usa para asignar valores predeterminados cuando un valor evaluado es falsy.

```javascript
let usuario = null;
let nombre = usuario || "Invitado";

console.log(nombre); // "Invitado"
```

Ya que usuario al momento de evaluarse es un valor del tipo falsy, el operador OR se encargará de pasar el valor "invitado" al operador de asignación (=).

**Operador AND (&&)**
Nos permite ejecutar una expresión solo si la primera es un valor de tipo truthy.

```javascript
let usuario = "Juan";
usuario && console.log("Bienvenido " + usuario);
```

En este ejemplo, ya que usuario contiene un valor del tipo truthy el operador AND (&&) ejecutara la expresión a su derecha, caso contrario, si usuario fuera "" (cadena vacía) nunca veríamos el mensaje en consola.

operador NOT(!).
Este operador está encargado de convertir un valor a tipo booleano mediante coerción implícita e invertirlo.

```javascript
console.log(!0);
// true , al invertir el valor booleano de 0 (false) obtenemos true.

console.log(!"Juan");
// false , la inversion del valor booleano de una cadena no vacia(true) es false
```

### Diferencias con otros lenguajes

En JavaScript, la coerción implícita es la encargada de convertir de manera automática ciertos valores en true o false. Pese a que este es un concepto global frente otros lenguajes de programación, la conversión booleana difiere entre los mismos.
Para poder observar correctamente esta idea, veamos una tabla comparativa de como diferentes lenguajes interpretan de manera distinta la coerción implícita:

| Valor                   | JavaScript | Python                                              | PHP                    |
| ----------------------- | ---------- | --------------------------------------------------- | ---------------------- |
| `false`                 | `falsy`    | `falsy`                                             | `falsy`                |
| `0`                     | `falsy`    | `falsy`                                             | `falsy`                |
| `-0`                    | `falsy`    | `truthy`                                            | `falsy`                |
| `0n` (BigInt)           | `falsy`    | `N/A` (No equivalente)                              | `N/A` (No equivalente) |
| `""` (cadena vacía)     | `falsy`    | `falsy`                                             | `falsy`                |
| `null`                  | `falsy`    | `falsy`                                             | `falsy`                |
| `undefined`             | `falsy`    | `N/A` (No existe `undefined`, pero `None` es falsy) | `N/A` (PHP usa `null`) |
| `NaN`                   | `falsy`    | `falsy`                                             | `falsy`                |
| `[]` (array vacío)      | `truthy`   | `falsy`                                             | `falsy`                |
| `{}` (objeto vacío)     | `truthy`   | `falsy`                                             | `truthy`               |
| `"0"` (cadena con cero) | `truthy`   | `truthy`                                            | `falsy`                |

## Conceptos Fundamentales

Hay que entender, que en JavaScript todos los valores pueden clasificarse en truthy o falsy al ser evaluados en un contexto booleano. Por ello, cuando usamos un valor dentro de una expresión lógica (ej. if, while, &&, ||, etc), se comportará como true o false sin necesidad de que hagamos una conversión explícita.

### Definición formal de truthy y falsy

**Definicion formal de Falsy:**
Un valor falsy es aquel que, cuando se evalúa en un contexto booleano, se convierte en false.

**Definición Formal de Truthy:**
Por otra parte, un valor Truthy es cualquier valor que no sea falsy, es decir, que cuando lo evaluamos en un contexto booleano, se convierte en true.

### Valores falsy en JavaScript

en la siguiente tabla encontraremos la representacion del conjunto de valores falsy.
| Valor | Descripción |
|------------|------------|
| `false` | El valor booleano `false`. |
| `0` | El número `0` en cualquier base (`0`, `0.0`, `0x0`, etc.). |
| `-0` | El número `-0`, que es distinto de `0` en ciertas operaciones matemáticas. |
| `0n` | El `BigInt` con valor `0n`. |
| `""` | Una cadena vacía. |
| `null` | Representa la ausencia de valor. |
| `undefined`| Representa un valor no definido. |
| `NaN` | El resultado de una operación matemática inválida. |

### Valores truthy en JavaScript

en la siguiente tabla encontraremos la representacion del conjunto de valores truthy.
| Valor | Descripción |
|---------------------------------|------------|
| `true` | El valor booleano `true`. |
| Cualquier número distinto de `0` | Incluye positivos y negativos como `42`, `-3.14`. |
| Cualquier `BigInt` distinto de `0n` | Ejemplo: `1n`, `-10n`. |
| Cadenas no vacías | `"hello"`, `"false"`, `"0"`, etc. |
| Objetos | `{}`, `{ key: "value" }`, `new Date()`, etc. |
| Arrays | `[]`, `[1, 2, 3]`, etc. (incluso un array vacío es truthy). |
| Funciones | `function() {}`, `() => {}`, etc. |

## Evaluación de Expresiones Booleanas

En JavaScript, como ya lo hemos visto, las expresiones booleanas son aquellas que se evalúan como true o false. Debido a que JavaScript tiene como parte de su naturaleza la coerción implícita, cuando evaluemos expresiones en un contexto booleano algunos valores se convertirán automáticamente en true (truthy) o false (falsy) sin necesidad de una conversión explicita por parte del desarrollador.

### Coerción Implícita en Operaciones Booleanas

La coerción implícita sucede cuando el motor de JavaScript convierte un valor de un tipo de datos a otro de manera automática, no necesariamente siempre a un valor booleano, no obstante, cuando hablamos de expresiones booleanas, cualquier valor que no sea estrictamente true o false se convertirá en uno de ellos cuando se use en un contexto lógico.

```javascript
let valor1 = 0;
let valor2 = 100;

console.log(valor1 ? "valor de conjunto truthy" : "valor de conjunto falsy"); // valor de conjunto falsy
console.log(valor2 ? "valor de conjunto truthy" : "valor de conjunto falsy"); // valor de conjunto truthy
```

### Operadores de Comparación y Truthy/Falsy

Los operadores de comparación que utilizamos cotidianamente (\<, \>, \<\=, \>\=, \=\=, \=\=\=) pueden verse afectados por la coerción implícita de valores, en especial cuando no usamos \=\=\=, ya que esto permite la conversión de tipos antes de la comparación

```javascript
console.log(0 == false); // true (0 es falsy y se convierte en false)
console.log("" == false); // true ("" es falsy y se convierte en false)
console.log(null == undefined); // true (JavaScript los trata como equivalentes)
console.log([] == false); // true (array vacío es truthy, pero se convierte a cadena vacía)
console.log(0 === false); // false (diferentes tipos: number vs boolean)
console.log("" === false); // false (diferentes tipos: string vs boolean)
console.log(null === undefined); // false (son diferentes tipos)
```

### == vs ===: impacto en truthy y falsy

Veamos la diferencia en este contexto de utilizar los dos operadores de igualdad que JavaScript nos provee, en el caso del operador == (igualdad no estricta) permite que el motor de JavaScript utilice la coerción implicita, por otra parte al utilizar el operador === (igualdad estricta) comparara los operandos tanto con su valor y el tipo de dato sin aplicar ninguna coercíon implícita.
Por tanto si quieres un mayor control granular al momento de verificar tus datos , es recomendable utilizar el operador de igualdad estricta.

```javascript
console.log("0" == 0); // true (con coerción: la cadena "0" se convierte a número)
console.log("0" === 0); // false (sin coerción: diferentes tipos, string vs number)

console.log([] == false); // true (con coerción: array vacío es truthy, pero se convierte a "")
console.log([] === false); // false (sin coerción: diferentes tipos, array vs boolean)
```

## Operadores Lógicos y Evaluación de Cortocircuito

En cualquier lenguaje de programación los operadores lógicos son fundamentales, y JavaScript no es una excepción de ello, el uso de operadores lógicos es muy común para realizar comparaciones, combinar expresiones booleanas y hasta para beneficiarse de un comportamiento conocido como evaluación de cortocircuito (short-circuit evaluación), que optimiza el rendimiento e influye en el flujo de control de los programas.
Primero profundicemos en los operadores lógicos &&, || y ! para a posterior abordar en cada uno comprender su flujo de un cortocircuito.

### Operador lógico && (AND)

el operar lógico && en condicionales devuelve true solo cuando ambos operandos (izquierdo y derecho) son un valor del conjunto Truthy.

```javascript
if (true && 5) {
    console.log("la evalaucion es true.");
} else {
    console.log("la evalaucion es false.");
} // la evalaucion es true.
```

```javascript
if (true && 0) {
    console.log("la evalaucion es true.");
} else {
    console.log("la evalaucion es false.");
} // la evalaucion es false.
```

En tanto cuando hablamos de asignación y argumentos el comportamiento del operador && determina que en caso de que el primer operando pertenezca al conjunto de valores truthy este devolverá el segundo operando (derecha), en contrario si pertenece al conjunto de valores falsy , devolverá el primer operando (izquierda).
Veámoslo mejor con un ejemplo.

```javascript
console.log(0 && "hola mundo"); // el primer operando es falsy , por lo cual mostrara 0
```

```javascript
console.log([] && "hola mundo"); // el primer operando es truthy , por lo cual mostrara "hola mundo"
//recuerda que para JavaScript un array vacio es un valor delc conjunto Truthy.
```

### Operador lógico || (OR)

el operador lógico || (or) devolverá true, si al menos 1 de los operandos es Truthy, si ambos son falsy , devolverá false.

```javascript
console.log(true || true); // true
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false
```

En tanto cuando hablamos de asignación y argumentos el comportamiento del operador || determina que en todos los casos se devolverá el primer operando (izquierda) sea cual sea, su conjunto de pertenencia(truthy o falsy)
Vayamos a un ejemplo para entenderlo mejor:

```javascript
console.log([] || "hola mundo"); // sin importar si es falsy o truthy , devolvera (0)[] un array vacio.
```

### Operador lógico ! (NOT)

El operador ! (NOT) tiene la particularidad a contraste de && y ||, de ser un operador unario, es decir que posee un único operando, en caso del lado derecho, al utilizarlo podremos notar que convierte el valor del operando a un valor booleano y a posterior invierte dicho valor, tal que, si el valor es false se convertirá en true y si el valor es true se convertirá en false.
observemos esto con el siguiente ejemplo:

```javascript
console.log(!true); // false
console.log(!false); // true
console.log(!0); // true
console.log(!""); // true
```

### Evaluación de cortocircuito

¡Ahora que abordamos los operadores comprometidos a este tema, podemos afrontar el concepto de cortocircuito! vayamos por él.
La evaluación de cortocircuito es una característica sumamente importante de los operadores lógicos en JavaScript.
Es comportamiento determina que el segundo operando de una expresión lógica no se evalúa si el resultado puede determinarse a partir del primer operando.

**Evaluación de cortocircuito con && (AND):**
Si el primer operando es falsy, el resultado de la expresión es falsy sin necesidad de evaluar el segundo operando.

```javascript
function anunciar() {
    console.log("La ejecucion paso por aqui!");
}

false && anunciar();
//no veremos nada por consola , por que el primer operando pertenece al conjunto falsy
```

en caso contrario, si el operador izquierdo es del conjunto truthy, el segundo operando será evaluado.

```javascript
function anunciar() {
    console.log("La ejecucion paso por aqui!");
}

true && anunciar();
//veremos por consola "La ejecucion paso por aqui!" , por que el primer operando pertenece al conjunto truthy
```

**Evaluación de cortocircuito con || (OR):**
Si el primer operando es truthy, el resultado es el primer operando, sin necesidad de evaluar el segundo operando.

```javascript
function anunciar() {
    console.log("La ejecucion paso por aqui!");
}

true || anunciar();
//no veremos nada por consola , por que el primer operando pertenece al conjunto trurhy.
```

Si el primer operando es falsy, el resultado es el segundo operando.

```javascript
function anunciar() {
    console.log("La ejecucion paso por aqui!");
}

false || anunciar();
//veremos por consola "La ejecucion paso por aqui!" , por que el primer operando pertenece al conjunto falsy
```

**Evaluación de cortocircuito y la seguridad:**
El uso de cortocircuito también nos permite minimizar los riesgos de error al intentar acceder a áreas no definidas o donde un operador no está definido, evitando así un fallo.
si el primer operando no es truthy el segundo operando no existiría, por ende, evitamos ejecutarlo.

```javascript
let user = null;

console.log(user && user.name); // user es null , por tanto user.name no existe y nunca se ejecuto el segundo operando.
```

## Manipulación Avanzada de Truthy y Falsy

Comprender como manipular la toma de decisiones avanzadas con fundamentos de truthy y falsy, nos va a permitir escribir un Código más limpio , seguro y eficiente. ¡Vamos por ello!

### Uso en asignaciones predeterminadas (|| y ??)

JavaScript nos permite asignar valores predeterminados a una variable en caso de que su valor original sea falsy o nullish. Tradicionalmente, se usaba el operador lógico || (OR) pero con la introducción de Nullish coalescing (??, coalision nula) tenemos una nueva opción más precisa.
Veamos la diferencia entre los dos , en un caso donde es propicia la utilización de ?? (nullish coalescing).

En este caso tenemos el operador || (OR) que considera el valor 0 como un Falsy y nos devolviera el segundo operador, pero en nuestro contexto de uso, queremos que el valor 0 nos permita definir un mensaje sin espera, pero el operador || (OR) no lo permite:

```Javascript
let tiempoEspera = 0;
let timeout = tiempoEspera || 3000;

setTimeout(() => {
    console.log("hola mundo.");
}, timeout); //aparecera un mensaje despues de 3 segundos.
```

es por ello que aquí entra en juego el operador ?? (nullish coalescing) cuyo comportamiento dictamina que todo valor que no sea null o undefined será considerado como valido, esto incluyendo al número 0 en cuestión. Entonces, si se recibe como primer operando un valor valido, obtendremos ese mismo valor, en caso de ser un valor no valido, obtendremos el valor del segundo operando.
Vemos como ahora sí, nuestra rutina funciona correctamente al ingresar el valor 0 o null/undefined.

```Javascript
let tiempoEspera = 0;
let timeout = tiempoEspera ?? 3000;

setTimeout(() => {
    console.log("hola mundo.");
}, timeout); //aparecera un mensaje en 0 segundos, es decir sin espera.
```

```Javascript
let tiempoEspera = undefined;
let timeout = tiempoEspera ?? 3000;

setTimeout(() => {
    console.log("hola mundo.");
}, timeout); //aparecera un mensaje en 3 segundos.
```

| Valor               | Considerado Válido (`??`) | Considerado Inválido (`??`) |
| ------------------- | ------------------------- | --------------------------- |
| `null`              | ❌ No                     | ✅ Sí                       |
| `undefined`         | ❌ No                     | ✅ Sí                       |
| `false`             | ✅ Sí                     | ❌ No                       |
| `0`                 | ✅ Sí                     | ❌ No                       |
| `""` (cadena vacía) | ✅ Sí                     | ❌ No                       |
| `"texto"`           | ✅ Sí                     | ❌ No                       |
| `NaN`               | ✅ Sí                     | ❌ No                       |
| `{}` (objeto vacío) | ✅ Sí                     | ❌ No                       |
| `[]` (array vacío)  | ✅ Sí                     | ❌ No                       |

### Doble negación (!!) y coerción explícita

**¿Qué es !!(double negation) y por qué se usa?**
En JavaScript, el uso de doble negación se usa para convertir cualquier valor en su equivalente booleano de manera explícita.
Al aplicar la primer negacion ! , utilizamos la coerción implícita para transforma un valor en un booleano y a su vez ese valor es invertido, el segundo operador de negación permite volver a invertir la negación inicial obteniendo explícitamente el valor booleano original.

```
console.log(!!"Hola");  // true
console.log(!!0);       // false
console.log(!!null);    // false
console.log(!!"");      // false
console.log(!![]);      // true (recuerda que un array vacío es truthy)
console.log(!!{});      // true (recuerda que un objeto vacío es truthy)
```

Normalmente, remitimos esta práctica a validar si una variable tiene un valor "real":

```javascript
let userInput = "";
if (!!userInput) {
    console.log("Tiene valor");
} else {
    console.log("No tiene valor");
} // "No tiene valor"
```

### Optional Chaining (?.) y falsy

El encadenamiento opción ?. (optional chaining) es una funcionalidad que nos permite acceder a propiedades de objetos sin provocar errores si la propiedad no existe o es nullish (null o undefined), en cambio nos devolverá undefined.
Veamos dos claros ejemplos para interpretar como procede esta funcionalidad muy útil.

Sin ?. (Optional Chaining):

```javascript
let usuario = { perfil: null };

console.log(usuario.perfil.nombre); // nos devolvera un error del tipo "Cannot read properties of null"
```

Con ?. (optional Chaining):

```javascript
let usuario = { perfil: null };

console.log(usuario.perfil?.nombre); // nos devolera "undefined"
```

## Aplicaciones Prácticas y Casos de Uso

El conocer sobre valor truthy y falsy, junto con los operadores &&, ||, ??, !, ?., tiene muchas aplicaciones prácticas en la programación, tales como validación de datos, asignación de valores predeterminados en funciones, estructuras de control y limpieza de datos.

### Validaciones de datos

una de las aplicaciones más comunes de estos conocimientos es la validación de datos mediante el manejo de truthy y falsy. por ejemplo, al trabajar con formularios, apis o bases de datos, es fundamental de que los valores que el usuario ingrese sean correctos y no estén vacíos.

```javascript
function preValidarFormulario(datos) {
    let errores = false;
    if (!datos.nombre) {
        console.log("El nombre es obligatorio.");
        errores = true;
    }

    if (!datos.apellido) {
        console.log("El apellido es obligatorio.");
        errores = true;
    }

    if (!datos.edad || datos.edad < 18) {
        console.log("Debes tener al menos 18 años");
        errores = true;
    }

    if (!errores) {
        console.log("los datos son validos.");
        return true;
    }

    return false;
}

usuario1 = { nombre: "Mauro", apellido: "Marucci", edad: "34" };
usuario2 = { nombre: "juan", apellido: "juancho", edad: "17" };

preValidarFormulario(usuario1);
preValidarFormulario(usuario2);
```

Aquí utilizamos ! (NOT) para verificar cadenas vacías o valores no definidos y || (OR) para controlar la edad mínima en caso de que se haya ingresado un valor

### Valores predeterminados en funciones

Al momento de definir funciones dado un contexto propicio es importante establecer valores predeterminados para evitar errores cuando los parámetros no son proporcionados.

```javascript
function saludar(nombre) {
    nombre = nombre || "Invitado";
    console.log(`Hola ${nombre}!`);
}

usuario = null;

saludar("Mauro"); // "Hola Mauro!"
saludar(""); // "Hola Invitado!"
saludar(undefined); // "Hola Invitado!"
saludar(usuario?.nombre); // "Hola Invitado!"
```

Aquí utilizamos || (OR) para asignar un valor en caso de no recibir uno valido y ?. (optional Chaining) para poder enviar un valor en caso de que el usuario no haya sido definido.

```javascript
let activo = true;

if (activo === true) {
    console.log("El usuario está activo");
}
```

lo cambiamos por :

```javascript
let activo = true;

if (activo) {
    console.log("El usuario está activo");
}
```

### Uso en estructuras de control

El conocimiento de truthy y falsy nos permite simplificar la lógica de muchas estructuras de control.

```javascript
let nombre = "Mauro";

if (nombre != "" && nombre != null && nombre != undefined) {
    console.log(`Hola ${nombre}!`);
}
```

lo cambiamos por :

```javascript
let nombre = "Mauro";

if (nombre) {
    console.log(`Hola ${nombre}!`);
}
```

otro ejemplo.

```javascript
if (usuario.estaVerificado) {
    if (enviarCorreoDeConfirmacion()) {
        esperarConfirmacion();
    }
}
```

lo cambiamos por:

```javascript
usuario.estaVerificado && enviarCorreoDeConfirmacion() && esperarConfirmacion();
```

### Filtros y limpieza de datos

El manejo de valores truthy y falsy es útil para filtrar arrays y limpiar datos en JavaScript.

```javascript
let datos = [0, "Hola", "", null, 42, undefined, "JavaScript", false];

let datosLimpios = datos.filter(Boolean); // Se usa Boolean como callback
console.log(datosLimpios); // [ "Hola", 42, "JavaScript" ]
```

## Errores Comunes y Buenas Prácticas

Abordaremos algunos errores comunes y buenas prácticas para poder aplicar lo aprendido de manera correcta, ¡recuerda que uno nunca deja de aprender!

### Confusión entre null, undefined , false y el uso de == y ===

Uno de los errores más comunes entre los desarrolladores es la confusión entre los valores null, undefined y false, aunque todos pertenecen al conjunto de falsy , no son lo mismo y tampoco operan igual ante el operador == (igualdad no estricta).
Veamos la definición de cada uno para entender esta idea correctamente.

**null:** Representa la ausencia intencionada de cualquier valor o referencia. Es un valor explícito asignado por el desarrollador para indicar que algo está vacío.

```javascript
let user = null; // Significa que la variable "user" está vacía, pero explícitamente.
```

**undefined:** indica que una variable ha sido declarada pero no inicializada (es decir, no se le ha asignado un valor). También es el valor que retorna una función que no tiene un return explícito.

```javascript
let user; // 'user' ha sido declarada, pero no inicializada, por lo tanto tiene el valor `undefined`
```

```javascript
function saludo() {
    console.log("Hola");
}
console.log(saludo()); // Esto devuelve `undefined` porque no hay un `return`
```

**false:**: es un valor booleano que explícitamente significa "falso".

```javascript
let activado = false; // activado esta explicitamente como falso.
```

por lo tanto null , undefined y false pertenecen al conjunto de valores falsy pero son diferentes , podemos corroborarlo ejerciendo una comparación estricta:

```javascript
console.log(false === null); // false, pertenecen los dos al conjunto falsy pero no son lo mismo
console.log(false === undefined); // false, pertenecen los dos al conjunto falsy pero no son lo mismo
console.log(null === undefined); // false, pertenecen los dos al conjunto falsy pero no son lo mismo
```

Así mismo, pese a que null , undefined y false pertenecen al conjunto de valores falsy el operador == (igualdad no estricta) posee sus propias reglas dentro del motor de JavaScript al ejercer la coerción implícita sobre undefined y null, donde se determina que solo ellos dos son no estrictamente iguales:

```javascript
console.log(false == null); // false para el operador de igualdad no estricta
console.log(false == undefined); // false para el operador de igualdad no estricta
console.log(null == undefined); // true para el operador de igualdad no estricta
```

### Errores con 0, NaN y cadenas vacías

los valores 0 , NaN y cadena vacía a pesar de ser considerados falsy en JavaScript, no son iguales entre sí, lo que puede llevar a conficiones.
Veamos la definición de cada uno para entender esta idea correctamente.

**0:** Representa el valor cero. Es un número, pero cuando se utiliza en una condición, se considera falsy.

```javascript
let numero = 0;
if (!numero) {
    console.log("El número es falsy");
}
```

**NaN:** Es un valor especial que representa "Not-a-Number". Resulta de operaciones aritméticas inválidas, como dividir cero entre cero. Es importante saber que a pesar de ser falsy, NaN no es igual a sí mismo, y para validar si es un valor NaN debe usarse la funcion isNaN(), esto se debe a que NaN es un número especial que representa una cantidad indefinida o invalida, y no se puede igualar a sí misma, ya que es un valor incierto o bien no comparable.

```javascript
let numeroInvalido = 0 / 0;
console.log(isNaN(numeroInvalido)); // true
console.log(numeroInvalido === NaN); // false, por que NaN no es igual a si mismo
console.log(NaN == NaN); //false no es posible comparar NaN con sigo misma.
```

**Cadenas vacías (""):** Es una cadena que no contiene ningún carácter. Aunque también es falsy, su comportamiento en comparación con otros valores falsy puede causar confusión.

```javascript
let cadena = "";
if (!cadena) {
    console.log("la cadena es falsy");
}
```

ahora abordemos las 3 diferencias comparándola entre ellas.

```javascript
console.log("" === 0); //false , por que no son lo mismo pese a pertenecer al conjunto de valores falsy.
console.log("" === NaN); //false, por que NaN no es comparable
console.log(0 === NaN); //false, por que NaN no es comparable

console.log("" == 0); // true por que la coerción implícita transforma "" y 0 en false explicito.
console.log("" == NaN); // false, por que NaN no es comparable
console.log(0 == NaN); // false, por que NaN no es comparable
```

### Manejo seguro de valores

Cuando hablamos de manejo seguro de valores, hacemos referencia a que el desarrollador debe de verificar que las variables y valores con los que trabajara este correctamente alineados y definidos con los tipos que se esperan para trabajar, esto ayudara a evitar errores de imprevistos.
