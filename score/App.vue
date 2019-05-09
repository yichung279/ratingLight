<template lang="pug">
#app(@click='test')
  svg(:width="width", :height="height")
    rect(:x="0.89*width", :y="Math.ceil(0.6*judge)*height/judge/2-padding", :width="0.1*width", :height="2*padding", fill="red")
    svg(v-for="(light, i) in lights")
      rect(:x="0.89*width", :y="i*light.height", :width="0.1*width", :height="light.height-padding", :fill="light.color")
      text(:x="0.94*width", :y="(i+0.9)*light.height", text-anchor="middle", :font-size="0.8*light.height", fill="black") {{2*judge - i}}
</template>

<script>
export default {

  created() {
    let lights = []
    for(let i=0; i < this.judge * 2; i++)
      lights.push({
        height: this.height / (this.judge * 2),
        color: 'darkgrey'
      })
    this.lights=lights
  },

  data(){return{
    height: window.innerHeight,
    lights: [],
    // {
    //   height: 100
    //   color: 'darkgrey'
    // }
    judge: 10,
    score: 10,
    padding: 1,
    width: window.innerWidth
  }},

  methods:{
    test() {
      this.score++
    }
  },

  watch:{
    score(newVal){
      this.lights.forEach((light, i) => {
        if(2*this.judge - i <= newVal)
          if(0.6*this.judge > i)
            light.color = 'red'
          else if(0.6*this.judge <= i)
            light.color = 'yellow'
        else if(2*this.judge - i  > newVal)
          light.color = 'darkgrey'
      })
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
