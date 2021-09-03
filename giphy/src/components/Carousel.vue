<template>
    <div class="carousel">
        <slot></slot>

        <button @click="next" class="next">Next</button>
        <button @click="prev" class="prev">Prev</button>
    </div>
</template>
<script>

export default {
    data (){
        return{

        }
    },
    methods:{
        next(){
            this.$emit('next')
        },
        prev(){
            this.$emit('prev')
        }
    }
}
</script>

<style>
.carousel {
  position: relative;
  overflow: hidden;
  width: 600px;
  height: 350px;
  z-index: 10;
}
button {
  padding: 5px 10px;
  background-color: black;
  border: 1px solid;
  margin: 5px 10px;
  height: 40px;
  width: 50px;
  position: absolute;
  color: white;
  top: calc(50% - 20px);
}
button:hover,button:focus {
  cursor: pointer;
  outline: none;
}
.next {
  right: 0;
}
.prev {
  left: 0;
}
</style>