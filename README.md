# Evaluación Conjunta Web - P2
Sistema de preśtamo y devolución de libros usando principios de desarrollo de Aplicaciones Web Interactivas utilizando HTML, CSS y JavaScript

# Escenario

Una biblioteca digital necesita mejorar su sistema de gestión de préstamos y devoluciones de
libros. Actualmente, los usuarios pueden buscar libros, pero no hay una forma eficiente de reservarlos,
devolverlos o verificar su disponibilidad en tiempo real. Además, el sistema no cuenta con alertas para
recordar a los usuarios la fecha de devolución ni notificaciones sobre la disponibilidad de libros reservados

# Análisis

## Estructura del sistema de préstamos

**¿Cómo organizar y manipular los libros prestados usando
arrays y sus métodos (push, pop, shift, unshift, splice)?** 

Para organizar los libros prestados vamos a utilizar un array de objetos, donde cada objeto represente un libro prestado. Esto implica que usaremos también una clase para representar a los libros, la cual tendrá los siguientes atributos:

**`Libro`**
- `id`: un identificador único para cada libro.
- `titulo`: el título del libro.
- `autor`: el autor del libro.
- `fechaPublicacion`: la fecha de publicación del libro.

Y los objetos que contendrá el array de libros prestados serán objetos compuestos por los siguientes atributos:

- `libro`: un objeto de la clase `Libro` que representa al libro prestado.
- `fechaPrestamo`: la fecha en la que se prestó el libro.
- `fechaDevolucion`: la fecha en la que se debe devolver el libro.


Ahora, para manipular esta lista, vamos a utilizar los métodos `push` y `splice` de los arrays. El método `push` nos permitirá agregar un libro prestado a la lista, mientras que el método `splice` nos permitirá eliminar un libro prestado de la lista.

También existirá otra lista principal donde constarán todos los libros que estén disponibles, para su posterior consulta y manipulación.

## Filtrado y búsquedas dinámicas

**¿Cómo implementar filtros (filter) y búsqueda de libros por título,
autor o género?**

Para implementar filtros y búsquedas vamos a utilizar el método `filter` de los arrays. Este método nos permite filtrar los elementos de un array que cumplan con ciertas condiciones.

Más concretamente, si queremos buscar libros por título, autor o género, podemos utilizar el método `filter` para filtrar los libros que cumplan con alguna de estas condiciones. Para ello, podemos definir una función que tome como argumento un libro y devuelva `true` si cumple con la condición de búsqueda y `false` en caso contrario:

```js
function buscarPorTitulo(libro, titulo) {
  return libro.titulo.toLowerCase().includes(titulo.toLowerCase());
}

listaLibros.filter(libro => buscarPorTitulo(libro, "Harry Potter"));
```

## Interacción con el usuario

**¿Cómo mostrar la lista de libros disponibles y los libros prestados
usando manipulación del DOM (getElementById, querySelectorAll)?**

En nuestra estructura de HTML, vamos a tener dos listas `<ul>` debidamente identificadas, una para los libros disponibles y otra para los libros prestados. Cada libro estará representado por un elemento `<li>` que contendrá la información del libro, como el título, autor y fecha de publicación.

Vamos a poder acceder fácilmente a estos elementos utilizando los métodos `getElementById` y `querySelectorAll` para seleccionar los elementos que queremos manipular. Por ejemplo, para agregar un libro a la lista de libros prestados, podemos hacer lo siguiente:

```js
const listaPrestados = document.getElementById("lista-prestados");

listaPrestados.innerHTML += `
  <li id="libro-${libro.id}">
    <span>${libro.titulo}</span>
    <span>${libro.autor}</span>
    <span>${libro.fechaPublicacion}</span>
  </li>
`;
```

En este ejemplo, estamos directamente modificando el contenido HTML de la lista de libros ya que sabemos que todos sus elementos son `<li>`. Nótese que estamos asignando un identificador único a cada libro prestado para poder manipularlo posteriormente.

En el caso de querer eliminar el elemento de alguna de las listas, podemos usar el identificador anteriormente mencionado y eliminarlo del DOM:

