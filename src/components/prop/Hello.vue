<template>
    Hello.vue
    <div>动态传递：{{message}}</div>
    <div>静态传递：{{aaa}}</div>
</template>

<script>
    import { defineComponent } from 'vue'
    export default defineComponent({
        // 子组件通过props接受父组件Content.vue传递的变量
        props: {
            message: {
                type:String,
                default: "你好", //如果上层不传该变量 则默认值为这个
                required: true, //必传
            },
            aaa: {
                type:String,
                default: "你好", //如果上层不传该变量 则默认值为这个
                required: true, //必传 
            },
        },

        setup(props) {
            console.log('props',props)
            console.log('props.message', props.message)
        }
    })
</script>