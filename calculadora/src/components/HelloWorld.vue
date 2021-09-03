<template>

  <div class="calculadora">
  <input class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight 
  focus:outline-none focus:bg-white focus:border-purple-500" type="text" value="0">

  
    <div class="calculadora-body"> 
      <button class="btn btn-blue">(</button>
      <button class="btn btn-blue">)</button>
      <button class="btn btn-blue">%</button>
      <button class="btn btn-blue">C</button>
      <button class="btn btn-blue">1</button>
      <button class="btn btn-blue">2</button>
      <button class="btn btn-blue">3</button>
      <button class="btn btn-blue">/</button>
      <button class="btn btn-blue">4</button>
      <button class="btn btn-blue">5</button>
      <button class="btn btn-blue">6</button>
      <button class="btn btn-blue">x</button>
      <button class="btn btn-blue">7</button>
      <button class="btn btn-blue">8</button>
      <button class="btn btn-blue">9</button>
      <button class="btn btn-blue">-</button>
      <button class="btn btn-blue">0</button>
      <button class="btn btn-blue">.</button>
      <button class="btn btn-blue">=</button>
      <button class="btn btn-blue">+</button>
    </div>
  </div>
</template>


<script setup>
import { defineProps, reactive } from 'vue'

defineProps({
  msg: String
})

const state = reactive({ count: 0 })
</script>

