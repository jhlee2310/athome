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
  import run3d from './assets/run3d.js'

  export default{
    data(){
      return {
        json: [],
        qry: '',
        eos:'',
      }
    },
    methods: {
      submit(){
        this.$axios.get(`/api/kakao_search?query=${this.qry}`).then(res => {
          this.json = res.data.documents
          this.qry = ''
          //console.log(this.json);
        }
      )},
      submit2(){
        this.$axios.get(`/api/eosblack`).then(res => {
          this.eos = res.data
          this.qry = ''
          //console.log(this.json);
        }
      )}
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