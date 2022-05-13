<template>
  <h1>MindSpeed Tester</h1>
  <br>

  <br>
  <input @click.prevent="startGame" :disabled="isPlaying" value="Start Game" :type="isPlaying ? 'button' : 'text'" class="btn btn-outline-dark">
  <Block @end="resault" :delay="isPlaying ? delay : ''" v-if="isPlaying"/>
  <Resault v-if="!isPlaying && gameEnd">
    <template v-slot:header>
      <h1>Ur Time Was : {{score}}</h1>
      <h2>{{ League }} League</h2>
    </template>
  </Resault>
</template>

<script>
import Block from "@/components/Block";
import Resault from "@/components/Resault";

export default {
  name: 'App',
  components: {
    Block,
    Resault
  },
  data(){
    return{
      delay:null,
      isPlaying:false,
      score:0,
      League:'',
      gameEnd:false,
      namee:''
    }
  },
  methods:{
    startGame(){
      console.log('Called');
      if (!this.isPlaying){
        this.resetData();
        this.delay = 1000 + Math.random() * 6000;
      }
    },
    resault(reactTime){
      this.isPlaying = false;
      this.score = reactTime;
      this.gameEnd = true

      this.leaguee();
    },
    leaguee(){
      if (this.score <= 300){
        this.League = 'Flash'
      }else if (this.score <= 600){
        this.League = 'fat flash'
      }else if(!(this.score <= 0)){

      }
      else{
        this.League = 'snail'
      }
    },
    resetData(){
      this.gameEnd = false;
      this.isPlaying = true;
      this.delay = null;
      this.score = 0;
      this.League = '';
    }
  },
  mounted() {
    console.log(window.innerWidth)

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.btn.btn-outline-dark{
  background: none;
  font-size: 15px;
  border: solid #242424;
  border-radius: 5px;
  padding: 8px;
  color: #242424;
  transition: all ease-in-out 0.1s;
}
.btn.btn-outline-dark:hover{
  background: #242424;
  color: white;
}
</style>
