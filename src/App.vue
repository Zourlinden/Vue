<template>
  <div class="app-container">
    <h1>App 根组件 --- {{ CountFromSon }}</h1>
    <hr />

    <input type="text" v-if="inputVisible" @blur="showButton" ref="iptRef">
    <button v-else @click="showInput">展示输入框</button>

    <div class="box">
      <!-- 渲染 Left 组件和 Right 组件 -->
      <Left :msg="message" :user="userInfo"></Left>
      <Right @numchange="getSonCount"></Right>
    </div>
  </div>
</template>

<script>
import Left from '@/components/Left.vue'
import Right from '@/components/Right.vue'
export default {
  data() {
    return {
      message: 'hello world',
      userInfo: { name : 'wsc', age: 18 },
      CountFromSon: 0,
      inputVisible: false,
    }
  },
  methods: {
    getSonCount(val){
      this.CountFromSon = val
    },
    showInput() {
      this.inputVisible = true
      this.$nextTick(() => {
        this.$refs.iptRef.focus()
      })
    },
    showButton() {
      this.inputVisible = false
    }
  },
  components: { Left, Right }
}
</script>

<style lang="less">
.app-container {
  padding: 1px 20px 20px;
  background-color: #efefef;
}
.box {
  display: flex;
}
</style>
