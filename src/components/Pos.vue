<template>
    <div class="posCore">
      <el-row>
        <el-col :span="8" id="order-list">
          <el-tabs>
            <el-tab-pane label="结账">
              <el-table :data="tableData" style="width:100%;text-align:left;" border >
                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                <el-table-column prop="count" label="数量" width="80"></el-table-column>
                <el-table-column prop="price" label="单价" width="80"></el-table-column>
                <el-table-column label="操作" fixed="right">
                  <template slot-scope="scope">
                      <el-button type="text" size="small" @click="delGoodsList(scope.row)">删除</el-button>
                      <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button> <!-- scope.row获取该行的数据内容 -->
                  </template>
                </el-table-column>
              </el-table>
              <div style="width:100%;background-color:#fff;text-align:center;font-size:16px;height:32px;line-height:32px;border: 1px solid #e5e9f2;">
                <span style="margin-right:20px;"><small>数量:</small>{{orderListCount}}</span><span><small>总价:￥</small>{{orderListPay}}</span>
              </div>
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAllGoods">删除</el-button>
              <el-button type="success" @click="checkout">结账</el-button>
            </el-tab-pane>
            <el-tab-pane label="挂单">
              2
            </el-tab-pane>
            <el-tab-pane label="外卖">
              3
            </el-tab-pane>
          </el-tabs>
        </el-col>
        <el-col :span="16">
          <el-row>
            <el-col :span="24" style="margin-bottom:60px;">
              <div class="often-goods-title">常用商品</div>
              <div class="often-goods-list">
                <ul>
                  <li v-for="(goods, item) in oftenGoods" :key="item" @click="addOrderList(goods)">
                    <span>{{goods.goodsName}}</span>
                    <span class="o-price">￥{{goods.price}}</span>
                  </li>
                </ul>
              </div>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="24">
              <el-tabs>
                <el-tab-pane label="汉堡">
                  <ul class="cookList">
                    <li  v-for="(goods,item) in type0Goods" :key="item" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" alt="汉堡"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}</span>
                    </li>
                  </ul>
                </el-tab-pane>
                <el-tab-pane label="小食">
                  <ul class="cookList">
                    <li v-for="(goods,item) in type1Goods" :key="item" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" alt="小食"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}</span>
                    </li>
                  </ul>
                </el-tab-pane>
                <el-tab-pane label="饮料">
                  <ul class="cookList">
                    <li v-for="(goods,item) in type2Goods" :key="item" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" alt="饮料"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}</span>
                    </li>
                  </ul>
                </el-tab-pane>
                <el-tab-pane label="套餐">
                  <ul class="cookList">
                    <li v-for="(goods,item) in type3Goods" :key="item" @click="addOrderList(goods)">
                      <span class="foodImg"><img :src="goods.goodsImg" alt="套餐"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}</span>
                    </li>
                  </ul>
                </el-tab-pane>
              </el-tabs>
            </el-col>
          </el-row>
        </el-col>
      </el-row>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'pos',
  data () {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: []
      // orderListCount: 0,
      // orderListPay: 0
    }
  },
  methods: {
    addOrderList (goods) {
      // 判断列表内是否已有商品数据
      let ishave = false
      const list = this.tableData // 这是优化代码
      const len = list.length
      //  for (const g in list) {
      //   // this.table是数组,for...in出来的g是index索引
      //   if (list[g].goodsId === goods.goodsId) {
      //     ishave = true
      //     list[g].count++
      //   }
      // }
      for (let i = 0; i < len; i++) {
        if (list[i].goodsId === goods.goodsId) {
          ishave = true
          list[i].count++
        }
      }
      //
      // 做判断后的逻辑处理
      let arr = []
      if (!ishave) {
        arr = {...Object.assign({}, goods), count: 1} // 复制选中的商品数据 并添加count
        this.tableData.push(arr)
      }
    },
    delGoodsList (goods) {
      this.tableData = this.tableData.filter(o => o.goodsId !== goods.goodsId)
    },
    delAllGoods () {
      this.tableData = []
    },
    checkout () {
    //   axios.post('...', {
    //     id:
    //     count:
    //     ...
    //   })
    // }
      if (this.tableData.length) {
        this.$message({
          message: '结账成功',
          type: 'success'
        })
      } else {
        this.$message({
          message: '暂无商品',
          type: 'error'
        })
      }
      this.tableData = []
    }
  },
  computed: {
    orderListCount () {
      return this.tableData.reduce(function (total, ind) {
        return total + ind.count
      }, 0) // 起始值必须要写  不写默认起始值就是数组的第一位 如果是第一位在这里作为起始值那就会error
    },
    orderListPay () {
      return this.tableData.reduce(function (total, ind) {
        return total + ind.count * ind.price
      }, 0)
    }
  },
  created () {
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods').then(response => {
      this.oftenGoods = response.data
      // console.log(response)
    }).catch(err => {
      console.log(err)
    })
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods').then(response => {
      let data = response.data
      this.type0Goods = data[0]
      this.type1Goods = data[1]
      this.type2Goods = data[2]
      this.type3Goods = data[3]
    }).catch(err => {
      console.log(err)
    })
  },
  mounted () {
    var clientHeight = document.body.clientHeight
    document.getElementById('order-list').style.height = clientHeight + 'px'
  }
}
</script>

<style>
.posCore {
  height: 100%;
  width: 100%;
  text-align: center;
}
/* #order-list { 不起作用 因为element-ui组件内有固定定义
  height: 100% !important;
} */
#order-list {
  border-right: 1px solid #c0ccda;
  background-color: #f9fafc;
}
.often-goods-title {
  height: 20px;
  border-bottom: 1px solid #f9fafc;
  background-color: #f9fafc;
  padding: 10px;
  text-align: left;
}
.often-goods-list ul li {
  width: 22%;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 6px;
  background-color: #fff;
  cursor: pointer;
}
.often-goods-list ul li:hover {
  background-color: #888;
}
.cookList li {
  width: 24%;
  border: 1px solid #e5e9f2;
  height: auto;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
  cursor: pointer;
}
.cookList li:hover {
  background-color: #888;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
}
.foodImg img {
  width: 100%;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}
.footPrice {
  font-size: 16px;
  padding-left: 10px;
}
</style>
