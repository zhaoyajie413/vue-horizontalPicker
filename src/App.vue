<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld :list="list" v-model="value" />
  </div>
</template>

<script>
import HelloWorld from './components/HorizontalPicker.vue'
const list=[];
      for(let i=0;i<30;i++){
        list[i] =  {text:i,value:i}
      }

export default {
  name: 'App',
  data(){
    return {
      list:list,
      value:6
    }
  },
  components: {
    HelloWorld
  }
}
</script>

<style>
  body{
    padding: 0;
    margin: 0;
  }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #f5f5f5;
  width: 100vw;
  height: 100vh;
}
</style>
