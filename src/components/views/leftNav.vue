<template>
    <div class="left-nav">
      <ul>
        <li>
          <i class="icon iconfont icon-wodezichan"></i>
          收银
        </li>

        <li>
          <i class="icon iconfont icon-dianpu"></i>
          店铺
        </li>

        <li>
          <i class="icon iconfont icon-hanbao"></i>
          商品
        </li>

        <li>
          <i class="icon iconfont icon-huiyuanqia"></i>
          会员
        </li>


        <li>
          <i class="icon iconfont icon-tongji"></i>
          统计
        </li>
      </ul>
    </div>
</template>
<script>
    export default {
        name : 'leftNav',
        data () {
            return{

            }
        }
    }
</script>
<style>
  .left-nav{
    color:#fff;
    font-size:10px;
    height:100%;
    background-color: #1D8ce0;
    float:left;
    width: 100%;
  }
  .iconfont{
    font-size:24px;
  }
  .left-nav ul{
    padding:0px;
    margin: 0px;
  }
  .left-nav li{
    list-style: none;
    text-align: center;
    border-bottom:1px solid #20a0ff;
    padding:10px;
  }
</style>
