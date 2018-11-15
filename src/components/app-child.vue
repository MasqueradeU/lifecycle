<template>
  <div id="app-child" :style="childStyle">
    <br>
    <button @click="extendWidth">extend-child</button>
    <button @click="destroyInstance">destroy-child</button>
  </div>
</template>

<script>

export default {
  name: 'app-child',
  data () {
    return {
      name: 'hitomi hatsukaze',
      childStyle: {
        width: '150%',
        height: '150%'
      }
    }
  },

  methods: {
    extendWidth () {
      this.childStyle.width = parseInt(this.childStyle.width) + 10 + '%'
    },

    destroyInstance () {
      this.$destroy()
    }
  },

  // Reactive data has not been initialized yet. This section is just before it.
  beforeCreate () {
    console.log('beforeCreate-child')
    console.log(this.name) // Output 'undefined'
  },

  // Reactive data was initialized.
  created () {
    console.log('create-child')
    console.log(this.name) // Output 'hatsukaze hitomi'
  },

  // DOM has not been structured yet. This section is just before it.
  beforeMount () {
    console.log('beforeMount-child')

    // Output error because dom has not been structed
    // console.log(this.$el.clientWidth)
  },

  // DOM was structured.
  mounted () {
    console.log('mounted-child')
    console.log(this.$el.clientWidth) // Output '1413' (It depends on the environment)
  },

  // Reactive data was updated and DOM has not been updated yet.
  // If $destroy() was called, this hook(and updated hook) will not be executed
  beforeUpdate () {
    console.log('beforeUpdate-child')

    // Output '1413' (It depends on the environment) if button was clicked once.
    // Output '1507' (It depends on the environment) if button was clicked twice.
    console.log(this.$el.clientWidth)
  },

  // Reactive data was updated and DOM was updated.
  updated () {
    console.log('updated-child')

    // Output '1507' (It depends on the environment) if button was clicked once.
    // Output '1601' (It depends on the environment) if button was clicked twice.
    console.log(this.$el.clientWidth)
  },

  // $destroy() was called and vue instance has been dropped yet.
  beforeDestroy () {
    console.log('beforeDestroy-child')
    console.log(this.name) // Output 'hatsukaze hitomi'
  },

  // $destroy() was called and vue instance has been dropped yet.
  destroyed () {
    console.log('destroyed-child')
    console.log(this.name) // Output 'hatsukaze hitomi' (Data is left.)
  }

}
</script>
