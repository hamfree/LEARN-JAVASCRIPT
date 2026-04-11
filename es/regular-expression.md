---
layout: editorial
chapter: 14
pageNumber: 119
description: Una expresión regular, a menudo abreviada como "regex", es una poderosa herramienta para la coincidencia de patrones y la búsqueda dentro de cadenas. Proporciona una forma concisa y flexible de buscar, unir y manipular texto según patrones específicos.
---

# Capítulo 14

## Expresión regular

Una expresión regular es un objeto que puede construirse con el constructor `RegEx` o escribirse como un valor literal encerrando un patrón entre una barra diagonal `(/)`. Las sintaxis para crear una expresión regular se muestran a continuación.

```javascript
// usando el constructor de expresión regular
new RegExp(patron[, banderas]);

// usando literales
/patron/modificadores
```

Las banderas son opcionales al crear una expresión regular usando literales. Un ejemplo de creación de un regular idéntico utilizando el método mencionado anteriormente es el siguiente.

```javascript
let re1 = new RegExp("xyz"); 
let re2 = /xyz/;
```

Ambas formas crearán un objeto regex y tendrán los mismos métodos y propiedades. Hay casos en los que podríamos necesitar valores dinámicos para crear una expresión regular; en ese caso, los literales no funcionarán y tendrán que ir con el constructor.

{% hint style="info" %}
En los casos en los que queremos que una barra diagonal sea parte de una expresión regular, tenemos que escapar de la barra diagonal `(/)` con una barra invertida `(\)`.
{% endhint %}

Los diferentes modificadores que se utilizan para realizar búsquedas que no distinguen entre mayúsculas y minúsculas son:

* `g` - búsqueda global (encuentra todas las coincidencias en lugar de detenerse después de la primera)

Ejemplo :

```javascript
const str = "Hello world, hello again!";
const regex = /hello/g;
const matches = str.match(regex);
// Si estás pensando en .match() lee esto 👇
// Es un método integrado en JavaScript que se utiliza para buscar una cadena que coincida con una expresión.
// Si se encuentra la coincidencia, devuelve una matriz de todas las coincidencias que se encontraron. Si no, el método .match() devuelve nulo.

console.log(matches); // ["Hello", "hello"]
```

* `i` - búsqueda que no distingue entre mayúsculas y minúsculas

Ejemplo :

```javascript
const str = "HeLlO WoRlD";
const regex = /hello/i;
const match = regex.test(str);
// El método '.test()' devuelve un valor booleano: 
// 'true' si se encuentra una coincidencia, y 'false' si la coincidencia no se encuentra.

console.log(match); // true
```

* `m` - coincidencia multilínea

Ejemplo :

```javascript
const str = "This is a\nmultiline string.";
const regex = /./mg;
const matches = str.match(regex);
// La bandera m se utiliza para hacer coincidir caracteres de nueva línea (\n).
// Esto significa que la expresión regular coincidirá con los 26 caracteres de la cadena.
// incluyendo el carácter de nueva línea.

console.log(matches.length); // 26
```

Los _corchetes_ se utilizan en una expresión regular para encontrar un rango de caracteres. Algunos de ellos se mencionan a continuación.

* `[abc]` - Encuentra cualquier carácter entre corchetes.

Ejemplo :

```javascript
const str = "The cat and the dog are both animals.";
const regex = /[abc]/g;
const matches = str.match(regex);

console.log(matches); // Matriz de todas las ocurrencias de a, b, y c

[
  'c', 'a', 'a',
  'a', 'b', 'a',
  'a'
]
```

* `[^abc]` - encontrar cualquier carácter, menos los que están entre corchetes

Ejemplo :

```javascript
const str = "The cat and dog.";
const regex = /[^abc]/g; // Coincide cualquier carácter que no sea 'a', 'b', o 'c'
const matches = str.match(regex);

console.log(matches); // Matriz de todas las ocurrencias de caracteres que no sean 'a', 'b', o 'c'

[
  'T', 'h', 'e', ' ',
  't', ' ', 'n', 'd',
  ' ', 'd', 'o', 'g',
  '.'
]

```

* `[0-9]` - encuentra cualquier dígito de los que están entre corchetes

Ejemplo :

```javascript
const str = "The price of the item is $25, but it may change to $30.";
const regex = /[0-9]/g; // Coincide con cualquier dígito desde el 0 al 9
const matches = str.match(regex);

console.log(matches); // Matriz con todas las ocurrencias de los dígitos

[
  '2', '5', '3', '0'
]

```

* `[^0-9]` - encuantra cualquier dígito, menos los que estaán entre corchetes

Ejemplo :

```javascript
const str = "The price is $25.";
const regex = /[^0-9]/g; // Coincide con cualquier carácter que no sea un dígito
const matches = str.match(regex);

console.log(matches); // Matriz de todas las ocurrencias de números que no son dígitos

[
  'T', 'h', 'e', ' ',
  'p', 'r', 'i', 'c',
  'e', ' ', 'i', 's',
  ' ', '$', '.'
]

```

* `(x|y)`- encuentre cualquiera de las alternativas separadas por |

Ejemplo :

