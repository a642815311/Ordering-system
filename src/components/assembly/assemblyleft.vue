<template>
  <div class="assemblyleft" id="howall">
      <ul>
          <li>
              <i class="icon iconfont icon-shangdian"></i>
              <div>商品</div>
          </li>
          <li>
              <i class="icon iconfont icon-kuanchuangyidianzishangwutubiaoshiliangsucai--"></i>
              <div>特价商品</div>
          </li>
          <li>
              <i class="icon iconfont icon-shouyin"></i>
              <div>收银</div>
          </li>
          <li>
              <i class="icon iconfont icon-huiyuan"></i>
              <div>会员</div>
          </li>
          <li>
              <i class="icon iconfont icon-shezhi"></i>
              <div>设置</div>
          </li>
      </ul>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  mounted:function(){
      var bodyHeight=document.body.clientHeight;
     console.log(bodyHeight)
  }
  
}
</script>


<style>
 .assemblyleft{
     color: 	white;
      height: 100%;
      width: 5%;
     background-color: #C0C0C0;
    float: left;
      }
.iconfont{
    font-size: 24px;
}
.assemblyleft ul{
    padding: 0;
    margin: 0;

}
.assemblyleft ul li{
    list-style: none;
    font-size: 20px;
    border-bottom: 2px solid black;
    text-align: center;
    padding: 20px;
}
</style>


