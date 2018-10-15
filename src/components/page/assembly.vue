<template>
    <div class="assembly">
        <el-row :gutter="24">
            <el-col :span="7" class="assembly-one" id="assembly-one1">
               <el-tabs>
                   <el-tab-pane label="点餐">
                       <el-table :data="oftercommodity" border>
                           <el-table-column prop="goodName" label="商品"></el-table-column>
                           <el-table-column prop="price" label="金额"></el-table-column>
                           <el-table-column prop="count" label="数量" ></el-table-column>
                       </el-table>
                   </el-tab-pane>
                   <el-tab-pane  label="挂单"></el-tab-pane>
                   <el-tab-pane  label="结账"></el-tab-pane>
                </el-tabs>
                         <div class="closecommodity">
                             <b>数量：</b>{{totalCount}}  &nbsp;&nbsp;&nbsp;  <b>总价：</b>{{totalPrice}}
                        </div>
                    <el-button type="primary" @click="checkout">结账</el-button>
                    <el-button type="info">挂单</el-button>
                    <el-button type="danger" @click="delallgoods">重置</el-button>
            </el-col>
            <el-col :span="15" class="product" >
                <div class="allproduct">全部商品</div>
                 <div class="commodity0">
                 <ul>
                     <li v-for="good in allcommodity" :key="good.id" @click="addcommodity(good)">
                         <span class="goodsName">{{good.goodName}}</span>
                         <span class="goodsPrice">{{good.price}}</span>
                     </li>
                 </ul>
                 </div>
         <div class="commodity1">
            <el-tabs>
                <el-tab-pane label="主食">
                    <ul>
                        <li v-for="good in type0Goods" :key="good.id" @click="addcommodity(good)">
                            <span class="goodsImg"><img :src="good.goodsImg" style="width:110px"></span>
                            <span class="goodsName">{{good.goodName}} </span>
                            <span class="goodsprice">{{good.price}} </span>
                        </li>
                    </ul>
                </el-tab-pane>
                <el-tab-pane label="寿司">
                    <ul>
                        <li v-for="good in type1Goods" :key="good.id" @click="addcommodity(good)">
                            <span class="goodsImg"><img :src="good.goodsImg" style="width:110px"></span>
                            <span class="goodsName">{{good.goodName}} </span>
                            <span class="goodsprice">{{good.price}} </span>
                        </li>
                    </ul>
                </el-tab-pane>
                <el-tab-pane label="小食">
                     <ul>
                        <li v-for="good in type2Goods" :key="good.id" @click="addcommodity(good)">
                            <span class="goodsImg"><img :src="good.goodsImg" style="width:110px"></span>
                            <span class="goodsName">{{good.goodName}} </span>
                            <span class="goodsprice">{{good.price}} </span>
                        </li>
                    </ul>
                </el-tab-pane>
                <el-tab-pane label="饮料">
                     <ul>
                        <li v-for="good in type3Goods" :key="good.id"  @click="addcommodity(good)">
                            <span class="goodsImg"><img :src="good.goodsImg" style="width:110px" ></span>
                            <span class="goodsName" >{{good.goodName}} </span>
                            <span class="goodsprice">{{good.price}} </span>
                        </li>
                    </ul>
                </el-tab-pane>
             </el-tabs>
       </div>
            </el-col>
         
        </el-row>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    data(){
        return{
        oftercommodity:[],
        allcommodity:[],
        type0Goods:[],
        type1Goods:[],
        type2Goods:[],
        type3Goods:[],

        totalPrice:0,
        totalCount:0,

    }},
    mounted:function(){
             var oneheight=document.body.clientHeight;
             document.getElementById('assembly-one1').style.height=oneheight+'px';
    },
    created(){
        axios.get('http://120.78.75.213:8080/cloudmusic/goods/dishesName')
        .then((Response)=>{
            //console.log(Response);
          this.allcommodity=Response.data;
        })
        .catch((error)=>{
            //console.log(error);
        } ),
        axios.get('http://120.78.75.213:8080/cloudmusic/goods/dishesKind')
        .then((Response)=>{
            console.log(Response.data);
            this.type0Goods=Response.data[0];
            this.type1Goods=Response.data[1];
            this.type2Goods=Response.data[2];
            this.type3Goods=Response.data[3];
        })
        .catch((error)=>{
            //console.log(error);
        })

    },
    methods:{
        addcommodity(good){
           this.totalCount=0;
           this.totalPrice=0;
            var isHave=false;
            for(var i=0;i<this.oftercommodity.length;i++){
                if(this.oftercommodity[i].goodId==good.goodId){
                    isHave=true; 
                }
            }
            if(isHave){
                //如果存在的话就进行数量添加
                //对数组进行过滤
                var arr = this.oftercommodity.filter(o =>o.goodId==good.goodId);
                arr[0].count++;
            }
            else{
                //如果不存在的话，就压入数组
               var pushfoods={goodId:good.goodId,goodName:good.goodName,price:good.price,count:1};
                this.oftercommodity.push(pushfoods);
            
            }
             this.oftercommodity.forEach((element)=>{
                 this.totalCount+=element.count;
                 console.log(this.totalCount)
                 console.log(element);
                 this.totalPrice+=(element.price*element.count);
             })    

            },
            //重置全部选中的商品
           delallgoods(){
              this.oftercommodity=[],
              this.totalCount=0,
              this.totalPrice=0
            },
            //模拟结账操作
            checkout(){
               if(this.totalCount!=0){
                this.oftercommodity=[],
                this.totalCount=0,
                this.totalPrice=0,
                this.$message({
                    message:'支付成功，欢迎您再次光临~',
                    type:'success',
                })
               }else{
                   this.$message.error('您在玩儿呢？')
               }
            },
            
            }
            
            }
</script>
<style>
.assembly{
    margin: 0;
    padding: 0;
}

.assembly-one{
    border-right: 1px solid black;
}
.el-tabs__item{
    height: 20%;
    font-weight: bold;
    font-size: 20px;
}
.allproduct{
    border-bottom: 2px solid #808080;
    text-align: center;
    font-size: 30px;
    background-color:	#1E90FF;
}
.commodity0 ul li{
    list-style: none;
    display: inline-block;
    width: 20%;
    padding: 10px;
    margin: 10px;
    text-align: left;
    border: 1px solid #D8BFD8;
  background-color:#EE82EE;
  cursor: pointer;

}
.commodity1 ul li{
    list-style: none;
    display: inline-block;
  margin: 10px;
    border: 1px solid #D8BFD8;
    font-size: 15px;
    text-align: left;
    }
    .goodsName,.goodsprice{
        display: block;
        text-align: center;
        cursor: pointer;
    }
    .closecommodity{
        border-bottom: 1px solid #D8BFD8;
        margin: 10px;
        text-align: center;
        padding-top: 10px;
    }

</style>
