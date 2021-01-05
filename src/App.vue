<template>
  <div id="app" :style="{backgroundColor:background}">
    <div v-if="son" class="titre">{{son.titre}}</div>
    <div class="balls">
      <Ball v-for="i in 20"></Ball>
    </div>

    <button @click="go"></button>

    <audio v-if="son" ref="son" :src="son.url" loop></audio>

  </div>
</template>

<script>
  import Ball from './components/Ball.vue'

  export default {
    name: 'App',
    components : {Ball},
    data() {
      return {
        background:'orange',
        backgrounds : [
        '#ff2400','#e81d1d','#e8b71d','#e3e81d','#1de840','#1ddde8','#2b1de8','#dd00f3','#dd00f3','#fee100'
        ],
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
      changerCouleur() {
        this.background = this.backgrounds[Math.floor(Math.random() * this.backgrounds.length)];
      },
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
      this.sons.forEach(son => {
        let audio = new Audio();
        audio.src = son.url;
      })


      this.changerSon();
      setInterval(this.changerCouleur,5000)

    }
  }
</script>

<style>
.titre {
  color:white;
  font-family: Comic Sans MS, Comic Sans, cursive;
  margin:1em;
  position: absolute;
  bottom: 0;
}
#app {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: white;
  transition: background-color 1s ease;
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



</style>
