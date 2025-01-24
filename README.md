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

