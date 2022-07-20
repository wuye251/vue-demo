<template>
    <children @child-click="fatherClick" ref="child"></children>
</template>

<script>
import { defineComponent, reactive, ref, onMounted } from 'vue'
import Children from '@/components/emits/Children'

export default defineComponent({
  components: {
    Children
  },

  setup () {
    const child = ref<HTMLElement>(null)
    
    onMounted(() => {
        console.log('child', child)        
    })
    // 定义一个更新年龄的方法
    const fatherClick = (msg) => {
        console.log('Father.vue fatherClick.msg', msg)
    }

    return {
      // return给template用
      fatherClick,
      child
    }
  }
})
</script>