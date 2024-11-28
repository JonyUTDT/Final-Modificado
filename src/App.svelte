<script>
  // Función para inicializar el componente de Flourish y tomar el script que nos permite hacer el scrolly gratis!
  import { onMount } from 'svelte';
  import * as d3 from "d3";

  let drivers = [];
  let currentDriver = null;
  let questions = [];
  let correctAnswers = 0;
  let totalQuestions = 6; // Número total de preguntas
  let score = 0;
  let searchQuery = "";
  let allQuestionsAnswered = false;
  let isActive =false;


  // Cargar datos del CSV
  async function loadDrivers() {
      drivers = await d3.csv("/src/data/F1DriversDataset.csv", (d) => ({
          name: d.Driver,
          nationality: d.Nationality,
          championships: +d.Championships || 0,
          seasons: d.Seasons ? d.Seasons.split(",") : [],
          fastestLaps: +d.Fastest_Laps || 0,
          podiums: +d.Podiums || 0,
          raceWins: +d.Race_Wins || 0,
      }));
  }

  // Generar preguntas para un piloto
  function generateQuestions(driver) {
      currentDriver = driver;
      questions = [
          {
              question: `¿Cuál es la nacionalidad de ${driver.name}?`,
              correct: driver.nationality,
              options: getRandomOptions(driver.nationality, drivers.map((d) => d.nationality)),
              selected: null,
          },
          {
              question: `¿Cuántos campeonatos ganó ${driver.name}?`,
              correct: `${driver.championships}`,
              options: getRandomOptions(
                  `${driver.championships}`,
                  drivers.map((d) => `${d.championships}`)
              ),
              selected: null,
          },
          {
              question: `¿Cuántas vueltas rápidas tiene ${driver.name}?`,
              correct: `${driver.fastestLaps}`,
              options: getRandomOptions(
                  `${driver.fastestLaps}`,
                  drivers.map((d) => `${d.fastestLaps}`)
              ),
              selected: null,
          },
          {
              question: `¿Cuántos podios logró ${driver.name}?`,
              correct: `${driver.podiums}`,
              options: getRandomOptions(
                  `${driver.podiums}`,
                  drivers.map((d) => `${d.podiums}`)
              ),
              selected: null,
          },
          {
              question: `¿En cuántas carreras ganó ${driver.name}?`,
              correct: `${driver.raceWins}`,
              options: getRandomOptions(
                  `${driver.raceWins}`,
                  drivers.map((d) => `${d.raceWins}`)
              ),
              selected: null,
          },
          {
              question: `¿En qué temporada debutó ${driver.name}?`,
              correct: `${driver.seasons[0] || "N/A"}`,
              options: getRandomOptions(
                  `${driver.seasons[0] || "N/A"}`,
                  drivers.flatMap((d) => d.seasons)
              ),
              selected: null,
          },
      ];
      allQuestionsAnswered = false;
      correctAnswers = 0;
      score = 0;
  }

  // Generar opciones aleatorias
  function getRandomOptions(correct, pool) {
      const incorrectOptions = pool.filter((opt) => opt !== correct);
      const randomOptions = [];
      while (randomOptions.length < 2) {
          const randomOption = d3.shuffle(incorrectOptions)[0];
          if (!randomOptions.includes(randomOption)) {
              randomOptions.push(randomOption);
          }
      }
      return d3.shuffle([correct, ...randomOptions]);
  }

  // Manejar respuesta
  function handleAnswer(selected, questionIndex) {
      const question = questions[questionIndex];
      if (question.selected === null) {
          question.selected = selected;

          if (selected === question.correct) {
              correctAnswers++;
          }
          if (questions.every((q) => q.selected !== null)) {
              allQuestionsAnswered = true;
              score = Math.round((correctAnswers / totalQuestions) * 100);
          }
      }
  }

  onMount(loadDrivers);

  // Array para guardar la data de cada slide. Cambiar cada uno con el epígrafe específico para cada slide.
  // Posiciones pilotos y eso
  const slides = [
    "Texto slide 1. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 2. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 3. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
  ]

  // Posiciones escuderias y eso
  const slides2 = [
    "Texto slide 1. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 2. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
  ]

  // Circuito USA
  const slides3 = [
    "Texto slide 1. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 2. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 3. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
  ]

  // Circuito Mexico
  const slides4 = [
    "Texto slide 1. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 2. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 3. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
  ]

  // Circuito Brasil
  const slides5 = [
    "Texto slide 1. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 2. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
    "Texto slide 3. Fusce quis augue et tortor interdum bibendum. Nam dolor elit",
  ]

  function loadFlourishScrolly() {
    const script = document.createElement('script')
    script.src = "https://cdn.flourish.rocks/flourish-scrolly-v3.1.0.min.js"
    script.type = "text/javascript"
    script.onload = () => initFlourishScrolly()
    document.body.appendChild(script)
  }


  onMount(() => {
    loadFlourishScrolly()
  });

  let currentImage = "./public/images/Posiciones Pilotos.png";
