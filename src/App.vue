<template>
  <div id="app" :style="appStyle">
    <img src="./assets/logo.png">
    <br>
    <button @click="extendWidth">extend</button>
    <button @click="destroyInstance">destroy</button>
    <app-child :name="name"/>
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

  watch: {
    'appStyle.width' () {
      console.log(this.$el.clientWidth)
    }
  },

  methods: {
    extendWidth () {
      this.appStyle.width = parseInt(this.appStyle.width) + 10 + '%'
      this.$nextTick(() => {
        console.log(this.$el.clientWidth)
      })
    },

    destroyInstance () {
      this.$destroy()
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

    // Output error because dom has not been structed
    // console.log(this.$el.clientWidth)
  },

  // DOM was structured.
  mounted () {
    console.log('mounted')
    console.log(this.$el.clientWidth) // Output '942' (It depends on the environment)
  },

  // Reactive data was updated and DOM has not been updated yet.
  // If $destroy() was called, this hook(and updated hook) will not be executed
  beforeUpdate () {
    console.log('beforeUpdate')

    // Output '942' (It depends on the environment) if button was clicked once.
    // Output '1021' (It depends on the environment) if button was clicked twice.
    console.log(this.$el.clientWidth)
  },

  // Reactive data was updated and DOM was updated.
  updated () {
    console.log('updated')

    // Output '1021' (It depends on the environment) if button was clicked once.
    // Output '1099' (It depends on the environment) if button was clicked twice.
    console.log(this.$el.clientWidth)
  },

  // $destroy() was called and vue instance has been dropped yet.
  beforeDestroy () {
    console.log('beforeDestroy')
    console.log(this.name) // Output 'hatsukaze hitomi'
  },

  // $destroy() was called and vue instance has been dropped yet.
  destroyed () {
    console.log('destroyed')
    console.log(this.name) // Output 'hatsukaze hitomi' (Data is left.)
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
