## 关于iview表单验证的问题

 
 - iview表单验证的步骤：
      
      - 第一步：给 Form 设置属性 rules   **:rules**
      - 第二步：同时给需要验证的每个 FormItem 设置属性 prop 指向对应字段即可 **prop=""**
      - 第三步：注意：Form标签里面是  **:model**
      - 第四步：注意：在Form标签里面必须添加  **ref**,相当于id,在此范围内的表单验证有效
      - 第五步：在操作保存按钮时，添加方法，对整个表单进行校验，参数为检验完的回调，会返回一个 Boolean 表示成功与失败。
  

```
   <Form :label-width="100" ref='contractForm' :model='contractForm' :rules="ruleValidate">
     <FormItem label='合同编号：' prop="contractNo">
         <Input placeholder="请输入合同编号" v-model='contractForm.contractNo'></Input>
     </FormItem>
     //data里面，写验证
     ruleValidate: {
       contractNo:[
             { required: true, message: '合同编号不能为空', trigger: 'blur' },
          ],
        }
       //methods里面，写方法
       addChange(name){
             this.$refs[name].validate(valid => {
                  if (valid) {
                  }
              });  
   </Form> 
```

 - iview进行表单验证select时候验证失败的问题：
      - 用iview自带的表单验证select标签的时候，一直验证不通过，**因为iview默认校验数据类型为String，而我的select用的value是number类型的**
  

```
ruleValidate: {
   customer:[
           { required: true, message: '客户名称不能为空', trigger: 'blur',type:'number'},
        ], 
      }  
```

 - iview进行表单验证时间日期验证失败的问题：
     -  和下拉框一样，日期的类型是data
 

```
  ruleValidate: {
   advance:[
           { required: true, message: '预送达时间不能为空', trigger: 'change' ,type: 'date'},
        ],
      }    
```

 - iview进行多重验证的写法：
    - 多重验证包括第一要验不能为空，第二要验证限制的一些长度，写正则表达式等
```
     ruleValidate: {
         goodsNum: [
                 { required: true, message: '数量不能为空', trigger: 'blur' },
                 { type: 'string',pattern:/^(([1-9]\d{0,3})|0)(\.\d{0,2})?$/, message:'数量应为正浮点数且不超过9999.99', trigger:'blur'},
                    ],
      }
```

 
