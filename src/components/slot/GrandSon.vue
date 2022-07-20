<template>
    <div>孙组件：{{message}}</div>
</template>

<script>
    import { defineComponent } from 'vue'
    export default defineComponent({
        inject:['message'],
        created() {
            console.log('inject message:', this.message)
        }
    })
</script>