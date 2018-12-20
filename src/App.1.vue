<template>
  <div>
    <div>
      <input v-model="qry" @keyup.enter="submit" /><button @click="submit">확인</button><button @click="submit2">이오스블랙</button> {{qry}}
      <div>
        <div v-for="j in json" style = "margin-bottom:20px">
          <div v-html="j.title" ></div>
          <div v-html="j.contents">{{j.contents}}</div>
        </div>
        <div>{{eos}}</div>
      </div>
    </div>
  </div>
</template>
<script>
  import * as THREE from 'three'
  import run3d from '@/assets/run3d.js'

  export default{
    data(){
      return {
        json: [],
        qry: '',
        eos:'',
      }
    },
    methods: {
      
        
    },
    created(){
      //run3d()
    },
    mounted(){

    }
  }
</script>
<style>

</style>