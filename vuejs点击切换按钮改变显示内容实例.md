## Vue.js点击切换按钮改变内容实例

+ 代码实例： 
  - 代码描述：点击切换按钮，来改变显示的内容，切换不同的单位。flag相当于一个开关，控制开关的改变，来切换不同的单位。同样适用于其他的切换内容实例，也可设置按钮点击显示隐藏等。
```
<!DOCTYPE html>  
<html>  
<head>  
    <meta charset="utf-8">  
    <title>vue点击切换改变内容</title>  
    <script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>  
</head>  
<body>  
    <Col span="2" style="text-align: center;">
       <p style='margin-top:8px;font-size:12px;' v-text="btnText" v-show='flag==true'></p>
       <p style='margin-top:8px;font-size:12px;' v-text="btnText" v-show='flag==false'></p>
    </Col>
    <Col span='2'>
       <span @click='switchChange'>
       <Icon type="arrow-swap" class='contractadd_icon'></Icon>      
       </span>
    </Col>
    <script type="text/javascript">  
    new Vue({  
        el:"#example",  
        data:{  
           flag:true,//单位切换开关
           btnText:'元/吨',
        },  
        methods:{  
            showToggle:function(){  
                this.flag = !this.flag  
                if(this.flag==true){  
                    this.btnText = "元/吨"  
                }else if(this.flag==false){  
                    this.btnText = "元/方"  
                } 
            }  
        }  
    })  
    </script>  
</body>  
</html>  
```
