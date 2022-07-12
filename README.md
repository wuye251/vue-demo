# 基础
- 语法糖： v-bind ：  v-on  @ 
- v-model实现原理 1.v-bind绑定数据 2.@input事件更新数据变量
# 组件化开发
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

## 组件之间的通信
> 即父子组件之间,获取对方的数据变量 大概有以下几种方式
> - v-model/ref/prop  父组件向子组件传值
> - emits/inject 子组件向父组件传值
> 下面详细记录各个方法的使用姿势

## 子组件获取父组件数据
### [prop](https://v3.cn.vuejs.org/guide/component-props.html#prop-%E9%AA%8C%E8%AF%81)

> 父组件通过prop向子组件传递数据： 
> 父组件<Children :message='msg'></Children>
> 子组件 props: [message] 页面{{message}}就可以拿到父组件中msg的值
> 注意： 在js中 如果要使用props传下来的值如setup 需要在参数中加上props 以props.message访问
```vue
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
            console.log('props.message', props.message) //应是
            console.log('this.message', this.message) //不应是
        }
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
        props:{
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
        }
    }
</script>

```
### [v-model](https://vue3.chengpeiquan.com/communication.html#v-model-emits)
> 父组件v-model传递数据 `<template>
  <Child
    v-model:user-name="userInfo.name"
  />
</template>`
> 子组件用prop接收即可 

## 父组件获取子组件数据
### [emits](https://vue3.chengpeiquan.com/communication.html#%E7%BB%91%E5%AE%9A-emits-new)
> 子组件向父组件传递数据修改事件
#### 举例

```vue
<!--Children.vue -->
<template>
	<!--子组件先绑定事件 -->
    <button @click="updateAge">updateAge</button>
</template>

<script>
import { defineComponent } from 'vue'
export default defineComponent({
    methods: {
        updateAge() {
            //通过this.$emit(father.func, 'param')传到父组件中
            this.$emit('child-click', 'hahaha')
            console.log('Children.vue updateAge.msg', 'hahaha')
        }
    },
})
</script>
<!--Father.vue -->
<template>
    <!--父组件以@子组件传递的 @father.func = fatherClick 绑定到父组件中的fatherClick事件中处理-->
    <children @child-click="fatherClick"></children>
</template>

<script>
import { defineComponent, reactive } from 'vue'
import Children from '@/components/emits/Children'


export default defineComponent({
  components: {
    Children
  },
  setup () {
    // 定义一个更新年龄的方法
    const fatherClick = (msg) => {
        console.log('Father.vue fatherClick.msg', msg)
    }

    return {
      // return给template用
      fatherClick
    }
  }
})
</script>
```



### [ref](https://vue3.chengpeiquan.com/communication.html#ref-emits)

>  还没掌握 目前是通过<Children ref="hello"></Children>这样设置后  在父组件的js里 就可以调用hello的方法了  


## slot槽

> 复用同一组件， 但是内容定制化修改， 会用到插槽

#### 举例

```vue
<!-- Children.vue -->
<template>
    <div> 
        这是每个复用该组件都显示的
        <slot></slot>
    </div>
</template>

<!--Father.vue -->
<template>
  <Children>
    这是父组件的内容
  </Children>
</template>

<script>
import { defineComponent, reactive, ref, onMounted } from 'vue'
import Children from '@/components/slot/Children'

export default defineComponent({
  components: {
    Children
  },
})
</script>
```

#### 具名插槽

> 一个组件 有多个插槽， 复用的对于各个插槽准确使用， 那就给每个插槽起个名字即可

```vue
<!--Father.vue-->
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

<!--Children.vue-->
<template>
    <div> 
        这是每个复用该组件都显示的
        <slot></slot>
        <slot name="slot1"></slot>
        <slot name="slot2"></slot>
        <slot name="slot3"></slot>
    </div>
</template>
```



#### 作用域插槽

#### 插槽备用内容



# 附录
- https://vue3.chengpeiquan.com/
- https://v3.cn.vuejs.org/guide/introduction.html