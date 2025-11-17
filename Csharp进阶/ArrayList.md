## 回顾
[索引器](../Csharp核心/面向对象_封装/索引器.md)

## ArrayList的本质
ArrayList是一个C#为我们封装好的类
它的本质是一个`object`类型的数组
`ArrayList`类帮助我们实现了很多方法
比如数组的增删改查

### 声明
需要引用命名空间`using System.Collections;`
```C#
ArrayList array = new ArrayList();
```

### 增删改查

#### 增
```
array.Add(1);
array.Add("114514");
array.Add(true);
array.Add(new object());
array.Add(new Test());
array.Add(1);
```