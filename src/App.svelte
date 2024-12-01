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


let showFlourish = false;

function toggleImage() {
  showFlourish = !showFlourish;
}

let showFlourish2 = false;

function toggleImage2() {
  showFlourish2 = !showFlourish2;
}
</script>

<!-- Tipografia Anta -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anta&display=swap" rel="stylesheet">

<!-- Tipografia Roboto Condensed-->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anta&family=Roboto+Condensed:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
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
<div class="cuerpo" style="margin: 0 auto; max-width: 1200px; padding: 0 16px;">
  <!-- Posiciones Pilotos -->
  <div class="Posiciones-Pilotos">
    <h1 style="text-align: center; font-family:anta; margin-bottom: 0%">Posiciones pilotos</h1>
    {#if showFlourish}
    <!-- Mostrar el gráfico de Flourish cuando showFlourish es true -->
    <iframe src='https://flo.uri.sh/visualisation/20521052/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:1300px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20521052/?utm_source=embed&utm_campaign=visualisation/20521052' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    <button class="red-button" style="font-family: anta;" on:click={toggleImage}>Ver menos</button>
  {:else}
    <!-- Mostrar la imagen original cuando showFlourish es false -->
    <img src="./public/images/Posiciones Pilotos.png" alt="Posiciones-Pilotos" />
    <button class="red-button" style="font-family: anta;" on:click={toggleImage}>Ver más</button>
  {/if}
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
            <h2 style="font-family: anta; text-align: center">¿Cuánto sabes de tu piloto favorito?</h2>
            <input style="font-family: Roboto Condensed;"
                type="text" 
                bind:value={searchQuery} 
                placeholder="Buscar piloto..." 
                class="search-input" 
            />
            <ul class="driver-list" style="font-family: Roboto Condensed;">
                {#each drivers.filter(driver => driver.name.toLowerCase().includes(searchQuery.toLowerCase())) as driver}
                    <li on:click={() => generateQuestions(driver)}>{driver.name}</li>
                {/each}
            </ul>
            {#if questions.length > 0}
                <div class="questions-container">
                    <h3 style="font-family: anta;">¿Cuánto sabes de {currentDriver.name}?</h3>
                    {#each questions as question, index}
                        <div class="question" style="font-family: anta;">
                            <p>{index + 1}. {question.question}</p>
                            <div class="options" style="font-family: Roboto Condensed;">
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
                                        style="background-color: {question.selected !== null ? 'red;' : '#f0f0f0;'}; font-family: Roboto Condensed"

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
                            <p class="score-text" style="font-family: anta;">{score}%</p>
                        </div>
                    {/if}
                </div>
            {/if}
        </div>
    {:else}
        <p style="font-family: anta;">Cargando datos...</p>
    {/if}
  </div>
  
  <!-- Enters para espaciado -->
  
  <br>
  <br>
  <br>

  <!-- Posiciones Escuderias y Titulos-->
  <div class="Posiciones-Escuderias-Titulos">
    <h1 style="text-align: center; font-family: anta; margin-bottom: 0%">Posiciones escuderías</h1>
    <div class="Posiciones-Pilotos">
    {#if showFlourish2}
    <!-- Mostrar el gráfico de Flourish cuando showFlourish es true -->
    <iframe src='https://flo.uri.sh/visualisation/20548807/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:720px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20548807/?utm_source=embed&utm_campaign=visualisation/20548807' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:7px!important;border:none!important;margin:0!important;'> </a></div>
    <button class="red-button" style="font-family: anta;" on:click={toggleImage2}>Ver menos</button>
  {:else}
    <!-- Mostrar la imagen original cuando showFlourish es false -->
    <img src="./public/images/Posiciones Escuderias.png" alt="Posiciones-Pilotos" />
    <br>
    <button class="red-button" style="font-family: anta;" on:click={toggleImage2}>Ver más</button>
  {/if}
    <!-- Enters para espaciado-->
    </div>
    </div>
    <br>
    <br>
    <br>
    <br>
    <div class="Graficos-flourish">
    <div class="Titulos Escuderias">
      <h1 style="text-align: center; font-family: anta">Todos los títulos de las escuderías</h1>
      <div class="flourish-embed flourish-chart" data-src="visualisation/20393896"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/visualisation/20393896/thumbnail" width="100%" alt="chart visualization" /></noscript></div>
    </div>
  </div>
  
  <!-- Enters para espaciado -->
  
  <br>
  <br>
  <br>

  <!-- Circuito Emiratos Arabes-->
  <h1 style="text-align: center; font-family: anta">Todo listo en Abu Dabi: el reloj corre para la gran carrera</h1>
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

  <!-- Mapa de Flourish-->
  <div class="Mapa de todos los Circuitos">
    <h1 style="text-align: center; font-family: anta">Mapa de todos los circuitos de la F1</h1>
    <div class="flourish-embed flourish-map" data-src="visualisation/20166772"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/visualisation/20166772/thumbnail" width="100%" alt="map visualization" /></noscript></div>
  </div>

  <!-- Enters para espaciado -->

  <br>
  <br>
  <br>
</div>
  <!-- Fotter -->
  <div class="Foot" style="background-color: #CC0000; text-align: center; width: 100%; margin-bottom: -3%;margin-top:-5%; font-family: anta">
  <footer class="footer">
    <p style= "font-size: 16px; margin-bottom: 5px; color: #FFFFFF ">Creado por Federico Villanueva y Jonathan Jeifetz</p>
    <p style= "font-size: 16px; margin-bottom: 5px; color: #FFFFFF">
      <a href="https://www.linkedin.com/in/federico-mateo-villanueva-a52196279" target="_blank" style="color: #FFFFFF">LinkedIn</a> |
      <a href="https://github.com/JonyUTDT/Final-Modificado.git" target="_blank" style="color: #FFFFFF">GitHub</a>
    </p>
    <p style="font-size: 16px; margin-bottom: 5px; color: #FFFFFF">
      <a href="https://mail.google.com/mail/?view=cm&fs=1&to=fvillanueva@mail.utdt.edu" target="_blank" style="color: #FFFFFF">fvillanueva@mail.utdt.edu</a> |
      <a href="https://mail.google.com/mail/?view=cm&fs=1&to=jjeifetz@mail.utdt.edu" target="_blank" style="color: #FFFFFF">jjeifetz@mail.utdt.edu</a> 
    </p>
    <div class="DiTella">
      <p style= "font-size: 16px; margin-bottom: 20px; color: #FFFFFF">Visualización de Datos, Universidad Torcuato Di Tella</p>
    </div>
  </footer>
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
  font-size: 20px;
  margin-top: 10px;
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