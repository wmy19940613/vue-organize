## Vue的computed计算属性

+ computed计算属性：在模板中的表达式都是需要很简洁的，只是写结构，绑定字段，太多的逻辑会造成代码难以维护，所有较大的数据计算要写在computed计算属性里面。
+ 想要计算的数据，可以使用{{}}、或者v-model进行绑定。例如想要计算单价*数量的总金额

```
   <FormItem label='单价：' required prop='price'>
      <Input placeholder="自动带入单价" v-model='purchaseForm.price'></Input>
  </FormItem>
  <FormItem label='送气量：' prop='airSupply'>
         <Input placeholder="请输入送气量" v-model='purchaseForm.airSupply'></Input>
 </FormItem>
 <FormItem label='总金额：' prop='amount' required>
    <Input placeholder="单价*数量" v-model='amount' disabled></Input>
    <!-- {{amount}} -->
 </FormItem>

 ```
+ 在computed下

```
computed: {
  //总金额
  amount() {  //绑定的字段名    
             if(this.purchaseForm.airSupply===""||this.purchaseForm.airSupply===null||this.purchaseForm.airSupply===undefined||this.purchaseForm.price===""||this.purchaseForm.price===null||this.purchaseForm.price===undefined){
                  //这里只是条件判断  
                    return ""
                }else if(this.purchaseForm.airSupply===0||this.purchaseForm.price===0){
                    return 0
                }else{
                    return (this.purchaseForm.airSupply * 100 * this.purchaseForm.price * 100) / 10000
                }
            }
        },
```

+ 计算属性缓存 vs 方法 
在computed里面写的计算在methods方法里面写一个方法同样可以实现的。不同的是计算属性是基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 amount计算属性会立即返回之前的计算结果，而不必再次执行函数。
在methods里面每当触发重新渲染时，调用方法将总会再次执行函数
