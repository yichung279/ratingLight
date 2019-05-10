<template lang="pug">
#app(@click='test')
  svg(:width="width", :height="height")
    rect(:x="0.42*width", :y="0", :width="0.16*width", :height="height", fill="#ffee33")
    svg(v-for="(light, i) in lights")
      rect(:x="0.45*width", :y="i*light.height+0.07*height", :width="0.1*width", :height="light.height-padding", :fill="light.color")
      text(:x="0.5*width", :y="(i+0.9)*light.height+0.07*height", text-anchor="middle", :font-size="0.8*light.height", fill="black") {{2*judge - i}}
    rect(:x="0.45*width", :y="Math.ceil(0.6*judge)*0.85*height/judge/2-padding+0.07*height", :width="0.1*width", :height="2*padding", fill="red")
    rect(:x="0.44*width", :y="0.01*height", :width="0.12*width", :height="0.05*height", fill="orange")
    text(:x="0.5*width", :y="0.05*height", text-anchor="middle", :font-size="0.04*height", fill="#ffff66") UIDD+SWR
    rect(:x="0.43*width", :y="0.925*height", :width="0.14*width", :height="0.07*height", fill="red")
    circle(:cx="0.475*width", :cy="0.96*height", :r="0.03*height", fill="yellow")
    circle(:cx="0.525*width", :cy="0.96*height", :r="0.03*height", fill="yellow")

</template>

<script>
export default {

  created() {
    let lights = []
    for(let i=0; i < this.judge * 2; i++)
      lights.push({
        height: 0.85*this.height / (this.judge * 2),
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
            light.color = 'orange'
        else if(2*this.judge - i  > newVal)
          light.color = 'darkgrey'
      })
    }
  }
}

</script>

<style lang="sass">
body
  /* background-color: black */
  margin: 0
</style>

<!--
  vi:et:sw=2:ts=2
-->
