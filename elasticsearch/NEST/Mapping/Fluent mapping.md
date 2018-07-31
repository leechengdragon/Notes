# Fluent mapping

由于attribute mapping 不能完全自定义匹配，因此可以使用fluent mapping

假设有这样两个自定义类型

```c#
public class Company
{
    public string Name { get; set; }
    public List<Employee> Employees { get; set; }
}

public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Salary { get; set; }
    public DateTime Birthday { get; set; }
    public bool IsManager { get; set; }
    public List<Employee> Employees { get; set; }
    public TimeSpan Hours { get; set; }
}
```
通过fluent mapping来手动设置匹配属性

```c#
var createIndexResponse = client.CreateIndex("myindex", c => c
    .Mappings(ms => ms
        .Map<Company>(m => m
            .Properties(ps => ps
                .Text(s => s
                    .Name(n => n.Name)
                )
                .Object<Employee>(o => o
                    .Name(n => n.Employees)
                    .Properties(eps => eps
                        .Text(s => s
                            .Name(e => e.FirstName)
                        )
                        .Text(s => s
                            .Name(e => e.LastName)
                        )
                        .Number(n => n
                            .Name(e => e.Salary)
                            .Type(NumberType.Integer)
                        )
                    )
                )
            )
        )
    )
);
```
通过这样的方式可以精确地设置每一个匹配属性，但是这样出现一个问题，如果需要对类型中的每个属性进行设置，就会造成这个lambda表达式非常复杂，大部分时候我们都需要全部匹配类型中的属性，有没有一种方法既可以精确设置我们需要的属性，又可以自动匹配那些通常类型的属性？方法就是将automap()和fluent mapping 混合使用，例如
```c#
var createIndexResponse = client.CreateIndex("myindex", c => c
    .Mappings(ms => ms
        .Map<Company>(m => m
            .AutoMap()
            .Properties(ps => ps
                .Nested<Employee>(n => n
                    .Name(nn => nn.Employees)
                )
            )
        )
    )
);
```
这种方式精确设置自定义的属性，其他属性通过automap完成

上面这种写法与下面这种写法效果一样

```c#
var createIndexResponse = client.CreateIndex("myindex", c => c
    .Mappings(ms => ms
        .Map<Company>(m => m
            .Properties(ps => ps
                .Nested<Employee>(n => n
                    .Name(nn => nn.Employees)
                )
            )
            .AutoMap()
        )
    )
);
```
两者的区别在于automap的位置不同，因为automap方法是[幂等](https://github.com/leechengdragon/Notes/blob/master/幂等性.md)的，所以放在前和放在后效果是一样的

不同匹配模式的混用就会有一个优先级的问题，优先级高的操作会覆盖优先级低的操作，fluent mapping > attribute mapping > auto mapping