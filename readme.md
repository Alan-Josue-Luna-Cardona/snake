Adaptación del código para usar una cola con arreglo

Inicialización de la serpiente

La serpiente se inicializa como un arreglo con un solo elemento, que representa la cabeza:

let snake = [{ x: 9 * box, y: 9 * box }];

Aquí, snake es un arreglo que actúa como una cola. Inicialmente, solo tiene un elemento: la cabeza de la serpiente.

Movimiento de la serpiente

Cada vez que la serpiente se mueve, hacemos dos cosas:

Añadimos una nueva cabeza: Calculamos la nueva posición de la cabeza basada en la dirección actual y la añadimos al principio del arreglo usando unshift.

Eliminamos la cola: Si la serpiente no ha comido comida, eliminamos el último elemento del arreglo usando pop.

const newHead = { x: snakeX, y: snakeY }; // Nueva cabeza

if (snakeX === food.x && snakeY === food.y) {
    // Si come la comida, no eliminamos la cola
    food = { x: Math.floor(Math.random() * 20) * box, y: Math.floor(Math.random() * 20) * box };
} else {
    snake.pop(); // Elimina el último elemento (cola)
}

snake.unshift(newHead); // Añade la nueva cabeza al principio

unshift(newHead): Añade la nueva cabeza al principio del arreglo. Esto simula el movimiento de la serpiente hacia adelante.

pop(): Elimina el último elemento del arreglo, que representa la cola de la serpiente. Esto asegura que la serpiente no crezca indefinidamente a menos que coma comida.

Crecimiento de la serpiente

Cuando la serpiente come la comida, no eliminamos la cola (pop no se ejecuta), lo que hace que el arreglo crezca en longitud. Esto simula el crecimiento de la serpiente.

if (snakeX === food.x && snakeY === food.y) {
    // Generar nueva comida
    food = { x: Math.floor(Math.random() * 20) * box, y: Math.floor(Math.random() * 20) * box };
} else {
    snake.pop(); // Solo elimina la cola si no come
}

Detección de colisiones

Para detectar si la serpiente choca consigo misma, recorremos el arreglo snake y verificamos si la nueva cabeza (newHead) coincide con alguna parte del cuerpo.

function collision(head, array) {
    for (let i = 0; i < array.length; i++) {
        if (head.x === array[i].x && head.y === array[i].y) {
            return true; // Hay colisión
        }
    }
    return false; // No hay colisión
}

Visualización de la serpiente

El arreglo snake se utiliza para dibujar la serpiente en el canvas. Recorremos el arreglo y dibujamos cada segmento:

for (let i = 0; i < snake.length; i++) {
    ctx.fillStyle = (i === 0) ? 'green' : 'lightgreen'; // Cabeza verde, cuerpo claro
    ctx.fillRect(snake[i].x, snake[i].y, box, box); // Dibuja cada segmento
    ctx.strokeStyle = 'darkgreen';
    ctx.strokeRect(snake[i].x, snake[i].y, box, box);
}

Resumen de cómo funciona la cola con arreglo

Añadir elementos: Usamos unshift para añadir la nueva cabeza al principio del arreglo.

Eliminar elementos: Usamos pop para eliminar la cola del arreglo cuando la serpiente no come.

Crecimiento: Si la serpiente come, no eliminamos la cola, lo que hace que el arreglo crezca.

Colisiones: Verificamos si la nueva cabeza choca con algún segmento del cuerpo recorriendo el arreglo.

Ventajas de usar una cola con arreglo

Simplicidad: Los arreglos en JavaScript son fáciles de usar y manipular.

Eficiencia: Para este caso específico, el uso de unshift y pop es eficiente porque la longitud de la serpiente no es extremadamente grande.

Claridad conceptual: El código refleja claramente el comportamiento de una cola, lo que facilita su comprensión.