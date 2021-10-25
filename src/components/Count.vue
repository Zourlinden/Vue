<template>
  <div>
      <h5>Count 组件</h5>
      <p>count 的值是：{{ count }}</p>
      <button @click="add">+1</button>
  </div>
</template>

<script>
export default {
    // props 是自定义属性，允许使用者通过自定义属性，为当前组件指定初始值
    // 自定义属性的名字，是封装者自定义的
    // props 中的数据，可以直接在模板结构中被使用
    // props 是只读的，不要直接修改props的值，否则终端会报错
    // props: ['init'],
    props: {
        init: {
            // 提供默认值
            default: 0,
            // init的值必须是Number 数字
            type: Number,
            // 必填项校检
            // required: true
        }
    },
    data() {
        return {
            count: this.init,
        }
    },
    methods: {
        add() {
            this.count++;
        }
    }
}
</script>

<style lang="less">

</style>