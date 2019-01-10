<template>
  <div id="app">
    <leftside></leftside>

    <div class="main">
      <router-view/>
    </div>
  </div>
</template>

<script>
import leftside from '@/components/LeftSide' // 注意引入用小写 因为下面要写组件标签化
export default {
  name: 'App',
  components: {
    leftside
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  /* width: 100%; */
  height: 100%;
}
/* #app .pos::after {   只能父级在伪类清除浮动
  content: '';          在浮动区域最后加个标签并clear:both
  display: block;       父类触发BFC
  height: 0;            以上是清除浮动的三种方式
  clear: both;
} */
#app .main{
  width: 94%;
  height: 100%;
  float: left;
}
</style>
