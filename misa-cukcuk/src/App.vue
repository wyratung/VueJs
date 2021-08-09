<template>
  <div id="app">
    <the-header/>
    <the-wrapper/>
    
  </div>
</template>

<script>
import TheHeader from "./components/layout/TheHeader.vue"
import TheWrapper from "./components/layout/TheWrapper.vue"
export default {
  name: "App",
  data(){
    return{

    }
  },
  components:{
    TheHeader,
    TheWrapper
  }
}
</script>
  
<style>
  @import url('./css/maincss.css');
</style>