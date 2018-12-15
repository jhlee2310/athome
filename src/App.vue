<template>
  <div>
    {{json}}
  </div>  
</template>
<script>
  export default{
    data(){
      return {
        json:''
      }
    },
    mounted(){
      this.$axios.get('http://localhost:4000').then(
        res => console.log(res)
      )
    }
  }
</script>
<style>

</style>