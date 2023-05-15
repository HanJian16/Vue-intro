<template>
  <h1>Cena {{ position + 1 }} con el rey godo <b>{{ king }}</b></h1>
  <span>Precio: <b>{{ productos[position].precio }}$</b></span>
  <div class="weekEnd css" v-if="productos[position].finDeSemana">(Solo fines de semana)</div>
  <div class="allWeek css" v-else>(De Lunes a Domingo)</div>
  <div class="conteiner" v-if="productos[position].precio < 100">
    <div>Ahora un 10% dto: <b>{{ priceDesc }}$</b></div>
    <img :src="oferta" alt="" />
  </div>
  <img :src="imgKing" alt="" class="king">
  <button @:click="siguiente">Siguiente ({{ position + 1 }}/{{ productos.length }})</button>
</template>

<script setup>
import { ref, computed } from 'vue';
import { productos } from './db.js';
const oferta = "oferta.jpg"
const position = ref(0);
const ruta = "https://www.html6.es/img/rey_"
const siguiente = () => {
  if (position.value >= productos.length - 1) {
    position.value = 0;
  } else {
    position.value = position.value + 1;
  }
}
const king = computed(() => {
  const name = productos[position.value].nombre.toLowerCase();
  return name[0].toUpperCase() + name.slice(1);
});
const priceDesc = computed(() => {
  // return productos[position.value].precio - (productos[position.value].precio / 10);
  return Number(productos[position.value].precio/1.10).toFixed(2);
});
const imgKing = computed(() => {
  return ruta + king.value.toLowerCase() + ".png";
})
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

b {
  color: green;
  display: inline;
}

span {
  font-size: 25px;
}

.css{
  font-size: 20px;
  width: 200px;
  height: 25px;
  color: white;
  text-align: center;
  border-radius: 5px;
}

.weekEnd {
  background: red;
}

.allWeek {
  background: green;
}

button {
  display: flex;
  width: fit-content;
}

img {
  width: auto;
  height: auto;
  max-width: 40px;
  max-height: 40px;
}

.conteiner {
  display: flex;
  margin: 10px;
  align-items: center;
  justify-content: center;
}

.king {
  width: auto;
  height: auto;
  max-width: 300px;
  max-height: 300px;
  margin: 20px 0;
}
</style>