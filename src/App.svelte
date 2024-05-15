<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"

  /* Array donde guardaremos la data */
  let respuestas = []
  
  /* Escala para genero (nota musical) */
  let Genero = d3
    .scaleOrdinal() /* dato categóricos */
    .domain(["Femenino", "Masculino", "No Binario"])
    .range(["../images/CORCHEA.svg", "../images/semicorchea.svg", "../images/negra.svg"])

  /* Escala para tiempo de escucha (tamaño de la nota musical)*/
  let TiempoEnHoras = d3
    .scaleOrdinal()
    .domain(["0-4","5-9","10 o más"])
    .range(["80","100","120"])

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

      respuestas = data
    })
  })
</script>

<main>
  <div class="header">
    <img src="/images/logo.png" width="90" alt="logo" class="logo" />
    <h1 class="headline"> <b>Preferencias Musicales</b> </h1>
    <h4>  Representación visual y significativa de los gustos musicales del curso de VD (alumnos y profesores) </h4>
  </div>

  <!-- Conedor de las entidades -->
  <div class="container">
    {#each respuestas as rta}
      <div class="person-container">
        <div class="aspectoNota">
          {#if rta.Genero == "Masculino"}
          <svg width="{TiempoEnHoras(rta.TiempoEnHoras)}" viewBox="0 0 111 153" fill="{MomentoDeEscucha(rta.Momento)}" xmlns="http://www.w3.org/2000/svg" class="svg-hombre">
            <path d="M40.4101 94.26C38.2601 93.75 18.3101 89.33 7.41006 101.26C6.56006 102.19 0.380059 108.95 2.41006 114.26C5.10006 121.3 21.4801 123.86 31.4101 117.26C32.5901 116.48 37.6101 113.14 39.4101 107.26C40.2701 104.46 40.3201 101.06 40.4101 94.26C40.4401 92.01 40.4101 90.34 40.4101 90.26C40.3001 84.14 40.0501 51.37 39.7201 2.57999" fill="{MomentoDeEscucha(rta.Momento)}"/>
            <path d="M108.88 31.95C108.77 90.71 108.79 114.91 108.88 119.95C108.88 120.03 108.91 121.7 108.88 123.95C108.79 130.75 108.74 134.15 107.88 136.95C106.08 142.83 101.06 146.17 99.8801 146.95C89.9501 153.55 73.5701 150.99 70.8801 143.95C68.8501 138.64 75.0301 131.88 75.8801 130.95C86.7801 119.02 106.73 123.44 108.88 123.95" fill="{MomentoDeEscucha(rta.Momento)}"/>
            <path d="M39.8845 26.5C62.8845 35.89 85.8415 45.11 108.842 54.5V31C85.8415 21.39 62.7297 13.61 39.7297 4L39.8845 26.5Z" fill="white"/>
            <path d="M40.4101 94.26C38.2601 93.75 18.3101 89.33 7.41006 101.26C6.56006 102.19 0.380059 108.95 2.41006 114.26C5.10006 121.3 21.4801 123.86 31.4101 117.26C32.5901 116.48 37.6101 113.14 39.4101 107.26C40.2701 104.46 40.3201 101.06 40.4101 94.26ZM40.4101 94.26C40.4401 92.01 40.4101 90.34 40.4101 90.26C40.3001 84.14 40.0501 51.37 39.7201 2.57999M108.88 31.95C108.77 90.71 108.79 114.91 108.88 119.95C108.88 120.03 108.91 121.7 108.88 123.95M108.88 123.95C108.79 130.75 108.74 134.15 107.88 136.95C106.08 142.83 101.06 146.17 99.8801 146.95C89.9501 153.55 73.5701 150.99 70.8801 143.95C68.8501 138.64 75.0301 131.88 75.8801 130.95C86.7801 119.02 106.73 123.44 108.88 123.95ZM39.8845 26.5C62.8845 35.89 85.8415 45.11 108.842 54.5V31C85.8415 21.39 62.7297 13.61 39.7297 4L39.8845 26.5Z"
            stroke="{MomentoDeEscucha(rta.Momento)}" stroke-width="5" stroke-miterlimit="10"/>
          </svg>
         
          {:else if rta.Genero == "Femenino"}
          <!-- <h1> {TiempoEnHoras(rta.TiempoEnHoras)}</h1>
          <h1> {rta.TiempoEnHoras}</h1> -->
          <svg width="{TiempoEnHoras(rta.TiempoEnHoras)}"  viewBox="0 0 85 122" fill="{MomentoDeEscucha(rta.Momento)}" xmlns="http://www.w3.org/2000/svg" class="svg-mujer">
            <path d="M42.96 2.70001C43.58 5.38001 44.38 7.41001 44.96 8.70001C45.86 10.72 48.12 15.2 61.38 28.28C62.31 29.2 62.34 29.22 62.73 29.61C67.28 34.17 79.19 47.15 81.38 62.28C83.81 79.16 73.39 93.6 72.38 93.28C71.39 92.97 79.31 78.55 74.38 62.28C70.71 50.16 61.82 43.35 60.38 42.28C54.17 37.65 47.95 35.96 44.38 35.28C43.91 24.42 43.43 13.56 42.96 2.70001Z" fill="{MomentoDeEscucha(rta.Momento)}"/>
            <path d="M41.4101 0C41.3001 58.76 41.3201 82.96 41.4101 88C41.4101 88.08 41.4401 89.75 41.4101 92C41.3201 98.8 41.2701 102.2 40.4101 105C38.6101 110.88 33.5901 114.22 32.4101 115C22.4801 121.6 6.10006 119.04 3.41006 112C1.38006 106.69 7.56006 99.93 8.41006 99C19.3101 87.07 39.2601 91.49 41.4101 92" fill="{MomentoDeEscucha(rta.Momento)}"/>
            <path d="M41.4101 0C41.3001 58.76 41.3201 82.96 41.4101 88C41.4101 88.08 41.4401 89.75 41.4101 92M41.4101 92C41.3201 98.8 41.2701 102.2 40.4101 105C38.6101 110.88 33.5901 114.22 32.4101 115C22.4801 121.6 6.10006 119.04 3.41006 112C1.38006 106.69 7.56006 99.93 8.41006 99C19.3101 87.07 39.2601 91.49 41.4101 92ZM42.96 2.70001C43.58 5.38001 44.38 7.41001 44.96 8.70001C45.86 10.72 48.12 15.2 61.38 28.28C62.31 29.2 62.34 29.22 62.73 29.61C67.28 34.17 79.19 47.15 81.38 62.28C83.81 79.16 73.39 93.6 72.38 93.28C71.39 92.97 79.31 78.55 74.38 62.28C70.71 50.16 61.82 43.35 60.38 42.28C54.17 37.65 47.95 35.96 44.38 35.28C43.91 24.42 43.43 13.56 42.96 2.70001Z"
            stroke="{MomentoDeEscucha(rta.Momento)}" stroke-width="4" stroke-miterlimit="10"/>
            </svg>
            
          {:else if rta.Genero == "No Binario"}
          <svg width="60" viewBox="0 0 45 122" fill="{MomentoDeEscucha(rta.Momento)}" xmlns="http://www.w3.org/2000/svg" class="svg-no-binario">
            <path d="M41.4101 0C41.3001 58.76 41.3201 82.96 41.4101 88C41.4101 88.08 41.4401 89.75 41.4101 92C41.3201 98.8 41.2701 102.2 40.4101 105C38.6101 110.88 33.5901 114.22 32.4101 115C22.4801 121.6 6.10006 119.04 3.41006 112C1.38006 106.69 7.56006 99.93 8.41006 99C19.3101 87.07 39.2601 91.49 41.4101 92" fill="{MomentoDeEscucha(rta.Momento)}"/>
            <path d="M41.4101 0C41.3001 58.76 41.3201 82.96 41.4101 88C41.4101 88.08 41.4401 89.75 41.4101 92M41.4101 92C41.3201 98.8 41.2701 102.2 40.4101 105C38.6101 110.88 33.5901 114.22 32.4101 115C22.4801 121.6 6.10006 119.04 3.41006 112C1.38006 106.69 7.56006 99.93 8.41006 99C19.3101 87.07 39.2601 91.49 41.4101 92Z" 
            stroke="{MomentoDeEscucha(rta.Momento)}" stroke-width="6" stroke-miterlimit="10"/>
            </svg>
          {/if} <!--cierro -->
        </div>

        <div class="plataforma">
          {#if rta.Plataforma == "Tidal"}
            <svg width="300" height="300" xmlns="http://www.w3.org/2000/svg" class="difuminado2">
              <rect width="200" height="200" x="55" y="50" fill={GeneroMusical(rta.GeneroMusical)} />
            </svg>

          {:else if rta.Plataforma == "Spotify"}
            <svg height="300" width="300" xmlns="http://www.w3.org/2000/svg" class="difuminado">
              <circle r="110" cx="150" cy="150" fill={GeneroMusical(rta.GeneroMusical)}/>
                <!-- Falta definir la forma de Tidal -->
            </svg>
          {/if} <!--cierro -->
        </div>
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

<footer class="footer">
  <div class="footer-container">
    <p class="atribucion">Representación visual creada por <a href="https://www.linkedin.com/in/serena-marelli/">Serena Marelli</a> y <a href="https://www.linkedin.com/in/josefina-jahde/">Josefina Jahde</a></p>
    <div class="redes-sociales">
      <a href="https://www.linkedin.com/in/serena-marelli/"><img src="../images/logo-linkedin.png" alt="LinkedIn Serena Marelli"></a>
      <a href="https://www.linkedin.com/in/josefina-jahde/"><img src="/images/logo-linkedin.png" alt="LinkedIn Josefina Jahde"></a>
    </div>

    <a href="https://github.com/seremare9/entrega2_vd.git" class="github-link">Ver código en GitHub</a>
  </div>
</footer>

<style>
  .logo {
    position: absolute;
    top: 1%;
    left: 1%;
  }
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
    margin-bottom: 80px;
  }
  .headline {
    position: absolute;
    top: 20px; 
    left: 50%; 
    transform: translateX(-50%); /* Esto lo centra completamente */
    font-size: 35px;
    line-height: 1.5;
    font-weight: normal;
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

  .name {
    font-size: 18px;
    color: rgb(65, 65, 65);
    font-weight: bold;
    text-align: center;
    margin-top: 5px;
  }
  .name:hover{
    color: crimson;
    transition: transform 0.2s ease-in-out; /* Agregar una transición suave */
  }
  .cancionFav {
    font-size: 13px;
    color: rgb(65, 65, 65);
    font-weight: light;
    transform: translate(3%, -100%);
  }
  
  .difuminado{ /*ciruclos*/
    position: relative; /* permite posicionar sus elementos secundarios de forma absoluta */
    background: radial-gradient(circle, transparent 0%, rgba(255,255,255,0.5) 100%); /* Crea un gradiente radial */
    filter: blur(9px);
    z-index: 1;
  }

  .difuminado2 { /*cuadrado*/
  position: relative; /* permite posicionar sus elementos secundarios de forma absoluta */
  filter: blur(9px); /* Aplica un efecto de desenfoque */
  z-index: 1; /* Asegura que esté sobre otros elementos */
}

.aspectoNota {
  z-index: 2;
  position: absolute; /*posiciona las notas musicales arriba de los ciruclos/cuadrado*/
  transform: translate(3%, -30%) /* Traslada las notas hacia la derecha y hacia arriba*/
}

.svg-hombre:hover,
.svg-mujer:hover,
.svg-no-binario:hover {
  transform: scale(1.2); /* Aumentar tamaño un 20% al pasar el mouse */
  transition: transform 0.2s ease-in-out; /* Agregar una transición suave */
}

</style>
