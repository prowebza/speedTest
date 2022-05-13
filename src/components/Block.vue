<template>
  <div class="block" v-if="showBLock" @click.prevent="stopTimer" :style="{'left':3}" >
    <p>Click Me</p>
  </div>
</template>

<script>
const rnd = (min, max) => Math.floor(min + Math.random() * max);
export default {

  name: "Block",
  props:['delay'],
  data(){
    return{
      showBLock:false,
      timer: null,
      reactTime:0,
      pleft:'',
      ptop:''
    }
  },
  methods:{
    blockShow(){
      this.pleft = String(rnd(0,window.innerWidth - 10)) + 'px';
      this.ptop = String(rnd(0,window.innerHeight - 10))  + 'px';
      console.log('left :' + this.pleft + ' Top:' + this.ptop);
      setTimeout(()=>{
        this.showBLock = true;
        this.startTimer();
      },this.delay);
    },
    stopTimer(){
      clearInterval(this.timer);
      console.log(this.reactTime);
      this.$emit('end',this.reactTime);
    },
    startTimer(){
      this.timer = setInterval(()=>{
        this.reactTime += 10
      },10)
    }
  },
  mounted() {
    this.blockShow();
  }
}
</script>

<style >
  .block{
    text-align: center;
    display: flex;
    width: 100px;
    height: 100px;
    background: #40BA82;
    border-radius: 100px;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    margin-top: 50px;
    margin-left: auto;
    margin-bottom: auto;
    margin-right: auto;
    position: absolute;
    left: v-bind(pleft);
    top: v-bind(ptop);
  }
</style>