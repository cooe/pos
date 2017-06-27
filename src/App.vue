<template>
  <div id="app">
    <div id="head" class="row">
          <div class="col-md-6 logo"><img src="./assets/img/longxia.jpg" class="logo-img"></div>
          <div class="col-md-6 title"><h2>{{title}}</h2></div>
    </div>
    <div class="row">
      <div class="left col-md-1">
        <left-nav></left-nav>
      </div>
      <div class="right col-md-11">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
  import leftNav from '@/components/views/leftNav'
export default {
  name: 'app',
  components : {
      leftNav
  },
  data () {
      return {
          title:"南部肥肠，欢迎订餐"
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
  .logo{
    text-align: right;
  }
.logo-img{
  width: 220px;
}
  #head{
    padding:30px 10px;
    border-bottom: 1px solid #cccccc;
  }
  .title{
    padding-top: 20px;
  }
</style>
