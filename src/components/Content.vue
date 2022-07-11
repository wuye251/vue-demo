<template>
    <!-- 通过v-bind 绑定到子组件message里 -->
    <Hello :message='msg'></Hello>
    <div>
        <h2>{{msg}}</h2>
        <button @click="msg='改变后的值'">改变Conten中的msg值</button>
    </div>
</template>

<script>
import Hello from './Hello.vue'

export default {
    components: {
        Hello,
    },
    data() {
        return {
            msg:"我是content.vue"
        }
    },
}
</script>