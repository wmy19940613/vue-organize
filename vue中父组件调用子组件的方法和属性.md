## vue中父组件调用子组件的方法和属性
+ 应用场景：子组件中的方法要在父组件里面使用，例如tabs栏切换，每一个tab页面都封装成一个组件，在每个组件里面都有初始化列表这个方法，所有在tabs页面要调用这个方法
+ 凡是要调用子组件的方法和属性都可以参考下面的实例
+ 利用ref属性可以获取到dom元素或者是子组件，从而可以调用子组件的方法（注意2.0版本用ref取代了el
1. 当ref直接定义在dom元素上时，则通过this.$refs.name可以获取到dom对dom进行原生的操作
```
<div class="foods-wrapper" ref="foods-wrapper">
```
  通过this.$refs获取到dom进行操作（注意ref属性的命名不能用驼峰，同时获取的时候也是）
```
 let menuList=this.$refs['menu-wrapper'].getElementsByClassName('menu-list-hook');//此处如果用this.$refs["menuWrapper"]将获取不到元素
```
2. (最常用)通过在引用的子组件上使用ref属性实现父组件调用子组件的方法以及属性（父组件引用子组件，不要忘记注册和import引入）
   在父组件中引用子组件并定义ref
```
<v-food  ref="selectfood"></v-food>(v-food是子组件的名)
```
   调用定义在子组件中的方法show（比如show()方法）
```
this.$refs.selectfood.show();//同时也可以调用子组件中的属性
```
+ ref介绍
 - 用来绑定某个dom元素，或者用来绑定某个组件，然后在$refs里面调用
 - 作用：可减少dom节点的消耗,可以打印下console.log(this.$refs)，用来给元素或组件注册引用信息，引用信息将会注册在父组件的$refs上面，如果是在普通元素上面使用，引用指向的就是普通元素，如果用在子组件上面，引用就指向组件实例。
 - ref：string
 - $refs: object可.方法或属性，它拥有所有的ref的所有子组件
