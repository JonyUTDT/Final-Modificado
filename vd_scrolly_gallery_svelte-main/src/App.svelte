<script>
  import Scroller from "@sveltejs/svelte-scroller"
  import * as d3 from "d3"
  /* Importamos componente para video scroll */
  import ScrollyVideo from "scrolly-video/dist/ScrollyVideo.svelte"

  /* Componentes */
  import Medallero from "./components/Medallero.svelte"
  import DebugScroller from "./components/DebugScroller.svelte"
  import Loremipsum from "./components/Loremipsum.svelte"

  import atletas from "/src/data/atletas.json"

  /* Variables para Transición animada */
  let atletasFiltered = atletas
  let count
  let index
  let offset
  let progress
  let top = 0.1
  let threshold = 0.5
  let bottom = 0.9

  $: {
    // Se ejecuta cuando cambia el valor de index
    if (index === 0) {
      atletasFiltered = atletas
    } else if (index === 1) {
      atletasFiltered = atletas.filter(d => d.genero === "F")
    } else if (index === 2) {
      atletasFiltered = atletas.filter(d => d.genero === "M")
    } else if (index === 3) {
      atletasFiltered = atletas.filter(d => d.continente === "América")
    } else {
      atletasFiltered = atletas
    }
  }
  /* Fin Transición animada */

  /* Variables para Secuencia gráfica */
  let index2
  let offset2
  let charts = ["lines_01.png", "lines_02.png", "lines_03.png"]
  /* Fin para Secuencia gráfica */
</script>

<main>
  <div class="header">
    <img src="/images/olympics-logo.png" width="100" alt="anillos" />
    <h3 class="headline">
      <b>Triunfos Olímpicos</b>
      Medallas, alturas y continentes
    </h3>
    <p class="bajada">Explorando los logros olímpicos a través de datos</p>
    <div class="lorem_ipsum">
      <Loremipsum />
    </div>
  </div>

  <!--------------------------->
  <!-- 1. Transición animada -->
  <!--------------------------->
  <h2 class="subtitulo">1. Transición animada</h2>
  <Scroller
    top={top}
    threshold={threshold}
    bottom={bottom}
    bind:count={count}
    bind:index={index}
    bind:offset={offset}
    bind:progress={progress}
  >
    <div slot="background">
      <Medallero deportistas={atletasFiltered} />
    </div>
    <!-- Epigrafes -->
    <div slot="foreground" class="foreground_container">
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion 0</h3>
          <p>Todos los deportistas</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion 1</h3>
          <p>Deportistas femeninas</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion 2</h3>
          <p>Deportistas masculinos</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion 3</h3>
          <p>Deportistas americanos</p>
        </div>
      </section>
    </div>
  </Scroller>
  <!---------------------------->
  <!-- FIN Transición animada -->
  <!---------------------------->

  {#if progress < 1}
    <DebugScroller
      index={index}
      count={count}
      offset={offset}
      progress={progress}
    />
  {/if}

  <div class="lorem_ipsum">
    <Loremipsum />
  </div>

  <!-------------------------->
  <!-- 2. Secuencia gráfica -->
  <!-------------------------->
  <h2 class="subtitulo">2. Secuencia gráfica</h2>
  <Scroller bind:index={index2} bind:offset={offset2}>
    <div slot="background" class="image_container">
      {#each charts as chart, i}
        <img
          src="/images/{chart}"
          alt="chart"
          class="charts"
          style="opacity: {1 - Math.abs(index2 - i - offset2)};"
        />
      {/each}
    </div>
    <div slot="foreground" class="foreground_container">
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index2 + 1}</h3>
          <p>Gráfico 1</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index2 + 1}</h3>
          <p>Gráfico 1</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index2 + 1}</h3>
          <p>Gráfico 1</p>
        </div>
      </section>
    </div>
  </Scroller>
  <!--------------------------->
  <!-- FIN Secuencia gráfica -->
  <!--------------------------->

  <div class="lorem_ipsum">
    <Loremipsum />
  </div>

  <!--------------------->
  <!-- 3. Video Scroll -->
  <!--------------------->
  <h2 class="subtitulo">3. Video Scroll</h2>
  <ScrollyVideo
    src="https://int.nyt.com/newsgraphics/2024/suni/main/move0727finb-1600.mp4"
  />
  <div class="foreground_container" style="margin-bottom: 300px;">
    <section class="step_foreground">
      <div class="epi_foreground">
        <h3>Seccion 1</h3>
        <p>Todos los deportistas</p>
      </div>
    </section>
    <section class="step_foreground">
      <div class="epi_foreground">
        <h3>Seccion 2</h3>
        <p>Deportistas femeninas</p>
      </div>
    </section>
    <section class="step_foreground">
      <div class="epi_foreground">
        <h3>Seccion 3</h3>
        <p>Deportistas masculinos</p>
      </div>
    </section>
    <section class="step_foreground">
      <div class="epi_foreground">
        <h3>Seccion 4</h3>
        <p>Deportistas americanos</p>
      </div>
    </section>
  </div>
  <!---------------------->
  <!-- FIN Video Scroll -->
  <!---------------------->
</main>

<style>
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
    margin-bottom: 80px;
  }
  .headline {
    font-size: 30px;
    line-height: 1.2;
    font-weight: normal;
    text-align: center;
    margin: 20px;
  }
  .bajada {
    font-size: 18px;
    font-weight: normal;
    text-align: center;
    margin: 10px;
  }
  .headline b {
    display: block;
  }
  .subtitulo {
    text-align: center;
    margin: 50px 0;
  }

  /* Estilos para el scroller */
  .foreground_container {
    position: relative;
    /* pointer-events: none; */
    /* padding-left: 50%; */
  }

  .step_foreground {
    display: flex;
    justify-content: center;
    align-items: end;
    max-width: 1280px;
    height: 100vh;
    border: 1px solid rgba(0, 0, 0, 0.4);
    color: white;
    padding: 1em;
    /* margin: 0 0 2em 0; */
    margin: auto;
    margin-bottom: 2em;
  }
  .epi_foreground {
    text-align: center;
    padding: 20px;
    min-width: 250px;
    background-color: rgba(0, 0, 0, 0.5);
  }
  .lorem_ipsum {
    margin: 100px auto;
    max-width: 740px;
  }
  .image_container {
    position: relative;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .charts {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: all 1s;
  }
</style>
