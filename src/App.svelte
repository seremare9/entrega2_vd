<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"

  /* Array donde guardaremos la data */
  let respuestas = []
  
  /* Escala para genero (nota musical) */
  let Genero = d3
    .scaleOrdinal() /* dato categóricos */
    .domain(["Femenino", "Masculino", "No Binario"])
    .range(["../images/corchea.svg", "../images/semicorchea.svg", "../images/negra.svg"])

  /* Escala para tiempo de escucha (tamaño de la nota musical)*/
  let TiempoEnHoras = d3
    .scaleLinear()
    .domain(["0-4","5-9","10 o más"])
    .range([80,100,120])

  /* Escala para momento de escucha (color de la nota musical)*/
  let MomentoDeEscucha = d3
    .scaleOrdinal()
    .domain(["Mañana", "Tarde", "Noche"])
    .range(["#94B8D7", "#365B77", "#02152B"])

  /* Escala para plataforma favorita (forma de la sombra) */
  let Plataforma = d3.scaleOrdinal()
    .domain(["Spotify", "Tidal"])
    .range(["Ellipse.svg", "Star.svg"])

  /* Escala para género musical favorito (color de la sombra)*/
   let GeneroMusical = d3.scaleOrdinal()
    .domain(["Rock", "Indie", "Pop", "Hip-hop", "Jazz", "Otro"])
    .range(["#FF9999", "#FFC399", "#FFEE99","#FF99FF","#AA99FF","#BBFF99"])
  
  onMount(() => {
    d3.csv("./data/Proyecto2VD.csv", d3.autoType).then(data => {
      console.log(data)

      /* Actualizamos dominio con la data de edad */
      // let minMaxEdad = d3.extent(data, d => d.edad)
      // grosor = grosor.domain(minMaxEdad)

      /* Actualizamos dominio y rango con la data de altura */
      // let minMaxAltura = d3.extent(data, d => d.altura)
      // radioAltura = radioAltura.domain(minMaxAltura).range([25, 50])

      respuestas = data
    })
  })
</script>

