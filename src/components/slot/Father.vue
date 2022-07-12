<template>
  <Children>
    这是父组件的内容
  </Children>
</template>

<script>
import { defineComponent, reactive, ref, onMounted } from 'vue'
import Children from '@/components/slot/Children'

export default defineComponent({
  components: {
    Children
  },
})
</script>