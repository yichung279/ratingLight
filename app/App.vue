<template lang="pug">
#app
  svg(:width="width", :height="height")
    circle(v-for="(light, i) in lights", :cx="0.25*width+i*0.5*width", :cy="0.25*width", :r="0.2*width", :fill="light.color", @click="lightSwitch(light.color, i)")
</template>

<script>
export default {

  data(){return{
    height: window.innerHeight,
    lights: [
      {color: 'darkgrey'},
      {color: 'darkgrey'}
    ],
    score: 0,
    width: window.innerWidth
  }},

  methods:{

    lightSwitch(color, idx){
      if (color === 'yellow') {
        this.lights[idx].color = 'darkgrey'
        this.score--
      }else if (color === 'darkgrey') {
        this.lights[idx].color = 'yellow'
        this.score++
      }
      console.log(this.score)
    },

    reset(){
      this.lights.forEach( light =>
        light.color = 'darkgrey'
      )
    }

  }
}

</script>

<style lang="sass">
body
  background-color: black
  margin: 0
</style>

<!--
  vi:et:sw=2:ts=2
-->