const secondImage = "./public/images/imagentodasposiciones.png"; // Cambiar por la ruta de la otra imagen

function toggleImage() {
  currentImage = currentImage === "./public/images/Posiciones Pilotos.png" 
    ? secondImage 
    : "./public/images/Posiciones Pilotos.png";
}

let currentImage2 = "./public/images/Posiciones Escuderias.png";
const secondImage2 = "./public/images/Constructorespos.png"; // Cambiar por la ruta de la otra imagen

function toggleImage2() {
  currentImage2 = currentImage2 === "./public/images/Posiciones Escuderias.png" 
    ? secondImage2 
    : "./public/images/Posiciones Escuderias.png";
}
</script>

<body>
<!-- Encabezado-->
<div class="Encabezado" style="width: 100%; margin: 0%; padding: 0;">
  <img 
    src="./public/images/Header.png" 
    alt=""
  >
</div>

<!-- Enters para espaciado -->

<br>
<br>

<!-- Posiciones Pilotos -->
<div class="Posiciones-Pilotos">
  <h1 style="text-align: center; font-family:anta">Posiciones pilotos</h1>
  <img 
    src={currentImage} 
    alt="Posiciones Pilotos"
    class="centered-image" 
  >
  <div class="button-container">
    <button class="red-button" on:click={toggleImage}>
      Ver más
    </button>
  </div>
</div>

<!-- Enters para espaciado -->

<br>
<br>
<br>
<br>
<br>

<!-- Sueldos Pilotos y los mas Ganadores --> 
 <div class="Graficos-flourish">
 <div class="Sueldos-Maximos-Ganadores" style="display: flex; gap: 1rem;">
  <div class="Mas Campeones" style="flex: 1;">
    <div class="flourish-embed flourish-bar-chart-race" data-src="visualisation/20513307">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript><img src="https://public.flourish.studio/visualisation/20513307/thumbnail" width="100%" alt="bubble-chart visualization" /></noscript>
    </div>
  </div>  
  <div class="Sueldos" style="flex: 1;">
    <div class="flourish-embed flourish-bubble-chart" data-src="visualisation/20393188">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript><img src="https://public.flourish.studio/visualisation/20393188/thumbnail" width="100%" alt="bubble-chart visualization" /></noscript>
    </div>
  </div>
</div>
<!-- Enters para espaciado -->
  <br>
  <br>
  <br>
  <br>
  <div class="Leyenda escuderias" style="text-align: center;">
    <img 
      src="./public/images/Colores Escuderias.png" 
      alt="Leyenda"
      style="width: 50%; object-fit: contain;"
    >
  </div>
</div>

<!-- Enters para espaciado -->

<br>
<br>
<br>

