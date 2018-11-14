<template>
  <div id="app" :style="appStyle">
    <img src="./assets/logo.png">
    <app-child/>
  </div>
</template>

<script>
import AppChild from './components/app-child'

export default {
  name: 'App',
  components: {
    AppChild
  },

  data () {
    return {
      name: 'hatsukaze hitomi',
      appStyle: {
        width: '120%',
        height: '120%'
      }
    }
  },

  // Reactive data has not been initialized yet. This section is just before it.
  beforeCreate () {
    console.log(this.name) // Output 'undefined'
  },

  // Reactive data was initialized.
  created () {
    console.log(this.name) // Output 'hatsukaze hitomi'
  },

  // DOM has not been structured yet. This section is just before it.
  beforeMount () {
    console.log(document.getElementById('app').clientWidth) // Output '785' (It depends on the environment)
  },

  // DOM was structured.
  mounted () {
    console.log(document.getElementById('app').clientWidth) // Output '942' (It depends on the environment)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
