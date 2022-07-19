<template>
  <lifecycle></lifecycle>
</template>

<script>
import lifecycle from '@/components/lifecycle/lifecycle'
export default {
  name: 'App',
  components: {
    lifecycle,
  },
  data() {
    return {
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
