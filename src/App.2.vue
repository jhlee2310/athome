<template>
<div>
  <div class="wrap" style="position:relative">
    <div class="player">
      <span>Player</span>
    </div>
    
  </div>
  <div>
    <div>Pannel</div>
    <div>
      <input/><input/><input/><button @click="q(opt)">submit</button>
    </div> 
  </div>
</div>
</template>
<script>
  import Ani from '@/assets/js/animate.js'
  import * as THREE from 'three'
  import Vue from 'vue/dist/vue.js'
  
  export default{    
    data(){
      return{
        opt:{
          what: 'translateX',
          how: '400',
          duration: 1000,
          easing: 'easeInOutBounce',
          fps: 60
        }
      }
    },

    methods: {
      q(_opt){
        const $obj = document.querySelector('.player')
        const w = () => {

        const { what,how,duration,easing,fps } = _opt
        const ease = Ani.easing[easing]

        console.log(ease)
        // how? +400
        // howLong? 10s
        // easing? easeInOutQuad
        // fps 60f / 1s
        // frame = 600f
        // dt = 10000ms / 600f    
       
          return new Promise( resolve => {
            let frame = fps * duration / 1000;
            let _timestep = duration / frame;            
            let cnt = 0
            let delta = how / frame;
            let value = 0;
            const _do = () => {              
              if (cnt++ == frame) {
                resolve()
                clearInterval(timer)
                return
              }
              value = ease(_timestep*cnt,0,9999,1000)

              //$obj.style.transform = `translate3d(${value}px,${value}px,0)`
              $obj.style.transform = `perspective(1px) rotateX(${value}deg)`
              //console.log(ease(_timestep*cnt,0,400,1000))   // t, b, c, d
            }
            const timer = setInterval(_do,_timestep)
            
          })

          
        }
        const run = async()=>{
          await w()

          console.log('done')
        }
        
        run()
      },
      stop(){

      }
    },        
    beforeCreate(){
      window.Ani = Ani;
      


    },    
  }
</script>
<style>
.wrap{width:1000px;height:500px;border:1px solid black}
.player{width:100px;height:100px;background-color: red;box-Sizing:border-Box;border:1px solid black;display:flex;position:absolute;
top:300px;left:300px}
</style>