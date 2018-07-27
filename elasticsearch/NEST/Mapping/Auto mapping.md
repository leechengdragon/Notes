# Auto mapping

#### 类型自动匹配
Nest客户端可以自动将c#中的类型匹配至elasticsearch,比如

|c# type|elasticsearch type|
|:-----:|:----------------:|
|datetime|date|
|timespan|long|
|bool|boolean|
|int|integer|
|自定义类型|object|

<i>注意：c# 中也有elasticsearch 没有的类型，比如decimal，在elasticsearch 中只能通过double类型与之对应，但是使用double类型会导致精度的损失，需要看情况使用</i>

#### 自定义对象的嵌套

c#中定义的类型可以嵌套，比如
```c#
public class A
{
    public A Person{get;set;}
}
```
这种情况在elasticsearch中匹配的时候首先会被匹配成为对象类型object，默认情况下只会匹配一级，就像
```json
{
    "person":{
        "person":{
            "type":"object"
        }
    }
}
```
这样做的好处在于防止无限递归带来的堆栈溢出，这是默认情况下，也可以通过修改nest中automap的参数来自定义匹配层数