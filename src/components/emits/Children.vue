<template>
    <button @click="updateAge">updateAge</button>
</template>

<script>
import { defineComponent } from 'vue'
export default defineComponent({
    methods: {
        updateAge() {
            this.$emit('child-click', 'hahaha')
            console.log('Children.vue updateAge.msg', 'hahaha')
        }
    },
})
</script>