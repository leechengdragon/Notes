# Class与Style绑定

### 绑定Class

**对象语法**

```html
<!--如果isActive,isEnable，则添加active,enable class，反之不添加-->
<span v-bind:class="{active:isActive,enable:isEnable}"></span>
```

**数组语法**

```html
<!--将会应用实例中data中isActive和isEnable属性的值-->
<span v-bind:class="[isActive,isEnable]"></span>
```

### 绑定样式

```html
<span v-bind:style="styleObject">test2</span>
```

```javascript
data:{
    styleObject:{
                  fontSize:'20px',
                  color:'yellow'
                }
}

```
