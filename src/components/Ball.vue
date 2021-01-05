<template>
  <div class="ball" ref="ball" :style="{background,left,top,transform,width,height}">

  </div>
</template>

<script>
  export default {
    data() {
      return  {
        // colors : ["#3CC157", "#2AA7FF", "#1B1B1B", "#FCBC0F", "#F85F36"],
        colors : ["#FFFFFF"],
        background : false,
        left:0,
        top:0,
        transform:false,
        width:0,
        height:0,
        to:{
          x: 0,
          y: 0
        }

      }
    },
    mounted() {
      this.background = this.colors[Math.floor(Math.random() * this.colors.length)];

      this.left = `${Math.floor(Math.random() * 100)}vw`;
      this.top = `${Math.floor(Math.random() * 100)}vh`;
      this.transform = `scale(${Math.random()})`;
      this.width = `${Math.random()*10}em`;
      this.height = this.width;
      let random = Math.floor(Math.random() * 10);

      this.to.x = Math.random() * ( random % 2 === 0 ? -11 : 11);
      this.to.y = Math.random() * 12

      let anim = this.$refs['ball'].animate(
        [
          { transform: "translate(0, 0)" },
          { transform: `translate(${this.to.x}rem, ${this.to.y}rem)` }
        ],
          {
            duration: (Math.random() + 1) * 2000,
            direction: "alternate",
            fill: "both",
            iterations: Infinity,
            easing: "ease-in-out"
          }
        );


    }
  }
</script>

<style>
.ball {
  position: absolute;
  border-radius: 100%;
  opacity: 0.9;
}
</style>
