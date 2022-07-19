<template>
    <div>lifecycle</div>
    <button @click="counter++">{{counter}}</button>
</template>

<script>

export default {
    data() {
        return {
            counter: 0
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