```js
document.getElementById("libro-1").remove();
```

También podemos cambiar completamente el contenido de cualquiera de las listas de tal manera que podamos volver a renderizar las listas programáticamente. Si bien no será el enfoque más eficiente, es una forma sencilla de usar los métodos que hemos visto en clase.

## Alertas y recordatorios

**¿Cómo enviar recordatorios automáticos de devolución usando setTimeout o setInterval?**

Podemos utilizar la función `setTimeout` para programar una alerta que se ejecute en una fecha y hora determinada. Por ejemplo, si queremos enviar una alerta 24 horas antes de la fecha de devolución de un libro, podemos hacer lo siguiente:

```js
const libro = listaPrestados.filter(libro => libro.id === 1)[0];
const fechaDevolucion = new Date(libro.fechaDevolucion);
const fechaRecordatorio = new Date(fechaDevolucion.getTime() - 24 * 60 * 60 * 1000);

setTimeout(() => {
  alert(`Recuerda devolver el libro "${libro.titulo}" mañana.`);
}, fechaRecordatorio.getTime() - Date.now());
```

En pocas palabras, aquí establecemos un temporizador que se ejecutará en la fecha y hora especificadas.

##Eventos y Usabilidad 

**¿Cómo mejorar la experiencia del usuario con eventos (onclick, onchange, onmouseover, onmouseout, onfocus, onblur)?**
Lo que podemos hacer es asignar acciones en botones utilizando el onclick, añadir efectos visuales con el onmouseover, monitorear los cambios en campos de entrada con el onchange y mejorar la accesibilidad al resaltar elementos con el onfocus 

• onclick: Asignar acciones a botones, como reservar o devolver libros. Por ejemplo, al hacer clic en "Reservar", el estado del libro cambia y se actualiza la lista visual.
•  onmouseover y onmouseout: Añadir efectos visuales al pasar el ratón sobre elementos interactivos, como botones que cambian de color o muestran información adicional.
•  onchange: Monitorear cambios en campos de entrada (como filtros de búsqueda) para actualizar dinámicamente la lista de libros.
•  onfocus y onblur: Mejorar la accesibilidad al resaltar elementos seleccionados o validar datos en tiempo real.

```js
      item.onmouseover = () => (item.style.backgroundColor = "lightblue");
      item.onmouseout = () => (item.style.backgroundColor = "");
      item.onclick = () => alert(`Reservaste el libro: "${libro.titulo}"`);
      contenedor.appendChild(item);
      function resaltar(elemento) {
          elemento.style.border = "2px solid blue";
        }
      
        function quitarResaltado(elemento) {
          elemento.style.border = "";
        }
```
##Funciones Avanzadas 
**¿Cómo usar funciones autoejecutables, anónimas, y async/await para manejar procesos asíncronos?

Uso de async/await, funciones anónimas y autoejecutables para modularidad y manejo eficaz de asincronía
•  Se agregó una función autoejecutada para inicializar el sistema automáticamente al cargar.
•  Se implementaron funciones async/await para manejar retrasos simulados al procesar reservas, mejorando la experiencia del usuario.

```js
 
    (function () {
      console.log("Sistema de biblioteca inicializado automáticamente.");
    })();
   
    async function procesarReserva(idLibro) {
      console.log("Procesando reserva...");
      await new Promise((resolve) => setTimeout(resolve, 2000)); // Simula 2 segundos de espera
      console.log(`Reserva confirmada para el libro con ID: ${idLibro}`);
    }
    
    procesarReserva(1);

```

##Simulacion de procesos asincronicos 

**¿Cómo implementar la reserva y devolución de libros usando promesas y setTimeout para simular tiempos de espera?

•	Reservas: Se implementó un retraso de 2 segundos al reservar un libro usando setTimeout dentro de una Promesa.
•	Devoluciones: Se simuló un tiempo de procesamiento de 3 segundos antes de actualizar el estado del libro como disponible.
•	Notificaciones: Se usaron Promesas para notificar al usuario cuando un libro reservado vuelva a estar disponible, con un retraso simulado de 5 segundos.




