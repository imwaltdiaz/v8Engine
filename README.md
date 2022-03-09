# Curso de JavaScript Engine (V8) y el Navegador

![alt text](https://static.platzi.com/media/user_upload/image001-3d079334-b097-4b4d-8162-071438354107.jpg)

## JavaScript Engine

### ¿Cómo funciona el JavaScript Engine?

https://dev.to/lydiahallie/javascript-visualized-the-javascript-engine-4cdf

El motor de V8 es un interpete entre JS y la computadora, es decir, transporta esto entre source code to machine code, lo pasa de JS a ceros y unos

Este proceso se llama Just in time compiler

Compilación en tiempo real

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--Xs5OQmGX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/pv4y4w0doztvmp8ei0ki.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--ID8wDIAy--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/bic727jhzu0i8uep8v0k.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--6IHw1BUH--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/sgr7ih6t7zm2ek28rtg6.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--HlXdsZRx--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/i5f0vmcjnkhireehicyn.gif)

### V8, el JavaScript Engine de Chrome

V8 es el motor de javaScript de Chrome, cada navegador tiene un motor diferente

Pero V8 es el motor estándar que ayuda a que sea más rápido y lo estan copiando otros navegadores

V8 nace para que google maps funcione de manera óptima, corre muchas cosas a la vez, y esto ayudará a que JS corra mas rápido y cause una mejor experiencia

Y muchos navegadores se empiezan a enfocar en aplicaciones con mayor interacción aprovechando a V8 y que JS pueda crear aplicaciones web muy robustas

node es la parte con la que puedes correr js desde el backend que corre a traves de V8 

JS corre en el navegador pero no es interpretado por el navegador.

### Profundizando en el Engine

