<template>
  <div class="left-container">
    <h3>Left 组件</h3>
    <p>msg 的值是： {{ msg }}</p>
    <p>user 的值是：{{ user }}</p>
    <button @click="msg = 'abc'">修改msg</button>
    <button @click="user.name = 'zs'">修改user</button>
    <hr>
    <button @click="send">发给我的好兄弟数据</button>
  </div>
</template>

<script>
import bus from './eventBus.js'
export default {
  props: [ 'msg', 'user'],
  data() {
    return {
      str: '我的天啊，兄弟组件的数据共享竟然如此简单'
    }
  },
  methods: {
    send() {
      bus.$emit('share',this.str)
    }
  }
}
</script>

<style lang="less" scoped>
.left-container {
  padding: 0 20px 20px;
  background-color: orange;
  min-height: 250px;
  flex: 1;
}
h3 {
  color: red;
}
// 在父组件中使用子组件时使用/deep/
// 当使用第三方组件库的时候，如果有修改组件默认样式的需求，需要用到/deep/
/deep/ h5{
  color: pink;
} 
</style>
