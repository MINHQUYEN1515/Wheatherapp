<template>
  <div class="app">
      <wheatherapp/>  
  </div>
  
</template>
<script>
import Wheatherapp from './components/wheatherapp.vue'
export default {
    components:{
    Wheatherapp
    }
}
</script>
<style>
  .app{
    transform: translate(100px,50px);
  }
</style>