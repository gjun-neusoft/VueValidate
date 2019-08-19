<template>
    <input type="text" @input="handleInput" v-model="inputValue"/>
</template>
<script>
export default {
    name:"kInput",
    props: {
        value: {
            type: String
        },
        name: {
            type: String
        }
    },
    data(){
        return {
            inputValue: this.value
        }
    },
    created(){
        // this.$emit('input')
    },
    methods: {
        handleInput(e){
            this.$bus.$emit('KFormItem', {val: this.inputValue, name: this.name})
        }
    }
}
</script>
<style>
    
</style>