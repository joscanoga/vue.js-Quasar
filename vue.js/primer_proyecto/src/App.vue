<script setup>
  import { computed, ref } from 'vue';
  import { datos } from './datos';
  const web=datos[0].web;
  const colorA="color:green;font-size:3em;font-weight:bold"
  const colorB="color:gray;font-size:3em;font-weight:bold"
  const micolor=ref(colorA)
  const contador1=ref(0)
  const contador2=ref(0)
  const cambiarColor=()=>{
    if (micolor.value==colorA){
      micolor.value=colorB
    }else{
      micolor.value=colorA
    }
    contador1.value+=1;
    contador2.value+=5;
  }
  const multiplo7= computed(()=>{
    return(contador1.value%7==0&&contador1.value>0)
  })
  const imagen1="images/pngegg.png"
  //<!--datos externos-->
  
</script>

<template>
  <header>
    <!--condicional-->
    <h1 v-if="contador1%5==0">Multiplos de 5</h1>
    <h1 v-else-if="contador1%2!=0">impar</h1>
    <h1 v-else>PAR</h1>
    <!--v-show-->
    <!--recomendado cuando estamos mostrando y ocultando items-->
    <h1 v-show="multiplo7">multiplo de 7</h1>
    <!--hacen lo mismo-->
    <h1 v-bind:style="micolor">hola {{ contador1 }}</h1>
    <button v-on:click="cambiarColor">Aceptar</button>
    <h1 :style="micolor">hola {{ contador2 }}</h1>
    <button @click="cambiarColor">Aceptar</button>
    <!--imagenes-->
    <img v-show="multiplo7" :src="imagen1" alt="">
    <!--datos externos-->
    <br/>
    <a :href="web">hola</a>
    

    
  </header>

  <main>
    
  </main>
</template>

<style scoped>

</style>
