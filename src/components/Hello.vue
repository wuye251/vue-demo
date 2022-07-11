<template>
    Hello.vue
    {{message}}
</template>

<script>
    export default{
        // 子组件通过props接受父组件Content.vue传递的变量
        props:['message']
    }
</script>