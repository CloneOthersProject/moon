# Form 表单验证

<ClientOnly>
  <form-demo/>
</ClientOnly>

**验证规则依赖库 async-validator**

```vue
<template>
    <div>
        <m-form ref='form' :model="formValidate" :rules="ruleValidate">
            <m-form-item label="用户名" prop="name">
                <m-input v-model="formValidate.name"></m-input>
            </m-form-item>
            <m-form-item label="邮箱" prop="mail">
                <m-input v-model="formValidate.mail"></m-input>
            </m-form-item>
            <m-form-item label="选择" prop="group">
                <m-checkbox-group v-model='formValidate.group'>
                    <m-checkbox label='选项1'>选项1</m-checkbox>
                    <m-checkbox label='选项2'>选项2</m-checkbox>
                    <m-checkbox label='选项3'>选项3</m-checkbox>
                </m-checkbox-group>
            </m-form-item>
        </m-form>
        <m-button  @click='submitForm'>提交</m-button>
        <m-button @click='restForm'>重置</m-button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                formValidate: {
                    name: '',
                    mail: '',
                    group: []
                },
                ruleValidate: {
                    name: [{required: true, message: '用户名不能为空', trigger: 'blur'}],
                    mail: [
                        {required: true, message: '邮箱不能为空', trigger: 'blur'},
                        {type: 'email', message: '邮箱格式不正确', trigger: 'blur'}
                    ],
                    group: [{type: "array", required: true, message: '必须选一个', trigger: 'change'}],
                }
            }
        },
        methods: {
            submitForm() {
                this.$refs.form.validate(valid => {
                    if (valid) {
                        window.alert('提交成功')
                    } else {
                        window.alert('表单校验失败')
                    }
                })
            },
            restForm() {
                this.$refs.form.resetFields()
            }
        }
    }
</script>
```