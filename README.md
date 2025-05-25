<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sorpresa Especial</title>
<style>
  body {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #f0f0f0;
    margin: 0;
    font-family: 'Arial', sans-serif;
    overflow: hidden; /* Para evitar barras de scroll si los mensajes son largos */
    perspective: 1000px; /* Para la animación 3D de explosión */
  }

  .heart-container {
    position: relative;
    cursor: pointer;
  }

  .heart {
    width: 100px;
    height: 90px;
    position: relative;
    background-color: #8A2BE2; /* Violeta */
    transform: rotate(-45deg);
    transition: transform 0.5s ease-out, opacity 0.5s ease-out;
    opacity: 1;
  }

  .heart::before,
  .heart::after {
    content: "";
    width: 100px;
    height: 100px;
    background-color: #8A2BE2; /* Violeta */
    border-radius: 50%;
    position: absolute;
  }

  .heart::before {
    top: -50px;
    left: 0;
  }

  .heart::after {
    top: 0;
    left: 50px;
  }

  .heart.exploded {
    transform: rotate(-45deg) scale(3) translateZ(300px); /* Animación de "explosión" */
    opacity: 0;
  }

  .small-heart-container {
    margin-top: 20px; /* Espacio después del primer mensaje */
    display: none; /* Oculto inicialmente */
    text-align: center;
  }

  .small-heart {
    width: 50px;
    height: 45px;
    /* Reutilizamos los estilos del corazón grande pero más pequeño */
    position: relative;
    background-color: #8A2BE2; /* Violeta */
    transform: rotate(-45deg);
    display: inline-block; /* Para centrar si es necesario */
    cursor: pointer;
    transition: transform 0.3s ease;
  }

  .small-heart:hover {
    transform: rotate(-45deg) scale(1.1);
  }

  .small-heart::before,
  .small-heart::after {
    content: "";
    width: 50px;
    height: 50px;
    background-color: #8A2BE2; /* Violeta */
    border-radius: 50%;
    position: absolute;
  }

  .small-heart::before {
    top: -25px;
    left: 0;
  }

  .small-heart::after {
    top: 0;
    left: 25px;
  }

  .message {
    font-size: 24px;
    color: #333;
    margin-top: 20px;
    text-align: center;
    opacity: 0;
    transition: opacity 0.5s ease-in;
    display: none; /* Oculto inicialmente */
    padding: 10px;
  }

  .message.visible {
    opacity: 1;
    display: block;
  }

</style>
</head>
<body>

<div class="heart-container" id="heartContainer">
  <div class="heart" id="mainHeart"></div>
</div>

<div class="message" id="message1">te amo pendeja</div>
<div class="small-heart-container" id="smallHeartContainer">
  <div class="small-heart" id="smallHeart"></div>
</div>
<div class="message" id="message2">Tonny es el mejor</div>

<script>
  const mainHeart = document.getElementById('mainHeart');
  const heartContainer = document.getElementById('heartContainer');
  const message1 = document.getElementById('message1');
  const smallHeartContainer = document.getElementById('smallHeartContainer');
  const smallHeart = document.getElementById('smallHeart');
  const message2 = document.getElementById('message2');

  let firstClickDone = false;
  let secondClickDone = false;

  // Evento para el corazón principal
  heartContainer.addEventListener('click', () => {
    if (firstClickDone || secondClickDone) return; // Evitar múltiples clics si ya se hizo la acción

    firstClickDone = true;
    mainHeart.classList.add('exploded');

    // Esperar a que termine la animación de explosión
    setTimeout(() => {
      heartContainer.style.display = 'none'; // Ocultar el corazón grande y su contenedor
      message1.classList.add('visible');
      smallHeartContainer.style.display = 'block'; // Mostrar contenedor del corazón pequeño
    }, 500); // Coincide con la duración de la transición de explosión
  });

  // Evento para el corazón pequeño
  smallHeart.addEventListener('click', () => {
    if (!firstClickDone || secondClickDone) return; // Solo activar si el primer paso se completó y este no

    secondClickDone = true;
    // Opcional: Ocultar el corazón pequeño o hacerlo menos prominente
    // smallHeartContainer.style.opacity = '0.5';
    message2.classList.add('visible');
  });

</script>

</body>
</html>
# ...
