<template>
    <div>lifecycle</div>
    <button @click="test">{{counter}}</button>
</template>

<script>
import {ref} from 'vue';
export default {
    data() {
        return {
            counter: 0
        }
    },
    setup() {
        console.log('setup');
        const counter = ref(0)
        function test() {
            counter.value++
        }

        return {
            counter,
            test,
        }
    },

    beforeCreate() {
        console.log('beforeCreate')
    },
    created() {
        console.log('Created')
    },
    beforeMount() {
        console.log('beforeMount')
    },
    mounted() {
        console.log('mounted')
    },

    beforeUpdate() {
        console.log('beforeUpdate')
    },

    updated() {
        console.log('updated')
    },

    beforeUnmount() {
        console.log('beforeUnmount')
    },

    unmounted() {
        console.log('unmounted')
    },
}
</script>