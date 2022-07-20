<template>
    <grand-son></grand-son>
</template>

<script>
    import { defineComponent } from 'vue'
    import GrandSon from '@/components/slot/GrandSon'
    export default defineComponent({
        components: {
            GrandSon,
        },
      data() {
        return {
          list: [1,2,3,4]
        }
      },
    })
    </script>