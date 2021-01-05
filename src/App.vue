<template>
  <div id="app">
    <div v-if="son" class="titre">{{son.titre}}</div>
    <div class="balls">
      <Ball v-for="i in 20"></Ball>
    </div>

    <button @click="go"></button>

    <audio v-if="son" ref="son" :src="son.url" preload loop></audio>

  </div>
</template>

<script>
  import Ball from './components/Ball.vue'

  export default {
    name: 'App',
    components : {Ball},
    data() {
      return {
        son:false,
        rang:0,
        sons : [
        {
          titre: 'Grenouilles',
          url : 'https://sopress.s3.eu-central-1.amazonaws.com/veilleuse/frogs.mp3'
        },
        {
          titre: 'Bruit blanc',
          url : 'https://sopress.s3.eu-central-1.amazonaws.com/veilleuse/03-White-Noise-10min.mp3'
        },
        {
          titre: 'Sèche linge',
          url : 'https://sopress.s3.eu-central-1.amazonaws.com/veilleuse/16-Dryer-10min.mp3'
        },
        {
          titre: 'Océan',
          url : 'https://sopress.s3.eu-central-1.amazonaws.com/veilleuse/25-Ocean-10min.mp3'
        },
        {
          titre: 'Pluie',
          url : 'https://sopress.s3.eu-central-1.amazonaws.com/veilleuse/42-Rain-10min.mp3'
        },
        {
          titre: 'Vagues',
          url : 'https://sopress.s3.eu-central-1.amazonaws.com/veilleuse/45-Waves-10min.mp3'
        }

        
        
        ]
      }
    },
    methods: {
      changerSon() {
        if(this.$refs['son']) {
          this.$refs['son'].pause();
        }

        this.son=this.sons[this.rang];
        this.rang++;
        if(this.rang==this.sons.length){
          this.rang=0;
        }
        console.log(this.son.titre)

        setTimeout(() => {
          this.$refs['son'].play();
        },100);

      },
      go(){
        if (document.fullscreenEnabled) {
          if (!document.fullscreenElement) {
            document.documentElement.requestFullscreen();
          }
        }
        this.changerSon();


      }
    },
    mounted(){

      this.changerSon();

    }
  }
</script>

<style>
.titre {
  color:white;
  font-family: "Comic sans ms";
  margin:1em;
}
#app {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: linear-gradient(124deg, #ff2400, #e81d1d, #e8b71d, #e3e81d, #1de840, #1ddde8, #2b1de8, #dd00f3, #dd00f3);
  background-size: 1800% 1800%;

  animation: rainbow 30s ease infinite;
}

button {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  opacity: 0
}

.balls {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}


@-webkit-keyframes rainbow {
  0%{background-position:0% 82%}
  50%{background-position:100% 19%}
  100%{background-position:0% 82%}
}
@-moz-keyframes rainbow {
  0%{background-position:0% 82%}
  50%{background-position:100% 19%}
  100%{background-position:0% 82%}
}
@-o-keyframes rainbow {
  0%{background-position:0% 82%}
  50%{background-position:100% 19%}
  100%{background-position:0% 82%}
}
@keyframes rainbow { 
  0%{background-position:0% 82%}
  50%{background-position:100% 19%}
  100%{background-position:0% 82%}
}
</style>
