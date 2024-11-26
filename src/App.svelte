<script>
  // Función para inicializar el componente de Flourish y tomar el script que nos permite hacer el scrolly gratis!
  import { onMount } from 'svelte';

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
</script>

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
   <img 
    src="./public/images/Posiciones Pilotos.png" 
    alt=""
  > 
</div>

<!-- Enters para espaciado -->

<br>
<br>
<br>
<br>
<br>

 <!-- Sueldos Pilotos y los mas Ganadores --> 
 <div class="Sueldos-Maximos-Ganadores" style="display: flex; gap: 1rem;">
  <div class="Mas Campeones" style="flex: 1;">
    <h3 style="text-align: center;">Los campeones del mundo de la F1</h3>
    <div class="flourish-embed flourish-bubble-chart" data-src="visualisation/20278994">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript><img src="https://public.flourish.studio/visualisation/20278994/thumbnail" width="100%" alt="bubble-chart visualization" /></noscript>
    </div>
  </div>  
  <div class="Sueldos" style="flex: 1;">
    <h3 style="text-align: center;">Cuanto ganan los pilotos?</h3>
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

<!-- Codigo Primer Juego-->
<div class="Primer Juego">
  <div class="titulo-con-bajada" style="text-align: center;">
    <h2>Cual es tu piloto favorito de la F1?</h2>
    <p>Cuanto sabes sobre el?</p>
  </div>
  <!-- Poner Codigo-->
   <h1 style="font-weight: bold;">PONER CODIGO DEL JUEGO</h1>
</div>
 
<!-- Enters para espaciado -->
 
<br>
<br>
<br>

<!-- Posiciones Escuderias y Titulos-->
<div class="Posiciones-Escuderias-Titulos">
  <div class="Posiciones Escuderias">
    <img
      src="./public/images/Posiciones Escuderias.png"
      alt=""
    >

  <!-- Enters para espaciado-->
  <br>
  <br>
  <br>
  <br>

  </div>
  <div class="Titulos Escuderias">
    <div class="flourish-embed flourish-chart" data-src="visualisation/20393896"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/visualisation/20393896/thumbnail" width="100%" alt="chart visualization" /></noscript></div>
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
   <h1 style="font-weight: bold;">PONER CODIGO DEL JUEGO</h1>
</div>

<!-- Circuito Emiratos Arabes-->
<div>
  <img 
    style=""
    src="" 
    alt="">
  <div class="iframe__container">
    <div class="flourish-embed flourish-countdown" data-src="visualisation/20395767"><script src="https://public.flourish.studio/resources/embed.js"></script><noscript><img src="https://public.flourish.studio/visualisation/20395767/thumbnail" width="100%" alt="countdown visualization" /></noscript></div>
  </div>
  <img 
    style="max-width: 800px; display: block; margin: auto;"
    src=./public/images/Circuito-Emirato-Arabes.png 
    alt="">
</div>

<!--Si quiero hacer mas scrolling copio de aca -->
<!-- Contenedor de la story de flourish (scrolly)-->

<!-- Circuito USA -->
<div id="my-wrapper">
  <!-- Reemplazar el ID de jeemplo por el de la story propia -->
  <div class="flourish-embed" data-src="story/2726949" data-url="https://public.flourish.studio/story/2726949/embed" data-height="100vh">
    
    <!-- <script src="https://public.flourish.studio/resources/embed.js"></script> -->
  </div>

  <!-- Iteramos sobre las distintas slides del componente de Flourish -->
  {#each slides3 as slide, index}
    <p>
      {slide}
      <!-- svelte-ignore a11y-missing-content -->
      <a href={"#story/2726949/slide-" + (index + 1)}></a>
    </p>
  {/each}
</div>

<!-- hasta aca -->

<!-- Circuito Mexico -->
<div id="my-wrapper">
  <!-- Reemplazar el ID de jeemplo por el de la story propia -->
  <div class="flourish-embed" data-src="story/2727016" data-url="https://public.flourish.studio/story/2727016/embed" data-height="100vh">
    
    <!-- <script src="https://public.flourish.studio/resources/embed.js"></script> -->
  </div>

  <!-- Iteramos sobre las distintas slides del componente de Flourish -->
  {#each slides3 as slide, index}
    <p>
      {slide}
      <!-- svelte-ignore a11y-missing-content -->
      <a href={"#story/2727016/slide-" + (index + 1)}></a>
    </p>
  {/each}
</div>

<!-- Circuito Brasil -->
<div id="my-wrapper">
  <!-- Reemplazar el ID de jeemplo por el de la story propia -->
  <div class="flourish-embed" data-src="story/2727025" data-url="https://public.flourish.studio/story/2727025/embed" data-height="100vh">
    
    <!-- <script src="https://public.flourish.studio/resources/embed.js"></script> -->
  </div>

  <!-- Iteramos sobre las distintas slides del componente de Flourish -->
  {#each slides3 as slide, index}
    <p>
      {slide}
      <!-- svelte-ignore a11y-missing-content -->
      <a href={"#story/2727025/slide-" + (index + 1)}></a>
    </p>
  {/each}
</div>

<!-- Mapa de Flourish-->
 <h1 style="font-weight: bold;">PONER CODIGO DEL MAPA</h1>

<!-- Enters para espaciado -->

<br>
<br>
<br>

<!-- Fotter -->
<div class="Fotter" style="width: 100%; margin: 0%; padding: 0;">
  <h1 style="font-weight: bold;">PONER CODIGO DEL MAPA</h1>  
</div>


<style>

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
</style>