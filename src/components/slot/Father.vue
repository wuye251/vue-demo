<template>
  <Children>
    这是父组件的内容
    <template v-slot:slot1>slot1</template>
    <template v-slot:slot2>slot2</template>
    <template v-slot:slot3>slot3</template>
    
    <template v-slot:slot4>slot4</template>

  </Children>
</template>

<script>
import { defineComponent } from 'vue'
import Children from '@/components/slot/Children'

export default defineComponent({
  components: {
    Children
  },
})
</script>