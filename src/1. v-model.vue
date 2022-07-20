<template>
  <!-- v-model 修饰符的使用 -->
  <!-- 输入框失去焦点之后再更新msg -->
  <input type="text" v-model.lazy="msg" />
  <h4>{{ msg }}</h4>
  <!-- number修饰符 输入框自动转换为数字 -->
  <input type="text" v-model.number="mobile" />
  <h4>{{ mobile }}</h4>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      msg:"",
      mobile:0,
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
