# Attribute mapping

当需要自定义匹配名称或者其他属性时可以用到attribute mapping,比如

```c#
[ElasticsearchType(Name = "employee")]
public class Employee
{
    [Text(Name = "first_name", Norms = false, Similarity = "LMDirichlet")]
    public string FirstName { get; set; }

    [Text(Name = "last_name")]
    public string LastName { get; set; }

    [Number(DocValues = false, IgnoreMalformed = true, Coerce = true)]
    public int Salary { get; set; }

    [Date(Format = "MMddyyyy")]
    public DateTime Birthday { get; set; }

    [Boolean(NullValue = false, Store = true)]
    public bool IsManager { get; set; }

    [Nested]
    [PropertyName("empl")]
    public List<Employee> Employees { get; set; }

     [Text(Name = "office_hours")]
     public TimeSpan? OfficeHours { get; set; }

     [Object]
     public List<Skill> Skills { get; set; }
}

public class Skill
{
    [Text]
    public string Name { get; set; }

    [Number(NumberType.Byte, Name = "level")]
    public int Proficiency { get; set; }
}
```
通过为相应的属性添加特性，在elasticsearch中生成自定义的类型，比如

```json
{
  "mappings": {
    "employee": {
      "properties": {
        "birthday": {
          "format": "MMddyyyy",
          "type": "date"
        },
        "empl": {
          "properties": {},
          "type": "nested"
        },
        "first_name": {
          "type": "text",
          "norms": false,
          "similarity": "LMDirichlet"
        },
        "isManager": {
          "null_value": false,
          "store": true,
          "type": "boolean"
        },
        "last_name": {
          "type": "text"
        },
        "office_hours": {
          "type": "text"
        },
        "salary": {
          "coerce": true,
          "doc_values": false,
          "ignore_malformed": true,
          "type": "float"
        },
        "skills": {
          "properties": {
            "level": {
              "type": "byte"
            },
            "name": {
              "type": "text"
            }
          },
          "type": "object"
        }
      }
    }
  }
}
```

