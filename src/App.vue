<script setup>
import { ref, computed } from 'vue'
  
  const name = 'tu número';

  let arrayFavoritos = ref([]);
 
  const counter = ref(0);
  
  const increment = () => {
    counter.value ++;
  };

  const decrement = () => {
    counter.value --;
  };

  const reset = () => {
    counter.value = 0;
  }

  const add = () => {
    arrayFavoritos.value.push(counter.value);
  }

  const borrar = () => {
    arrayFavoritos.value.pop()
  }

  const bloquearBtn = computed(() => {
    const searchNum = arrayFavoritos.value.find( num => num === counter.value)
    //return searchNum || searchNum === 0;
    if(searchNum === 0) return true;
    return searchNum ? true : false;
  })


  const classComputed = computed (() => {
    if(counter.value < 0) {
      return 'negative'
    } else if ( counter.value > 0) {
      return 'positive'
    } else if ( counter.value === 0) {
      return 'zero'
    }
  })

</script> 


<template>
  <div class="container text-center mt-5">
    <h1>ELIGE {{ name.toUpperCase() }}</h1>
    <h2 :class="classComputed" class="font-siez">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-warning">Disminuir</button>
      <button @click="reset" class="btn btn-danger">Resetear</button>
      <button @click="add" :disabled="bloquearBtn" class="btn btn-primary">Add</button>
      <button @click="borrar" class="btn btn-danger">Delete</button>
    </div>

    <ul class="list-group">
      <li class="list-group-item mt-3" v-for="(lista, index) in arrayFavoritos" :key="index">
        {{ lista }}
      </li>
    </ul>
  </div>
  
</template>


<style>
h1 {
  color: black;
  font-weight: bolder;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru;
}

</style>
