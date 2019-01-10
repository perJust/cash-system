<template>
  <div class="leftSide">
    <ul class="sider">
      <li>
        <i class="icon iconfont icon-wodedingdan"></i> <!-- icon这个类可以不用  但是为了后期自己方便管理图标而已 -->
        <p>付款</p>
      </li>
      <li>
        <i class="icon iconfont icon-shouye"></i>
        <p>店铺</p>
      </li>
      <li>
        <i class="icon iconfont icon-gouwuche"></i>
        <p>商品</p>
      </li>
      <li>
        <i class="icon iconfont icon-jushoucang"></i>
        <p>会员</p>
      </li>
      <li>
        <i class="icon iconfont icon-wancheng"></i>
        <p>统计</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'LeftSide'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.leftSide {
  width: 6%;
  height: 100%;
  float: left;
  font-size: 10px;
  text-align: center;
  background-color: #47a5f1;
}
.sider {
  width: 100%;
  height: 100%;
  padding: 0;
}
.sider li {
  padding: 10px;
  cursor: pointer;
}
.iconfont {
  font-size: 24px;
}
</style>
