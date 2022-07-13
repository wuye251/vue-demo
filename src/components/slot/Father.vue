<template>
  <div>父组件：{{message}}</div>
  <Children></Children>
</template>

<script>
import { defineComponent } from 'vue'
import Children from '@/components/slot/Children'

export default defineComponent({
  components: {
    Children
  },
  data() {
    return {
      message: "Father.vue message"
    }
  },
  provide() {
    return {
      message: this.message
    }
  }
})
</script>