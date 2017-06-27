<template>
    <div class="pos">
        <div>
            <el-row>
              <el-col :span='7'>
                <el-tabs>
                  <el-tab-pane label="点餐">
                  </el-tab-pane>
                  <el-tab-pane label="挂单">
                  </el-tab-pane>
                  <el-tab-pane label="外卖">
                  </el-tab-pane>
                </el-tabs>
                <el-table :data="checkoutData" border show-summary style="width: 100%" >
                  <el-table-column prop="goodsName" label="商品"  ></el-table-column>
                  <el-table-column prop="count" label="量" width="50"></el-table-column>
                  <el-table-column prop="price" label="金额" width="70"></el-table-column>
                  <el-table-column  label="操作" width="100" fixed="right">
                    <template scope="scope">
                      <el-button type="text" size="small">删除</el-button>
                      <el-button type="text" size="small">增加</el-button>
                    </template>
                  </el-table-column>
                </el-table>
                <el-row>

                </el-row>
              </el-col>
              <!--商品展示-->
              <el-col :span="17">
                我是产品栏
              </el-col>
            </el-row>
        </div>
    </div>
</template>
<script>
  import ElRow from "element-ui/packages/row/src/row";
    export default {
      components: {ElRow},
      name : 'Pos',
      data () {
          return {
              checkoutData :[
                {
                    goodsName : '毛血旺',
                    price : 16,
                    count : 1
                },
                {
                  goodsName : '冬瓜汤',
                  price : 8,
                  count : 1
                },
                {
                  goodsName : '香辣鸡丁',
                  price : 12,
                  count : 1
                },
                {
                  goodsName : '蒜苗回锅肉',
                  price : 12,
                  count : 1
                }
              ]
          }
      },
      mounted:function(){
        var orderHeight=document.body.clientHeight;
        document.getElementById("order-list").style.height=orderHeight+'px';
      }
    }
</script>
<style>
</style>
