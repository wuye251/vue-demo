<template>
    <!-- 通过v-bind 绑定到子组件message里 -->
    <!-- 可以通过v-bind(:)动态绑定  也可以传定值-->
    <!-- 目前通过msg变量传定值的没掌握  有解法的可以教教我 -->
    <Hello :mess1age='msg' aaa='msg'></Hello>
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