```javascript
const str = "The words 'xylophone' and 'yellow' contain the letters 'x' and 'y'.";
const regex = /(x|y)/g; // Coincide con 'x' o 'y'
const matches = str.match(regex);

console.log(matches); // Matriz de todas las apariciones de 'x' o 'y'

[
  'x', 'y', 'y', 'x', 'x', 'y'
]

```

Los _metacaracteres_ son caracteres especiales que tienen un significado especial en la expresión regular. Estos caracteres se describen con más detalle a continuación:

| Metacaracter | Descripción                                                                     |
| ------------- | ------------------------------------------------------------------------------ |
| `.`           | Coincide con un solo carácter excepto nueva línea o un terminador              |
| `\w`          | Coincide con un carácter de palabra (carácter alfanumérico `[a-zA-Z0–9_]`)     |
| `\W`          | Coincide con un carácter que no es una palabra (igual que `[^a-zA-Z0–9_]`)     |
| `\d`          | Coincide con cualquier carácter de dígito (igual que `[0-9]`)                  |
| `\D`          | Coincide con cualquier carácter que no sea un dígito                           |
| `\s`          | Coincide con un carácter de espacio en blanco (espacios, tabulaciones, etc.)   |
| `\S`          | Coincide con un carácter que no sea un espacio en blanco                       |
| `\b`          | Coincidencia al principio/final de una palabra                                 |
| `\B`          | Coincide pero no al principio/final de una palabra                             |
| `\0`          | Coincide con un carácter `NULL`                                                |
| `\n`          | Coincide con un carácter de nueva línea                                        |
| `\f`          | Coincide con un carácter de avance de formulario                               |
| `\r`          | Coincide con un carácter de retorno de carro                                   |
| `\t`          | Coincide con un carácter de tabulación                                         |
| `\v`          | Coincide un carácter de tabulación vertical                                    |
| `\xxx`        | Coincide con un carácter especificado por un número octal `xxx`                |
| `\xdd`        | Coincide con un carácter especificado por un número hexadecimal `dd`           |
| `\udddd`      | Coincide con un carácter especificado por un número hexadecimal `dddd`         |

Las propiedades y métodos admitidos por RegEx se enumeran a continuación.

| Nombre        | Descripción                                                                                        |
| ------------- | -------------------------------------------------------------------------------------------------- |
| `constructor` | Devuelve la función que creó el prototipo del objeto RegEx                                         |
| `exec()`      | Prueba la coincidencia y devuelve la primera coincidencia; si no hay coincidencia, devuelve `null` |
| `global`      | Comprueba si el modificador `g` está configurado                                                   |
| `ignoreCase`  | Comprueba si el modificador `i` está configurado                                                   |
| `lastIndex`   | Especifica el índice en el que comenzar la próxima coincidencia.                                   |
| `multiline`   | Comprueba si el modificador m está configurado                                                     |
| `source`      | Devuelve el texto de la cadena.                                                                    |
| `test()`      | Prueba la coincidencia y devuelve `true` o `false`                                                 |
| `toString()`  | Devuelve el valor de cadena de la expresión regular.                                               |

{% hint style="working" %}
Un método `compile()` compila la expresión regular y está en desuso.
{% endhint %}

### Un ejemplo común de expresión regular

```javascript
let texto = "Las mejores cosas de la vida son gratis";
let resultado = /e/.exec(texto); // busca una coincidencia de e en una cadena
// resultado: e


let textoHolaMundo = "¡Hola mundo!";
// Busca "Hola"
let pattern1 = /Hola/g;
let result1 = pattern1.test(textoHolaMundo);
// result1: true

let pattern1String = pattern1.toString();
// pattern1String : '/Hola/g'
```

### Un ejemplo real de expresiones regulares en la verificación de códigos PIN

```javascript
const handleSubmit = (e) => {
  // Evitar el comportamiento de envío de formulario predeterminado
  e.preventDefault();

  // Definir una lista de códigos PIN válidos
  const validPincodes = [
    110001, 110002, 110003, 110004, 110005, 110006, 110007, 110008, 110009,
    110010, 110011, 110012, 110013, 110014, 110015, 110016, 110017, 110018,
    110019, 110020, 110021, 110022, 110023, 110050, 110051, 110056, 110048,
    110057, 110058, 110059, 110060, 110061, 110062, 110063, 110064
  ];

  // Convertir los códigos PIN válidos en cadenas
  const validPincodeStrings = validPincodes.map((pincode) => String(pincode));

  // Crea un patrón de expresión regular para que coincida con códigos PIN válidos
  const regexPattern = new RegExp(`^(${validPincodeStrings.join("|")})$`);

  // Obtiene el código PIN enviado desde el campo de entrada
  const submittedPincode = pincode; // Asegúrese de que el 'pincode' esté definido en otra parte

  // Comprueba si el código PIN enviado coincide con el patrón de código PIN válido
  if (regexPattern.test(submittedPincode)) {
    // Muestra un mensaje de éxito
    // ...
  } else if (submittedPincode === "") {
    // Muestra un mensaje de error para una entrada vacía
    // ...
  } else if (submittedPincode.length < 6) {
    // Muestra un mensaje de error para una longitud de código PIN no válida
    // ...
  }
}
```
