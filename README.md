# 2.组件化开发
- 数据污染： 如果多次复用一个组件， 为防止数据变化影响其他地方的同一组件数据变化， 
> data() 必须返回对象 而不是在外面先定义const对象后返回 这样会造成他们之间的数据污染
```vue
<!-- Content.vue -->
<template>
    <!-- hello组件可复用 这里用完  下面也能继续引入 -->
    <Hello></Hello>
    <div>
        <h2>{{msg}}</h2>
        <button @click="msg='改变后的值'">改变Conten中的msg值</button>
    </div>
</template>

<script>
import Hello from './Hello.vue'

//如果msg在外层此处声明为const返回
// const obj = {
//     msg: "全局",
// } 
export default {
    components: {
        Hello,
    },
    data() {
        //多次复用返回的是同一对象， 会相互污染
        // return obj
        return {
            msg:"我是content.vue"
        }
    },
}
</script>

<!-- App.vue -->
<template>
    <!-- 此处复用了两次 -->
  <Content></Content>
  <Content></Content>
</template>

<script>
import Content from './components/Content.vue'

export default {
  name: 'App',
  components: {
    Content,
  },
}
</script>
```

- 通过prop向子组件传递数据
```vue
<!-- Content.vue -->
<template>
    <!-- 通过v-bind 绑定到子组件message里 -->
    <!-- 可以通过v-bind(:)动态绑定  也可以传定值-->
    <!-- 目前通过msg变量传定值的没掌握  有解法的可以教教我 -->
    <Hello :message='msg' aaa='msg'></Hello>
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
<!-- Hello.vue 通过prop获取父组件传递的变量 -->
<template>
    Hello.vue
    <div>动态传递：{{message}}</div>
    <div>静态传递：{{aaa}}</div>
</template>

<script>
    export default{
        // 子组件通过props接受父组件Content.vue传递的变量
        props:['message', 'aaa']
    }
</script>

```

- [prop类型验证](https://v3.cn.vuejs.org/guide/component-props.html#prop-%E9%AA%8C%E8%AF%81)
```vue
<template>
    Hello.vue
    <div>动态传递：{{message}}</div>
    <div>静态传递：{{aaa}}</div>
</template>

<script>
    export default{
        // 子组件通过props接受父组件Content.vue传递的变量
        props: {
            message: {
                type:String,
                default: "你好", //如果上层不传该变量 则默认值为这个
                required: true, //必传
            }
        }
    }
</script>
```