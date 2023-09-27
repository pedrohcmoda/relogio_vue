<template>
  <div id="app" :class="temaSelecionado">
    <!-- Inicio Header -->
    <header :class="temaSelecionado" class="header-top">

      <!-- Logomarca -->
      <a :class="temaSelecionado" class="marca" href="#">
        <img alt="Byte logo" src="./assets/byte.svg" style="width: 5rem; height: auto;">
        <h2 class="letracao">ByteNest</h2>
      </a>

      <!-- Seleção de Temas -->
      <div class="themes" :class="temaSelecionado">
        <label :class="temaSelecionado" for="Dark">
          <input type="radio" name="temas" id="Dark" value="dark" checked v-model="temaSelecionado">
          Dark
        </label>
        <label :class="temaSelecionado" for="Light">
          <input type="radio" name="temas" id="Light" value="light" v-model="temaSelecionado">
          Light
        </label>
        <label :class="temaSelecionado" for="Neon">
          <input type="radio" name="temas" id="Neon" value="neon" v-model="temaSelecionado">
          Neon
        </label>
        <label :class="temaSelecionado" for="Dabid">
          <input type="radio" name="temas" id="Dabid" value="dabid" v-model="temaSelecionado">
          Dabid
        </label>
      </div>

      <!-- Navegação -->
        <nav :class="temaSelecionado" class="header-top-nav">
          <ul :class="temaSelecionado" class="header-top-nav_ul">
            <li :class="temaSelecionado"><a class="header-top-nav_ul-li_btn" :class="temaSelecionado" href="#">Login</a></li>
            <li :class="temaSelecionado"><a  class="header-top-nav_ul-li_btn" :class="temaSelecionado" href="#">GRp</a></li>
            <li :class="temaSelecionado"><a  class="header-top-nav_ul-li_btn" :class="temaSelecionado" href="#">Relógio</a></li>
            <li :class="temaSelecionado"><a  class="header-top-nav_ul-li_btn" :class="temaSelecionado" href="#">Calculadora</a></li>
          </ul>
        </nav>


    </header>

    <!-- Inicio Main -->
    <main class="main">
      <div class="horario-container">
        <h1 class="horario" :class="temaSelecionado">{{horas}}:</h1>
        <h1 class="horario" :class="temaSelecionado">{{minutos}}:</h1>
        <h1 class="horario" :class="temaSelecionado">{{segundos}}</h1>
      </div>
    </main>
  </div> 
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      horas: this.horasAtual(),
      minutos: this.minutosAtual(),
      segundos: this.segundosAtual(),
      temaSelecionado:'light',
    };
  },
  methods: {
    formataAbaixoDe10(number) {
      return number.toString().padStart(2, '0');
    },
    horasAtual() {
      const horas = new Date();
      return this.formataAbaixoDe10(horas.getHours());
    },
    minutosAtual() {
      const minutos = new Date();
      return this.formataAbaixoDe10(minutos.getMinutes());
    },
    segundosAtual() {
      const segundos = new Date();
      return this.formataAbaixoDe10(segundos.getSeconds());
    },
    atualiza() {
      setInterval(() => {
        this.horas = this.horasAtual();
        this.minutos = this.minutosAtual();
        this.segundos = this.segundosAtual();
      }, 1000);
    },
  },
  watch: {
    temaSelecionado(newTema) {
      localStorage.setItem('temaSelecionado', newTema);
    },
  },
  mounted() {
    this.atualiza();
    this.temaSelecionado = localStorage.getItem('temaSelecionado');
  },
};
</script>



<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;500;700&display=swap');

  html{
    font-family: 'Open Sans', sans-serif;
  }

  body{
    margin: 0;
    padding: 0;
  }

  #app {
    font-family: 'Open Sans', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    width: 100%;
    margin: 0;
    padding: 0;
    min-height: 100vh;
    flex-grow: 1;

  img {
    width: 8em;
    height: 8em;
    display: block;
  }

  .marca {
    display: flex;
    box-sizing: border-box;
    align-items: center;
    width: fit-content;
    margin: 1em 0;
  }

  .letracao {
    font-family: 'Open Sans', sans-serif;
    box-sizing: border-box;
    letter-spacing: 0.1em;
    font-weight: 800;
    padding: 0;
    margin: 0;
    text-decoration: none;
    font-size: 3vw;
    text-transform: uppercase;
  }
  
  .logomarca {
    width: 5em;
    height: 5em;
  }

  
  .themes{
    display: flex;
    gap: 1em;
  }

  .horario-container {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 2em;
  }

  .horario {
    font-size: 15vw;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .header-top{
    padding: .5em 1em .5em .5em;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .header-top-nav{
    display: flex;
    flex-direction: column;
  }

  .header-top-nav_ul{
    padding: 0;
    list-style-type: none;
    display: flex;
    gap: .5em;
  }

  .header-top-nav_ul-li_btn{
    font-size: 1vw;
    border: solid 1px #222;
    padding: .3em .6em;
    border-radius: 15px;
  }
  
  .fodase{
    width: fit-content;
    display: flex;
  }

  /* Tema Dark */
  .dark {
    color: #ffffff;
    text-decoration: none;
    border-color: #ffffff;
  }

  /* Tema Light */
  .light {
    color:#333333;
    text-decoration: none;
    border-color: #333333;
  }

  /* Tema Neon */
  .neon {
    color: #ff66ff;
    text-decoration: none;
    border-color: #66ffff;
  }

  /* Tema Dabid */
  .dabid {
    color: #ffcc00;
    text-decoration: none;
    border-color: #ff1493;
  }

  .dabid h1 {
    color: #ffffff;
  }
  .neon h1{
    color: #ffffff;
  }

  label{
    font-size: 1vw;
    cursor: pointer;
  }

  input[type="radio"] {
    position: absolute;
    left: -99999px;
  }

  #app.light{
    background-color: #f5f5f5;
  }

  #app.dark{
    background-color: #1a1a1a;
  }

  #app.neon{
    background: linear-gradient(to top left, #000, #222);
  }

  #app.dabid{
    background: linear-gradient(to top right, #000, #222);
  }

  .header-top-nav_ul-li_btn:hover {
    border-color: transparent;
  }

  *{
    text-decoration: none;
    transition: all 0.3s ease;
  }

  .header-bottom {
    display: flex;
    gap: 1rem;
  }

  @media screen and (min-width: 1016px) {
    label:hover{
      animation: vibrate .3s linear infinite both;
    }

    .header-top-nav_ul li:hover{
      animation: vibrate .3s linear infinite both;
    }

    label.neon:hover{
      color: #66ffff;
    }

    label.dabid:hover{
      color: #ff1493;
    }
  }

  @media screen and (max-width: 1016px) {
    .horario-container{
      display: flex;
      flex-direction: column;
    }
    .header-top{
      flex-direction: column;
    }

    .letracao{
      font-size: 2em;
    }

    h2{
      display: none;
    }

    .header-top-nav_ul-li_btn{
      font-size: 1em;
    }

    label{
      font-size: 1em;
    }

    .horario{
      font-size: 8rem;
    }
  }

  @media screen and (max-width: 360px) {
    nav{
      display: none;
    }
  }

  @keyframes vibrate {
    0% {
      transform: translate(0);
    }
    20% {
      transform: translate(-2px, 2px);
    }
    40% {
      transform: translate(-2px, -2px);
    }
    60% {
      transform: translate(2px, 2px);
    }
    80% {
      transform: translate(2px, -2px);
    }
    100% {
      transform: translate(0);
    }
  }
} 
</style>
