<template>
  <div id="app">
    <div>
      <img src="http://pic8.photophoto.cn/20080703/0012024452706524_b.jpg">
      <h1>有什么卖什么料理店</h1>
    </div>
    <assemblylrft></assemblylrft>
    <assembly></assembly>
    <router-view/>
  </div>
</template>

<script>
import assemblylrft from '@/components/assembly/assemblyleft'
import assembly from '@/components/page/assembly'

export default {
  name: 'App',
  components:{
    assemblylrft,
    assembly
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
html,body{
  height: 100%;
   margin: 0;
   padding: 0;
}
#app h1{
  text-align: center;
  color: 	Fuchsia;
}
#app img{
  width: 5%;
  height: 5% auto;
}

</style>