<main>
  <div class="header">
    <img src="/images/logo.png" width="100" alt="logo" />
    <h3 class="headline">
      <b>Preferencias Musicales</b>
      Visualización de Datos
    </h3>
    <p class="bajada">Josefina Jahde y Serena Marelli</p>
  </div>

  <!-- Conedor de las entidades -->
  <div class="container">
    <!-- Iteramos la data para visualizar c/ entidad -->
    {#each respuestas as rta}
      <div class="person-container">
        <div class = "aspectoNota">
            {#if rta.Genero == "Masculino"}
              {#if rta.TiempoEnHoras == "0-4"}
                <svg width="80" viewBox="0 0 112.89 151.78" xmlns="http://www.w3.org/2000/svg"> 
                <path d="M42.72,24.58c23,9.39,46,18.78,69,28.17v-23.17C88.72,19.97,65.72,10.36,42.72.75v23.83Z"
                fill = {MomentoDeEscucha(rta.Momento)}/>
                </svg>
              {:else if rta.TiempoEnHoras == "5-9"}
                <svg width="100" viewBox="0 0 112.89 151.78" xmlns="http://www.w3.org/2000/svg"> 
                <path d="M42.72,24.58c23,9.39,46,18.78,69,28.17v-23.17C88.72,19.97,65.72,10.36,42.72.75v23.83Z"
                fill = {MomentoDeEscucha(rta.Momento)}/>
                </svg>
              {:else if rta.TiempoEnHoras == "10 o más"}
                <svg width="120" viewBox="0 0 112.89 151.78" xmlns="http://www.w3.org/2000/svg"> 
                <path d="M42.72,24.58c23,9.39,46,18.78,69,28.17v-23.17C88.72,19.97,65.72,10.36,42.72.75v23.83Z"
                fill = {MomentoDeEscucha(rta.Momento)}/>
                </svg>

            {:else if rta.Genero == "Femenino"}
              {#if rta.TiempoEnHoras == "0-4"}
                <svg width="80" viewBox="0 0 82.25 121.83" xmlns="http://www.w3.org/2000/svg"> 
                <path d="M42.96,2.7c.62,2.68,1.42,4.71,2,6,.9,2.02,3.16,6.5,16.42,19.58.93.92.96.94,1.35,1.33,4.55,4.56,16.46,17.54,18.65,32.67,2.43,16.88-7.99,31.32-9,31-.99-.31,6.93-14.73,2-31-3.67-12.12-12.56-18.93-14-20-6.21-4.63-12.43-6.32-16-7-.47-10.86-.95-21.72-1.42-32.58Z"
                fill = {MomentoDeEscucha(rta.Momento)}/>
                </svg>
              {:else if rta.TiempoEnHoras == "5-9"}
                  <svg width="100" viewBox="0 0 82.25 121.83" xmlns="http://www.w3.org/2000/svg"> 
                  <path d="M42.96,2.7c.62,2.68,1.42,4.71,2,6,.9,2.02,3.16,6.5,16.42,19.58.93.92.96.94,1.35,1.33,4.55,4.56,16.46,17.54,18.65,32.67,2.43,16.88-7.99,31.32-9,31-.99-.31,6.93-14.73,2-31-3.67-12.12-12.56-18.93-14-20-6.21-4.63-12.43-6.32-16-7-.47-10.86-.95-21.72-1.42-32.58Z"
                  fill = {MomentoDeEscucha(rta.Momento)}/>
                  </svg>
              {:else if rta.TiempoEnHoras == "10 o más"}
                  <svg width="120" viewBox="0 0 82.25 121.83" xmlns="http://www.w3.org/2000/svg"> 
                  <path d="M42.96,2.7c.62,2.68,1.42,4.71,2,6,.9,2.02,3.16,6.5,16.42,19.58.93.92.96.94,1.35,1.33,4.55,4.56,16.46,17.54,18.65,32.67,2.43,16.88-7.99,31.32-9,31-.99-.31,6.93-14.73,2-31-3.67-12.12-12.56-18.93-14-20-6.21-4.63-12.43-6.32-16-7-.47-10.86-.95-21.72-1.42-32.58Z"
                  fill = {MomentoDeEscucha(rta.Momento)}/>
                  </svg>
            
          {:else if rta.Genero == "No Binario"}
            <svg width="100" viewBox="0 0 44.42 121.83" xmlns="http://www.w3.org/2000/svg"> 
              <path d="M41.41,0c-.11,58.76-.09,82.96,0,88,0,.08.03,1.75,0,4-.09,6.8-.14,10.2-1,13-1.8,5.88-6.82,9.22-8,10-9.93,6.6-26.31,4.04-29-3-2.03-5.31,4.15-12.07,5-13,10.9-11.93,30.85-7.51,33-7"
              fill = {MomentoDeEscucha(rta.Momento)}/>
            </svg>
          {/if}
        </div>

        <svg height="300" width="300" xmlns="http://www.w3.org/2000/svg" class="difuminado">
          <circle r="110" cx="150" cy="150" fill={GeneroMusical(rta.GeneroMusical)}/>
             <!-- Falta definir la forma de Tidal -->
        </svg>
        <!-- <img src="{Plataforma(rta.Plataforma)}" alt="sombra"> -->
        <!-- style="width: {TiempoEnHoras(rta.TiempoDeEscucha)}px;"  -->
        <p class="name">
          <b>{rta.Nombre}</b>
          <br />
        </p>
        <p class="cancionFav">
          <b>{rta.Cancion}</b>
          <br />
        </p>
      </div>
    {/each}
  </div>
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
  .container {
    display: flex;
    justify-content: center;
    align-items: end;
    margin: auto;
    flex-wrap: wrap;
    max-width: 1000px;
    gap: 30px;
    margin-bottom: 100px;
  }
  .person-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    flex: 180px 0 0;
  }
  /* .person {
    width: 100px;
    height: 100px;
    border: 10px solid black;
    border-radius: 50%;
    box-sizing: border-box;
  } */
  /* .medal {
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background-color: gold;
    margin: 5px 0;
  } */
  .nota {
    /* filter: brightness(0) invert(1);
    mix-blend-mode: color; */
    /* background-color: {MomentoDeEscucha(rta.Momento)}; */
    filter: brightness(0) saturate(100%) hue-rotate(240deg);
    /* width: 50px; */
    z-index: 2;
  }
  .name {
    font-size: 15px;
    color: rgb(65, 65, 65);
    font-weight: bold;
    text-align: center;
    margin-top: 5px;
  }
  .cancionFav {
    font-size: 13px;
    color: rgb(65, 65, 65);
    font-weight: light;
    font-style: italic;
    text-align: center;
    margin-top: 5px;
  }
  
  .difuminado{
    background: radial-gradient(circle, transparent 0%, rgba(255,255,255,0.5) 100%); /* Crea un gradiente radial */
    filter: blur(9px);
    z-index: 1;
  }
    
</style>
