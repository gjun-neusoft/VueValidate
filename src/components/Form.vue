<template>
    <form>
        <h3>{{title}}</h3>
        <slot>

        </slot>
    </form>
</template>
<script>
export default {
    provide(){
        return {
            form: this
        }
    },
    name: 'from',
    props: {
        title:{
            type: String,
            default: '',
            required: true
        },
        model: {
            type: Object,
            required: true
        },
        rules: {
            type: Object,
            required: true
        }
    },
    data(){
        return {
           
        }
    }
    
}
</script>
<style>
    
</style>