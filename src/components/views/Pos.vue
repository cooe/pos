<template>
    <div class="pos">
        <div>
            <el-row>
              <el-col :span='7'>
                <el-tabs>
                  <el-tab-pane label="点餐">
                    <el-table :data="checkoutData" border show-summary style="width: 100%" >
                      <el-table-column prop="goodsName" label="商品"  ></el-table-column>
                      <el-table-column prop="count" label="量" width="50"></el-table-column>
                      <el-table-column prop="price" label="金额" width="70"></el-table-column>
                      <el-table-column  label="操作" width="100" fixed="right">
                        <template scope="scope">
                          <el-button type="text" size="small" @click="delSigleGoods(scope.row)">删除</el-button>
                          <el-button type="text" size="small" @click="addOrderList(scope.row)" >增加</el-button>
                        </template>
                      </el-table-column>
                    </el-table>
                  </el-tab-pane>
                  <el-tab-pane label="挂单">
                    有多少挂单可以结账
                  </el-tab-pane>
                  <el-tab-pane label="外卖">
                    有多少外卖可以吃
                  </el-tab-pane>
                </el-tabs>

                <span class="wrapper">
              <el-button type="success">结账</el-button>
              <el-button type="warning">挂单</el-button>
                  <el-button :plain="true" type="info">删除</el-button>
            </span>
              </el-col>
              <!--商品展示-->
              <el-col :span="17">
                  <!-- 热卖商品 -->
                  <el-row>
                    <div class="often-goods">
                      <div class="title">热卖商品</div>
                      <div class="often-goods-list">

                        <ul>
                            <li v-for="goods in hotGoods" v-on:click = "addOrderList(goods)">
                              <span>{{goods.goodsName}}</span>
                              <span class="o-price">￥{{goods.price}}元</span>
                            </li>
                        </ul>
                      </div>
                    </div>
                  </el-row>
                <!-- 所有商品 -->

                <el-row>
                  <hr>
                  <el-tabs>
                    <el-tab-pane label="主食">
                      <ul class='cookList'>
                        <li v-for="goods in type0Goods" v-on:click = "addOrderList(goods)">
                          <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                          <span class="foodName">{{goods.goodsName}}</span>
                          <span class="foodPrice">￥{{goods.price}}元</span>
                        </li>
                      </ul>
                    </el-tab-pane>
                    <el-tab-pane label="小食">
                      我爱吃小吃
                    </el-tab-pane>
                    <el-tab-pane label="饮料">
                      我爱喝可乐
                    </el-tab-pane>
                    <el-tab-pane label="套餐">
                      什么套餐可以吃
                    </el-tab-pane>
                  </el-tabs>
                </el-row>
              </el-col>
            </el-row>
        </div>
    </div>
</template>
<script>
  import ElRow from "element-ui/packages/row/src/row";
  import axios from 'axios'
    export default {
      components: {ElRow},
      name : 'Pos',
      data () {
          return {
              checkoutData :[

              ],
            hotGoods:[
            ],
            type0Goods:[
              {
                goodsId:1,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                goodsName:'香辣鸡腿堡',
                price:18
              }, {
                goodsId:2,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                goodsName:'田园鸡腿堡',
                price:15
              }, {
                goodsId:3,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                goodsName:'和风汉堡',
                price:15
              }, {
                goodsId:4,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                goodsName:'快乐全家桶',
                price:80
              }, {
                goodsId:5,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                goodsName:'脆皮炸鸡腿',
                price:10
              }, {
                goodsId:6,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                goodsName:'魔法鸡块',
                price:20
              }, {
                goodsId:7,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                goodsName:'可乐大杯',
                price:10
              }, {
                goodsId:8,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                goodsName:'雪顶咖啡',
                price:18
              }, {
                goodsId:9,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                goodsName:'大块鸡米花',
                price:15
              }, {
                goodsId:20,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                goodsName:'香脆鸡柳',
                price:17
              }

            ]
          }
      },
      created () {
          //读取远程数据
          axios.get('http://jspang.com/DemoApi/oftenGoods.php')
            .then(response=>{
                console.log(response);
                this.hotGoods = response.data;
            }).catch(error=>{
            console.log(error);
            alert('网络错误，不能访问');
          })
      },
      methods : {
          //从右侧添加商品到左侧结算处
          addOrderList(goods){
              this.totalCount = 0;
              this.totalMoney = 0;
              let isHave = false;//商品是否存在账单中
              let temp = 0;

            //判断商品是否存在账单中
            for(let i =0;i<this.checkoutData;i++){
              if(this.checkoutData[i].goodsId == goods.goodsId){
                    isHave = true;
                    temp = i ;
              }
            }
            //根据结果执行商品数量增加 或者商品新增的方法
            if(isHave){
               /* let arr = this.tableData.filter(o =>o.goodsId == goods.goodsId);
                arr[0].count++;*/
            }else{
                let newGoods = {goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                this.checkoutData.push(newGoods);
            }
            //统计商品总价
            this.checkoutData.forEach((element)=>{
                this.totalCount +=element.count;
                this.totalMoney = this.totalMoney + (element.price*element.count)
            });
          },
        delSigleGoods(goods){
          console.log(goods);
          //this.tableData=this.tableData.filter(o => o.goodsId !=goods.goodsId);
        }

      }
    }
</script>
<style>
  .title{
    height: 42px;
    border-bottom:1px solid #D3DCE6;
    background-color: #F9FAFC;
    padding:10px;
  }
  .often-goods-list ul li{
    list-style: none;
    float:left;
    border:1px solid #E5E9F2;
    padding:10px;
    margin:5px;
    background-color:#fff;
  }
  .o-price{
    color:#58B7FF;
  }
  .cookList li{
    list-style: none;
    width:23%;
    border:1px solid #E5E9F2;
    height: auot;
    overflow: hidden;
    background-color:#fff;
    padding: 2px;
    float:left;
    margin: 2px;

  }
  .cookList li span{

    display: block;
    float:left;
  }
  .foodImg{
    width: 40%;
  }
  .foodName{
    font-size: 18px;
    padding-left: 10px;
    color:brown;
  }
  .foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top:10px;
  }
</style>
