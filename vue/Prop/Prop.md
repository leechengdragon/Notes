# Prop

### Prop大小写

```html
    <div id="example1">
        <component-a post-title='123'></component-a>
    </div>
```

```javascript
let componentA={
        props:['postTitle'],
        template:`<h3>{{postTitle}}</h3>`
    }
    let example1=new Vue({
        el:'#example1',
        components:{
            'component-a':componentA
        }
    })
```

* html大小写不敏感，最后都会转化为小写，如果组件的属性名称采用驼峰法命名，在使用的时候需要使用连字符号

### Prop类型

定义prop的方式

1. 字符串数组

```javascript
props:['id','name','grade']
```

2. 对象形式(可以定义出每种属性的数据类型)

```javascript
props:{
    id:Number,
    name:String,
    grade:Number
}
```

### Prop值传递

```html
<!--传递静态值-->
<blog-post title="this is a title"></blog-post>
<!--传递动态值-->
<blog-post v-bind:title="post.title"></blog-post>
<!--可以传递所有数据类型-->
```

### 单项数据流

* 数据流只能从上到下，父组件数据更新时，子组件会同步更新，但是子组件更新时，父组件不会被修改

### Prop验证

```javascript
props:{
    //数据可能有多个类型
    propA:[String,Number]
    //必填
    propB:{
        Number,
        require:true
    }，
    //带有默认值
    propC:{
        Number,
        default:100
    }
    ...
}
```

