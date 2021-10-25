<template>
  <div class="app-container">
    <Header></Header>
    <Goods 
      v-for="item in list" 
      :key="item.id" 
      :id="item.id"
      :title="item.goods_name"
      :pic="item.goods_img"
      :price="item.goods_price"
      :state="item.goods_state"
      :count="item.goods_count"
      @state-change="getNewState"
    ></Goods>
    <Footer 
      :isfull="fullState" 
      :amount="amt"
      :all="total"
      @full-change="getFullState"
    ></Footer>
  </div>
</template>

<script>
// 导入 axios 请求库
import axios from 'axios'
// 导入需要的组件
import Header from '@/components/Header/Header.vue'
import Goods from '@/components/Goods/Goods.vue'
import Footer from '@/components/Footer/Footer.vue'

import bus from '@/components/eventBus.js'

export default {
  data() {
    return {
      // 用来存储购物车的列表数据，默认为空
      list: []
    }
  },
  components: {
    Header,
    Goods,
    Footer
  },
  methods: {
    // 封装请求列表数据的方法
    async initCartList(){
      // 调用axios 的 get 方法，请求列表数据
      const { data: res } = await axios.get('https://www.escook.cn/api/cart')
      if(res.status === 200){
        this.list = res.list
      }
    },
    // 接受子组件传递过来的数据
    getNewState(e) {
      // e 的格式为 { id, value }
      this.list.some(item => {
        if(item.id === e.id){
          item.goods_state = e.value
          // 终止后续的循环
          return true
        }
      })
    },
    // 接受 Footer 子组件传递过来的全选按钮
    getFullState(val) {
      this.list.forEach(item => (item.goods_state =val))
    }
  },
  created() {
    this.initCartList()
    bus.$on('share',(val) => {
      this.list.some(item => {
        if(item.id === val.id){
          item.goods_count = val.value
          return true
        }
      })
    })
  },
  // 计算属性
  computed: {
    // 动态计算出全选的状态是 true 还是 false
    fullState() {
      return this.list.every(item => item.goods_state)
    },
    // 已勾选商品的总价格
    amt() {
      // 1.先filter过滤
      // 2.再reduce累加
      return this.list.filter(item => item.goods_state).reduce((total,item) => (total += item.goods_price * item.goods_count),0)
    },
    // 已勾选商品的总数量
    total() {
        return this.list.filter(item => item.goods_state).reduce((t,item) => (t += item.goods_count),0)
    }
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
