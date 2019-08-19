<template>
    <div>
        <label>{{label}}</label>
        <slot></slot>
        <label v-if="validateStatus=='error'" class="error">
            {{errorMessage}}
        </label>
    </div>
</template>
<script>
export default {
    inject: ['form'],
    name: 'KFormItem',
    props: {
        label: {
            type:String,
            value: ''
        },
        prop: {
            type: String,
            value: ''
        }
    },
    data(){
        return {
            errorMessage: '',
            validateStatus: false
        }
    },
    methods: {
        getRules(){
            return this.form.rules[this.prop]
        },
        validate(data){
            if(data.name != this.prop) return
            const rules = this.getRules();
            if(Array.isArray(rules)){
                const rule_required = rules.find(v=>v.required)
                const rule_max = rules.find(v=>v.maxLength)
                if(rule_required.required && !data.val){
                    this.validateStatus = 'error';
                    this.errorMessage = rule_required.message
                    return false
                }else{
                    this.validateStatus = 'validating'
                }
                if(rule_max && data.val.length > rule_max.maxLength){
                    this.validateStatus = 'error';
                    this.errorMessage = rule_max.message;
                    return false
                }else{
                    this.validateStatus = 'validating'
                }
            }else{
                if(rules.required && !data.val){
                    this.validateStatus = 'error'
                    this.errorMessage = rules.message
                }else{
                    this.validateStatus = 'validating'
                }
            }
        }
    },
    created(){
        this.$bus.$on('KFormItem',(data)=>{
            this.validate(data)
        })
        
    }
}
</script>
<style>
    .error{
        color: red;
    }
</style>