<template>
  <div id="app" :style="appStyle">
    <img src="./assets/logo.png">
    <br>
    <button @click="extendWidth">extend</button>
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

  methods: {
    extendWidth () {
      this.appStyle.width = parseInt(this.appStyle.width) + 10 + '%'
    }
  },

  // Reactive data has not been initialized yet. This section is just before it.
  beforeCreate () {
    console.log('beforeCreate')
    console.log(this.name) // Output 'undefined'
  },

  // Reactive data was initialized.
  created () {
    console.log('create')
    console.log(this.name) // Output 'hatsukaze hitomi'
  },

  // DOM has not been structured yet. This section is just before it.
  beforeMount () {
    console.log('beforeMount')
    console.log(document.getElementById('app').clientWidth) // Output '785' (It depends on the environment)
  },

  // DOM was structured.
  mounted () {
    console.log('mounted')
    console.log(document.getElementById('app').clientWidth) // Output '942' (It depends on the environment)
  },

  beforeUpdate () {
    console.log('beforeUpdate')
    // Output '942' (It depends on the environment) if button was clicked once.
    // Output '1021' (It depends on the environment) if button was clicked twice.
    console.log(document.getElementById('app').clientWidth)
  },

  updated () {
    console.log('updated')
    // Output '1021' (It depends on the environment) if button was clicked once.
    // Output '1099' (It depends on the environment) if button was clicked twice.
    console.log(document.getElementById('app').clientWidth)
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
