<template>
  <k-form title="表单验证" :model="form" :rules="rules">
    <k-form-item label="姓名" prop="name">
      <k-input v-model="form.name" name="name">
      
      </k-input>
    </k-form-item>
    <k-form-item label="年龄" prop="age">
      <k-input v-model="form.age" name="age">

      </k-input>
    </k-form-item>
  </k-form>
</template>

<script>
import KForm from './components/Form'
import KFormItem from './components/FormItem'
import KInput from './components/Input'

export default {
  name: 'app',
  components: {
    KForm, KFormItem, KInput
  },
  data(){
    return {
      form: {
        name: '',
        age: ''
      },
      rules: {
        name: [
          {required: true, message: '用户名不能为空'},
          {maxLength: 10, message: '用户名长度不能大于10个字符'}
        ],
        age: {
          required: true,
          message: '年龄不能为空'
        }
      }
    }
  }
}
</script>

<style>

</style>
