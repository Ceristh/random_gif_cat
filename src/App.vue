<template>
  <div id="app">
    <div class="bg_celeste">
      <div class="container">
        <h1>Random Gif Cat</h1>
      </div>
    </div>
    <div class="bg_rosado">
      <div class="container">
        <div class="grilla">
          <div class="text-align-right">
            <label for="titulo">Titulo:</label>
          </div>
          <div>
            <input type="text" v-model="titulo">
          </div>
          <div class="text-align-right">
            <label for="filtro">Filtro:</label>
          </div>
          <div>
            <select name="filtro" id="filtro" v-model="filtro">
              <option value="blur">Blur</option>
              <option value="mono">Mono</option>
              <option value="sepia">Sepia</option>
              <option value="negative">Negative</option>
              <option value="paint">Paint</option>
              <option value="pixel">Pixel</option>
            </select>
          </div>
          <div class="text-align-right">
            <label for="color">Color:</label>
          </div>
          <div>
            <select name="color" id="color" v-model="color">
              <option value="red">Rojo</option>
              <option value="blue">Azul</option>
              <option value="green">Verde</option>
              <option value="white">Blanco</option>
              <option value="yellow">Amarillo</option>
              <option value="purple">Morado</option>
              <option value="black">Negro</option>
            </select>
            <span class="muestra_color" :style="{backgroundColor:color}"></span>
          </div>
          <div class="text-align-right">
            <label for="size">Tamaño:</label>
          </div>
          <div>
            <input id="size" type="number" v-model="size">
          </div>
        </div>
      </div>
    </div>

    <div class="bg_celeste">
      <div class="container">
          <button @click="consultar">Obtener mi gatito</button>
      </div>
      <div>
        <img :src="imagen_gato">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "App",
  data(){
    return {
      titulo: '',
      filtro: '',
      color: '',
      size: null,
      imagen_gato:'',
    }
  },
  methods:{
    consultar(){
      fetch(`https://cataas.com/cat/says/${(this.titulo || 'Hola')}?size=${this.size}&color=${this.color}&filter=${this.filtro}&width=300`)
      .then(resp => this.imagen_gato = resp.url);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  min-height: 100vh;
  background-color: #a2c8eb;
}
.container {
  width: 100%;
  max-width: 400px;
  padding-left: 15px;
  padding-right: 15px;
  margin-left: auto;
  margin-right: auto;
}
.bg_celeste {
  background-color: #a2c8eb;
  padding: 40px 0 20px;
}
.bg_rosado {
  background-color: #f57d6f;
  padding: 30px 0;
}
h1 {
  margin: 0;
  font-weight: 700;
  font-size: 34px;
}
.grilla {
  display: grid;
  grid-template-columns: 1fr 2fr;
  row-gap: 15px;
}
.grilla > div{
  display: flex;
  align-self: center;
}
.text-align-right {
  justify-content: flex-end;
  margin-right: 15px;
}
input , select {
  padding: .25rem .4rem;
  border-radius: 3px;
  border: 2px solid #dd6c5f;
  width: 160px;
}
button {
  background-color: #f2f4fa;
  color: #202020;
  border: 1px solid #b8b5b5;
  padding: .4rem;
  border-radius: .3rem;
  cursor: pointer;
  margin-bottom: 40px;
}
button:hover {
  background-color: #f57d6f;
}
input:focus, select:focus {
  outline-width: 1px;
  outline-color: #f57d6f;
}
.muestra_color {
  border: 1px solid rgb(236, 232, 232);
  width: 22px;
  height: 22px;
  margin-left: 10px;
  display: inline-block;
  border-radius: 50%;
}
</style>