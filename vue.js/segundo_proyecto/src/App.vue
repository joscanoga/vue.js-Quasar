<script setup>
import { computed, ref } from 'vue'
import {productos} from './datos.js'
const contador = ref(0)
const imagen =computed(()=>"https://www.html6.es/img/rey_"+productos[contador.value].nombre+".png")
function capitalizarPrimeraLetra(str) {
  return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}
</script>

<template>
  <header>
    
  </header>

  <main>
    <div class="target">
      <header>
        <h1>Cena {{ (contador)+1 }} con el rey <span>{{ capitalizarPrimeraLetra(productos[contador].nombre) }}</span></h1>
      </header>
      <section class="precio">
        <p class="valor">Precio: <span>{{ productos[contador].precio }} $</span></p>
        
        <p  v-if="productos[contador].finDeSemana"><span class="rojo">(Solo fin de semana)</span></p>
        <p v-else><span class="verde">(Todos los días)</span></p>
        <div class="oferta" v-show="productos[contador].precio >100"><p >Ahora un 10% de dsct: <span>{{ (productos[contador].precio*0.9).toFixed(2) }} $ </span></p><img class="ofertaimg" src="oferta.jpg" alt=""></div>
      </section>
      <section class="imagen">
        <img :src="imagen" alt="">
        
      </section>
      <br/>
      <section class="botones">
        <button @click="contador=(contador+1)%7">Siguiente</button>
      </section>
    </div>
  </main>
</template>

<style scoped>
  .target {
    width: 55vh;
    height: 75vh;
    margin: 0 auto;
    min-height: 500px;
    min-width: 350px;
    border-radius: 5%;
    text-align: center;
    border-block-color: black;
    border-style: solid;
    
  }
  .target header {
    height: 10%;
    justify-content: center;
    align-items: center;
    display: flex;
  }
  .target header span{
    color: green;
  }
  .target .precio {
    height: 15%;
    justify-content: center;
    align-items: center;
    
  }
  .target .precio span{
    color: green;
  }
  .target .precio .verde{
    background-color: green;
    color: blanchedalmond;
    border-radius: 5px;
    justify-content: center;
    align-items: center;
    padding: 2px;
  }
  .target .precio .rojo{
    background-color: red;
    color: blanchedalmond;
    border-radius: 5px;
    justify-content: center;
    align-items: center;
    
    
  }
  .target .imagen {
    height: 65%;
    justify-content: center;
    align-items: center;
    display: flex;
  }
  .ofertaimg{
    width: 35px;
    height: 35px;
  }
  .target .precio .oferta {
    justify-content: center;
    align-items: center;
    display: flex;
  }
</style>