<div class="container">
  {#if drivers.length > 0}
      <div class="game-container">
          <h2>Cuanto sabes de tu piloto favorito?</h2>
          <input 
              type="text" 
              bind:value={searchQuery} 
              placeholder="Buscar piloto..." 
              class="search-input" 
          />
          <ul class="driver-list">
              {#each drivers.filter(driver => driver.name.toLowerCase().includes(searchQuery.toLowerCase())) as driver}
                  <li on:click={() => generateQuestions(driver)}>{driver.name}</li>
              {/each}
          </ul>
          {#if questions.length > 0}
              <div class="questions-container">
                  <h3>¿Cuánto sabes de {currentDriver.name}?</h3>
                  {#each questions as question, index}
                      <div class="question">
                          <p>{index + 1}. {question.question}</p>
                          <div class="options">
                              {#each question.options as option}
                                  <button 
                                      on:click={() => {
                                        handleAnswer(option, index)
                                        isActive = true
                                        console.log(isActive)
                                      }}
                                      class={
                                          allQuestionsAnswered
                                              ? (option === question.correct ? "correct" : option === question.selected ? "incorrect" : "default")
                                              : question.selected !== null && option === question.selected
                                              ? (option === question.correct ? "correct" : "incorrect")
                                              : "default"
                                      }
                                      style="background-color: {question.selected !== null ? 'red;' : '#f0f0f0;'}"

                                      disabled={question.selected !== null}
                                  >
                                      {option}
                                  </button>
                              {/each}
                          </div>
                      </div>
                  {/each}
                  <!-- Visualización del círculo de puntuación -->
                  {#if allQuestionsAnswered}
                      <div class="score-container">
                          <svg width="150" height="150" viewBox="0 0 36 36">
                              <path
                                  d="M18 2a16 16 0 1 1 0 32 16 16 0 1 1 0-32"
                                  fill="none"
                                  stroke="#e6e6e6"
                                  stroke-width="4"
                              />
                              <path
                                  d="M18 2a16 16 0 1 1 0 32 16 16 0 1 1 0-32"
                                  fill="none"
                                  stroke="#007bff"
                                  stroke-width="4"
                                  stroke-dasharray={`${score}, 100`}
                                  stroke-linecap="round"
                                  transform="rotate(-90 18 18)"
                              />
                          </svg>
                          <p class="score-text">{score}%</p>
                      </div>
                  {/if}
              </div>
          {/if}
      </div>
  {:else}
      <p>Cargando datos...</p>
  {/if}
</div>
 
<!-- Enters para espaciado -->
 
<br>
<br>
<br>

<!-- Posiciones Escuderias y Titulos-->
<div class="Posiciones-Escuderias-Titulos">
  <h1 style="text-align: center;">Posiciones escuderias</h1>
  <div class="Posiciones Escuderias">
    <img 
    src={currentImage2} 
    alt="Posiciones Escuderias"
    class="centered-image" 
  >
  <div class="button-container">
    <button class="red-button" on:click={toggleImage2}>
      Ver más
    </button>
  <!-- Enters para espaciado-->
  </div>
  <br>
  <br>
  <br>
  <br>
  <div class="Graficos-flourish">
  <div class="Titulos Escuderias">
    <h3 style="text-align: center;">Todos los titulos de las escuderias</h3>
    <div class="flourish-embed flourish-chart" data-src="visualisation/20393896"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/visualisation/20393896/thumbnail" width="100%" alt="chart visualization" /></noscript></div>
  </div>
</div>
</div>
<!-- Enters para espaciado -->
 
<br>
<br>
<br>

<!-- Codigo Segundo Juego-->
<div class="Segund0 Juego">
  <div class="titulo-con-bajada" style="text-align: center;">
    <h2>Que escuderia te representa?</h2>
    <p>Descubri con que escuderia te llevarias mejor!</p>
  </div>
  <!-- Poner Codigo-->
   <h1 style="font-weight: bold; text-align: center;">PONER CODIGO DEL JUEGO</h1>
</div>

<!-- Circuito Emiratos Arabes-->
<div style="display: flex; width: 100%; justify-content: center; align-items: center; gap: 10px; height: 50vh;">
  <div class="iframe__container" style="width: 40%; display: flex; justify-content: center; align-items: center; margin: 0;">
    <div class="flourish-embed flourish-countdown" data-src="visualisation/20395767" style="width: 100%; max-width: 600px; height: auto; margin: 0; text-align:center; margin-bottom: 15%">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript>
        <img src="https://public.flourish.studio/visualisation/20395767/thumbnail" width="100%" alt="countdown visualization" />
      </noscript>
    </div>
  </div>
  <img 
    style="width: 30%; max-height: 100%; object-fit: contain; margin: 0;"
    src="./public/images/Circuito-Emirato-Arabes.png" 
    alt="Imagen del circuito">
</div>



<!--Si quiero hacer mas scrolling copio de aca -->
<!-- Contenedor de la story de flourish (scrolly)-->

<!-- Circuito USA -->
<div style="display: flex; width: 100%; height: 100vh;">
  <!-- Contenedor del gráfico Flourish -->
  <div style="width: 60%; display: flex; justify-content: center; align-items: center; padding: 10px; height: 100%; margin-top: 11%;">
    <div style="width: 100%; height: 100%; display: flex; align-items: center;">
      <div class="flourish-embed flourish-sports" 
           data-src="visualisation/20281846" 
           style="width: 100%; height: 100%;"> 
        <script src="https://public.flourish.studio/resources/embed.js"></script>
        <noscript>
          <img src="https://public.flourish.studio/visualisation/20281846/thumbnail" width="100%" alt="sports visualization" />
        </noscript>
      </div>
    </div>
  </div>

  <!-- Contenedor de imágenes -->
  <div style="width: 40%; display: flex; flex-direction: column; align-items: center; gap: 5px; height: 100%; justify-content: center;">
    <img 
      src="./public/images/Posiciones Estados Unidos.png" 
      alt="Posiciones Estados Unidos"
      style="width: 50%; object-fit: contain;">
    <img
      src="./public/images/Circuito Estados Unidos.png"
      alt="Circuito Estados Unidos"
      style="width: 80%; object-fit: contain;">
  </div>
</div>

<!-- Circuito Mexico -->
<div style="display: flex; width: 100%; height: 100vh;">
  <!-- Contenedor del gráfico Flourish -->
  <div style="width: 60%; display: flex; justify-content: center; align-items: center; padding: 10px; height: 100%; margin-top: 11%;">
    <div style="width: 100%; height: 100%; display: flex; align-items: center;">
      <div class="flourish-embed flourish-sports" 
           data-src="visualisation/20281711" 
           style="width: 100%; height: 100%;"> 
        <script src="https://public.flourish.studio/resources/embed.js"></script>
        <noscript>
          <img src="https://public.flourish.studio/visualisation/20281711/thumbnail" width="100%" alt="sports visualization" />
        </noscript>
      </div>
    </div>
  </div>

  <!-- Contenedor de imágenes -->
  <div style="width: 40%; display: flex; flex-direction: column; align-items: center; gap: 5px; height: 100%; justify-content: center;">
    <img 
      src="./public/images/Posiciones Mexico.png" 
      alt="Posiciones Estados Unidos"
      style="width: 50%; object-fit: contain;">
    <img
      src="./public/images/Circuito Mexico.png"
      alt="Circuito Estados Unidos"
      style="width: 80%; object-fit: contain;">
  </div>
</div>

<!-- Circuito Brasil -->
<div style="display: flex; width: 100%; height: 100vh;">
  <!-- Contenedor del gráfico Flourish -->
  <div style="width: 60%; display: flex; justify-content: center; align-items: center; padding: 10px; height: 100%; margin-top: 11%;">
    <div style="width: 100%; height: 100%; display: flex; align-items: center;">
      <div class="flourish-embed flourish-sports" 
           data-src="visualisation/20279891" 
           style="width: 100%; height: 100%;"> 
        <script src="https://public.flourish.studio/resources/embed.js"></script>
        <noscript>
          <img src="https://public.flourish.studio/visualisation/20279891/thumbnail" width="100%" alt="sports visualization" />
        </noscript>
      </div>
    </div>
  </div>

  <!-- Contenedor de imágenes -->
  <div style="width: 40%; display: flex; flex-direction: column; align-items: center; gap: 5px; height: 100%; justify-content: center;">
    <img 
      src="./public/images/Posiciones Brasil.png" 
      alt="Posiciones Estados Unidos"
      style="width: 50%; object-fit: contain;">
    <img
      src="./public/images/Circuito Brasil.png"
      alt="Circuito Estados Unidos"
      style="width: 80%; object-fit: contain;">
  </div>
</div>

<!-- Enters para espaciado -->

<br>
<br>
<br>

<!-- Mapa de Flourish-->
<div class="Mapa de todos los Circuitos">
  <h2 style="text-align: center;">Mapa de todos los circuitos de la F1</h2>
  <div class="flourish-embed flourish-map" data-src="visualisation/20166772"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/visualisation/20166772/thumbnail" width="100%" alt="map visualization" /></noscript></div>
</div>

<!-- Enters para espaciado -->

<br>
<br>
<br>

<!-- Fotter -->
<div class="Fotter" style="width: 100%; margin: 0%; padding: 0;">
  <h1 style="font-weight: bold; text-align: center;">PONER FOOTER</h1>  
</div>
</body>

<style>
.Posiciones-Pilotos {
  text-align: center; /* Asegura que el contenido dentro del div esté centrado */
}

.Posiciones-Pilotos img {
  display: inline-block; /* Hace que la imagen se comporte como un bloque en línea */
  max-width: 100%; /* Asegura que la imagen no se desborde */
  height: auto; /* Mantiene la proporción de la imagen */
}

.button-container {
  display: flex;
  justify-content: center; /* Centra horizontalmente */
  align-items: center; /* Centra verticalmente */
  margin-top: 1rem; /* Ajusta el margen según sea necesario */
}

.red-button {
  background-color: red;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
}

.red-button:hover {
  background-color: darkred; /* Cambia el color al pasar el mouse */
}


  html, body {
  height: 100%; /* Hace que el body y html ocupen el 100% de la altura de la ventana */
  margin: 0; /* Elimina márgenes por defecto */
  padding: 0; /* Elimina padding por defecto */
}
body{
  background-color: #EDEDED;
  margin: 0; /* Elimina márgenes por defecto */
  padding: 0; /* Elimina padding por defecto */
}
.container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      width: 100%;
  }

  .game-container {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background-color: white;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      width: 80%;
      max-width: 600px;
  }

  .search-input {
      padding: 10px;
      margin-bottom: 20px;
      width: 100%;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
  }

  .driver-list {
      list-style-type: none;
      padding: 0;
      margin: 0;
      width: 100%;
      max-height: 200px;
      overflow-y: auto;
  }

  .driver-list li {
      padding: 10px;
      background-color: #e8e8e8;
      margin: 5px 0;
      cursor: pointer;
      border-radius: 5px;
  }

  .driver-list li:hover {
      background-color: #ccc;
  }

  .questions-container {
      margin-top: 20px;
  }

  .question {
      margin: 20px 0;
      padding: 20px;
      border-radius: 5px;
      background-color: #e8e8e8;
  }

  .options button {
      margin: 5px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      border: 1px solid #ccc;
      border-radius: 5px;
  }

  .options button.default {
      background-color: #f0f0f0;
  }

  .options button.selected {
      background-color: blue;
  }

  .options button.default:active{
    background-color: blue;
  }

  .options button.correct {
      background-color: green;
      color: white;
  }

  .options button.incorrect {
      background-color: red;
      color: white;
  }

  .options button:disabled {
      background-color: lightgray;
      cursor: not-allowed;
  }

  .options button:focus{
    background-color: #d8d6d6;
    outline: none;
  }

  .score-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin-top: 20px;
  }

  .score-text {
      margin-top: 10px;
      font-size: 24px;
      font-weight: bold;
      color: #007bff;
  }

a {
  font-weight: 500;
  color: #646cff;
  text-decoration: inherit;
}
a:hover {
  color: #535bf2;
}
.iframe__container{
  max-width: 900px;
  margin: auto;
}
#my-wrapper {
  margin: auto;
  max-width: 1280px;
}
.titulo-con-bajada h2 {
  font-size: 2rem; /* Tamaño del título */
  font-weight: bold; /* Resaltar el título */
  margin-bottom: 0.5rem; /* Espaciado entre título y bajada */
}
.titulo-con-bajada p {
  font-size: 1.2rem; /* Tamaño más pequeño que el título */
  color: #555; /* Un color más suave */
  margin: 0; /* Sin márgenes adicionales */
}

.Graficos-flourish {
  margin-left: 50px;
  margin-right: 50px;
}
</style>