![Alt Text](https://static.platzi.com/media/user_upload/js-engine-complete%402x-285ce1e4-709b-4842-b4e4-90ec6d940f9f.jpg)

Una vez que se corre el JS, el navegador primero creau n entorno global, como un objeto principal al que se le llame window

El entorno global tiene
- Un Global Object
- Una variable *this*
- Un Outer Environment

En este contexto, this en el entorno global es igual a este objeto global y es igual a window

Una vez generado ese entorno global, se genera un contexto de ejecución donde se corre el código y apila las tareas una por una

El motor de JS genera un Parser que le ayuda a encontrar keywords importantes

Lo pasa al AST (Abstrack Syntax Tree), un arbol de sintaxis abstracto (https://astexplorer.net/)

El arbol es como una interpretación del JSON del código en neto que también esta en el 

Y las variables y funciones las empieza a transformar en un arbol sintaxico para luego mostrarlo en el navegador

Luego lo lleva a un Interpreter para interpretarlo y lo pasa a Bytecode, un lenguaje para que entienda lamaquina, no es tan bajo como binario o machine code pero lo intiende la maquina

Si el interpreter se da cuenta que puede optimizar cosas como variables repetidas o alguna función que pueda optimizar, entra un Profiler (Monitor) que ayuda a optimizar ese código, lo compila y lo regresa como Optimized code

En este paso del Interpreter al Progiler (Monitor) al Compiler sucede el Hoisting

Un caso de a veces error por una afan de ayudarnos rompe cosas, solo sucede con variables y funciones que una vez se llaman

![Alt Text](https://static.platzi.com/media/user_upload/Engine%20V8-7ee73612-fd87-42db-8b1d-2ec0d21d0d97.jpg)

![Alt Text](https://static.platzi.com/media/user_upload/bytecode-machine-code-dc786db8-d04e-488b-b96b-e9b385fdb33d.jpg)

### Ejemplo de Objeto global y hoisting

Un archivo vacio de Js, justo cuando el enigne hace su magia, el navegador genera un window, y la variable this

Aunque no haya nada en el documento js, ya hay estas apis, el objeto window y la variable this para trabajar

Si le das en consola a window, te mostrará todas las api que te las pone el navegador

Una vez que llame alguna, el navegador va a saber que hacer, esto viene directamente enel objeto window antes que se corra JS 

this dirá que es window

this es una variable de referencia a window, si verificas con window == this te dirá true

```js
console.log(nombre)
apellido()

var nombre = "Walter"
function apellido() {
    console.log("Diaz")
}
```
Te botará 
> undefined 

> Diaz

Esto será el hoisting, JS intentará ver lo que quieres decir y te ayuda con ciertas cosas

Al leer nombre no sabe lo que sucede, y enel compiler genera una nueva variable a la que le llama nombre y le asigna el undefined

Y respecto a funciones, tenemos la facilidad de primero mandar a llamar las funciones antes de hacerlas

```js
var nombre = undefined

console.log(nombre)
apellido()
//Sabe que es una funcion, la almacena en memoria y luego la ejecuta

// var nombre = "Walter"  Y esto no sucederá porque ya está el valor de undefined
function apellido() {
    console.log("Diaz")
}
```

Pero si usamos const...

```js
console.log(nombre)
apellido()

const nombre = "Walter"
function apellido() {
    console.log("Diaz")
}
```
Te botará 
> Uncaught ReferenceError: nombre is not defined

o tmb

> Cannot acces 'nombre' before initialization

Entonces tienes que inicializar primero al a variable para acceder a ella

No siempre vas a tener control de lo que se va a cambiar

Por eso procura como buena practica asignar primero las variables y luego llamalas o ejecuta las funciones

Resumen rápido:

– Las funciones y variables se almacenan en la memoria para un contexto de ejecución antes de ejecutar nuestro código. A esto se le llama Hoisting.

– Las funciones se almacenan con una referencia a la función completa, las variables con la palabra clave var con el valor de undefined y las variables con la palabra clave let y const se almacenan sin inicializar.

- Cuando comparamos window con this y da true, ese true NO lo da porque sean objetos iguales y tengan la información, ese true lo da porque ambas variables son EL MISMO objeto, es decir, ambas variables tienen la misma referencia de memoria, ambas variables están apuntando a la misma referencia en memoria de la computadora, por lo que, si cambias algo en una, también se cambiará en otra

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--lLfiCbTX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif7.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--vRtKMspn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif8.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--zvlaEaAo--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif9.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--nk1taOke--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif16.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--2nai6XPr--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif17.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--VVPlWhGC--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif18.gif)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--LGEaCMkS--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif12.gif)

## Código de Ejecución

### Memory Heap

Código de Ejecución

Hablamos del comportamiento de JS y de su sincronismo, esta característica se llama Single thread (Synchronous) donde JS solo puede hacer una cosa a la vez 

El Memory Heap es donde se van a almacenar los valores de las variables y de las funciones y luego como se van a llamar en el Call Stack, y primero se llama al Objeto Global (Global Object)

El engine a leer una variable, le designa un espacio para guardar esa variable y su valor 

El Memory Heap es como una repisa para lamacenar datos, esto no se guarda de forma numérica o lineal, no sabremos donde está exactamente, para que cuando se ejecute el código y llames a una variable, irá a donde estará guardado y los mostrará

```js
const carro = {
    marca: "Toyota",
    modelo: "2020"
}
//Y si lo llamas...
carro
{marca: "Toyota", modelo: "2020"}
```

**Dato:**
Los objetos en JS (objetos, arrays, funciones y básicamente todo lo que no sea un valor primitivo) se almacenan en la parte de memoria que de llama Memory Heap. Los valores primitivos son almacenados en el Call Stack, dentro del Scope (Contexto de Ejecución de la función que tenga acceso a esa variable). Acceder al Call Stack es mucho más rápido que al Heap. Además, en el Call Stack también se guardan las referencias, “como si fueran valores primitivos”. Cuando se asigna una variable a otra y esta apunta a un objeto, se copia la referencia, como si fuera un valor primitivo. Si el objeto tiene atributos como un número por ejemplo, este se guarda en la posición de memoria reservada para ese objeto. Los objetos también pueden tener más objetos dentro. En ese caso, dentro de la posición de memoria de ese objeto se va a guardar una referencia a otra posición de memoria

**Resumen:**
Memory Heap

- Donde se almacena los valores de las variables y las funciones

- Se destina un espacio en memoria para las variables.

- La información en el memory heap, No se guarda de manera lineal

![Alt Text](https://static.platzi.com/media/user_upload/DeepinScreenshot_Seleccionar%20%C3%A1rea_20200323110908-435fffa6-c8d4-4b18-9e3d-3fd27b76f2a8.jpg)

> Ojo

Los valores primitivos y los valores por referencia son almacenados en Stack.
Los objetos son almacenados en Heap

### Call Stack

Como se van a ejecutar las tarreas

Las tareas se van a apilar de abajo hacia arriba

Tenemos el Objeto Global primero y luego se ve a llamar las siguientes tareas

Si una tarea llama a otra, esta se va a poner arriba 

Esto se refiere a sincronia, y como JS solo puede hacer una cosa a la vez

Una vez que se va el objeto global como 1era tarea, va a por la 2da tarea, luego 3era, 4ta y así

Al final quedará la pila de tareas vacía

Vamos a Snippets en Sources dentro de Web Tools

Le damos a new snippet

Y ahi tendremos el call stack de como js y el navegador trabjaar als funciones y variables paso a paso

Tenemos el scope para la inicializacion

Y los breakpoints

Inicializamos

En el call stack estará un (anonymous) parte del objet global, como primera tarea la pantalla de window

Luego analizará las variables y constantes y trabajará con ellos

Ahora arriba de anonymous estará la tarea de calcular

luego en el scope veremos como trabaja con la variable y el this es window

Cuando hay una funcion que no puede hacer, manda al stakc del call la funcion que debe resolver 

Una vez resuewlta la quita, luego queda la siguiente función, luego resuelve el anonymous y listo

![Alt Text](https://miro.medium.com/max/783/1*E3zTWtEOiDWw7d0n7Vp-mA.gif)

Link: https://platzi.com/clases/1798-javascript-navegador/25685-call-stack/


**Ayuda:** https://www.youtube.com/watch?v=ygA5U7Wgsg8


**Guia de Sacha**

Cada vez que se llame una función se creara un registro y se la va a poner en la pila de ejecución, por cada funcion nueva se pondrá sobre el registro anterior

Cuando termine la ultima funcion, la sacará y continuará con el registro de abajo

Cuando hay un error, la ocnsolate botará el error como sucedió en el call stack para que sepas donde pasó

Esta tal cual el orden del call stack, esto se conoce ocmo el stacktrace, la secuencia de llamadas que se dieron hasta que hubo un error inesperado

Scope son las variables que se pueden acceder cuando se esta ejecutando una funcion

this es el objeto dueño de la función y el valor determina el contexto de la función

Window en nodejs es global

Cuando ejecutas una funcion general como console.log se asume que es al objeto window

Entonces el scope local trabja sobre el this y el scope global trabaja sobre el window o global

Las funciones salen de la pila cuando se terminan de ejecutar

Cada motor defina la cantidad de tareas que puede recibir

Lectura adicional: https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec

### Garbage Collection

Hay lenguajes donde debes recolectar la basura de cosas que no usas

JS te ayuda con ello

Mark and Sweep

Se hace un Mark para verificar lo que se llama y luego un sweep para eliminar lo que no

![Alt Text](https://i.stack.imgur.com/shG8h.gif)

Por ejemplo al reasignar valores, el valor antiguo se elimina y se queda la variable actual

Hay momentos donde esto se puede crashear con funciones o loop infinito asi que hay que tener cuidado

**Garbage Collection:** limpia la memoria de los datos no utilizados para no sobrecargarla y seguir trabajando sin problemas.

### Stack overflow

Que pasa si hay una fusión o algo que sobrellena la pila?

A esto se le llama stack overflow, con esto crasheas el navegador y se cerraba

Chrome ahora cuando detecta un gran numero de peticiones deja de ejecutar ese código

Recursion es cuando una función se llama asi misma, esto a veces puede causar un stackoverflow

Te botará la alerta de **Maximum call stack size exceeded**

**Resumen:**
El stack overflow se genera cuando el call stack se llena completamente (pila de tareas).

Esto pasa cuando se genera o se trabaja con bucles infinitos, recurcividad y funciones.

Entonces este entra en stack overflow , tenemos que tener cuidado de ocacionar estos stack

![Alt Text](https://miro.medium.com/max/632/1*xjhPcM027gMRApCCMdRUFw.gif)

### JavaScript Runtime

Por como va a entrando va una cosa a la vez, si una tarea toma mas tiempo, parotodo y hago eso

![Alt Text](https://aseemrb.me/images/weird-awesome-javascript/chrome.png)

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--BLtCLQcd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif14.1.gif)

### Asincronía

JS corre una cosa a la vez, como hacerlo asincronico?? 

En this verás todas las API que el navegador te da

Lista de funciones: https://developer.mozilla.org/en-US/docs/Web/API

Con funciones como el setTimeOut dice que no le toca y se lo deja al navegador, JS sigue ocn lo suyo, el navegador trabjaa con esa funcion y la pone en un callback queue y al momento qu esté vció lo del call stack, va lo que acabó el navegador

Y esto se da por un event loop que va preguntando al call stack si ya acabo, y en el momento que acabó, el callback queue le pasa la función 1 al call stack y luego la 2 y asi

Lo que le toca al navegador le queda al navegador y el call stack termina con lo suyo

Al final recién va lo del navegador que lo hace asíncrono

El evnet loop esta entre el call stack y el callback queue para enviar lo del queue al stack

Aunque no tarde el timeout nada, sea 0, igual irá al final la asincronia porque irá al final del call stack debido a que JS ya estará trabajando en lo demás

El navegador trabajará de forma paralela sin importar el tiempo

**Taquería DeGranda presenta a:**
.
🌮 - call stack: el taquero (órdenes rápidas)
👨‍🍳 - web APIs: la cocina
🌯 - callback queue : las órdenes preparadas
💁‍♂️ - event loop : el mesero
.
a que quedó súper claro el JS Runtime y cómo funciona el asincronismo!? 🤪

![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--BLtCLQcd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif14.1.gif)

Creo que aquí faltó hablar sobre las promesas y las “microtasks queues”, recomiendo esta clase del curso profesional de JS para que vean ese punto.
https://platzi.com/clases/1642-javascript-profesional/22169-event-loop/
Cabe resaltar que las “Microtasks queues” tienen preferencia ante la “Callback queue”

**Entonces:**
```js
console.log('taco 1')
console.log('taco 2')
console.log('taco 3')
setTimeout(()=>{
    console.log('torta 1')
},1000)
console.log('taco 4')
setTimeout(()=>{
    console.log('torta 2')
},500)
setTimeout(()=>{
    console.log('torta 3')
},0)

// Te botará

// taco 1
// taco 2
// taco 3
// taco 4
// torta 3
// torta 2
// torta 1

```

> Gracias por todo, este es el cierre del curso! :) 