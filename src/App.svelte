<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"

  /* Array donde guardaremos la data */
  let respuestas = []
  
  /* Escala para genero (nota musical) */
  let Genero = d3
    .scaleOrdinal() /* dato categóricos */
    .domain(["Femenino", "Masculino", "No Binario"])
    .range(["./images/corchea_final.png", "./images/semicorchea_final.png", "./images/negra_final.png"])

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
        <img src="{Genero(rta.Genero)}" alt="genero">
        <!-- <img src="{Plataforma(rta.Plataforma)}" alt="sombra"> -->
        style="width: {TiempoEnHoras(rta.TiempoDeEscucha)}px;" 
        <svg height="200" width="200" xmlns="http://www.w3.org/2000/svg">
          <circle r="45" cx="50" cy="50" fill={GeneroMusical(rta.GeneroMusical)}/>
           <!-- Falta definir la forma de Tidal -->
        </svg>

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
  .name {
    font-size: 15px;
    color: rgb(65, 65, 65);
    font-weight: bold;
    text-align: center;
    margin-top: 5px;
  }
  .cancionFav {
    font-size: 12px;
    color: rgb(65, 65, 65);
    font-weight: normal;
    font-style: italic;
    text-align: center;
    margin-top: 5px;
  }
    
</style>
