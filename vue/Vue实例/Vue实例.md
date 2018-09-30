# Vue实例

### 通过new关键字创建Vue实例

```javascript
let vm=new Vue({
    //选项
})
```

### 当创建好一个vue对象后，可以向其中的data对象添加属性，对属性的修改和对viewmodel的修改都将会影响数据（双向绑定）

```javascript
let data={num:1}
let vm=new Vue({
    data:data
})

data.num==vm.data //true

data.num=2
vm.num==2//true

vm.num=3
data.num==3//true
```
> <em> 注意：只有当实例创建时，data对象中存在的属性才会有双向绑定的效果，例如：在实例化vue对象之后，使用vm.name='123'赋值,这个name属性不会是响应的</em>

### 可以通过Object.freeze()方法冻结属性，这样属性将不会更新

```javascript
let obj={num:1}
Object.freeze(obj);
let vm=new Vue({
    data:obj
})
//后面对vm或者obj的修改将不会响应到页面上
```

### vue对象的其它属性和方法

```javascript
let obj={name:'test'}

let vm=new Vue({
    el:'#human',
    data:obj
})

//获取实例的data对象
vm.$data==obj//true

//获取对象的绑定的页面元素
vm.$el==document.getElementById('human')//true

//监听数据是否发生变化
vm.$watch('name',fuction(newValue,oldValue){
    //这里的代码将在name属性发生改变时执行
})
```