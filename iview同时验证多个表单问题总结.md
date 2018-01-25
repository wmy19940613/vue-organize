##  iview同时验证多个表单问题总结

+ iview验证一个表单问题： 
    - 在上一篇文章中总结了iview表单验证的问题。其实有两种写法：在点击验证时，这样写时，注意在前面的方法中将要验证的form表单加进去。
```
<Form ref="addAreaForm" :model="addAreaForm" :rules="ruleValidate" :label-width="120"></Form>
//点击确认按钮
<Button type='primary' @click='addAreaOK("addAreaForm")'>确定</Button>

addAreaOK(name){
   this.$refs[name].validate((valid)=>{
    if (valid){
        alert('验证成功')
    }
   })
}
```
- 还有一种写法：保存按钮不传form表单，在验证时直接this.$refs.addpurchaseForm.validate
    
```
<Button type="primary" @click="handleSubmit">保存</Button>
this.$refs.addpurchaseForm.validate((valid) => {
            // console.log(valid)
               if (valid) {
                    alert('验证成功')
               }
   }）
```

+ iview验证多个表单问题：在多表单验证时，让页面中的两个form都通过校验才能保存。解决方法就是:先验证第一个，在第一个验证通过得里面，验证第二个。
  ```
    this.$refs.addpurchaseForm.validate((valid) => {
                // console.log(valid)  //第一层验证第一个表单
                   if (valid) {
                   this.$refs.gasDataForm.validate((valid) => {
                    // console.log(valid)//第二层验证第二个表单
                          if(valid){
                             alert('验证成功')
                          }
                        })
                 }
             })
  ```         
