<template>
  <Father></Father>
</template>

<script>

import { defineComponent } from 'vue'
import Father from '@/components/slot/Father' 
export default defineComponent({
  name: 'App',
  components: {
    Father,
  },
  data() {
    return {
    }
  },
})
</script>