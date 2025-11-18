## List的本质
[泛型](../泛型/泛型.md) [一维数组](../../Csharp基础/数组/一维数组.md)
`List`是一个C#为我们封装好的类
它的本质是一个==**可变类型的泛型数组**==
List类帮助我们实现了很多方法
比如**泛型数组**的增删查改

### 声明
需要引用命名空间
```C#
using System.Collections.Generic
```

```C#
List<int> list = new List<int>();
List<string> list2 = new List<string>();
List<bool> list3 = new List<bool>();
```

### 增删查改

#### 增
一个一个加
```C#
list.Add(1);
list.Add(2);
list.Add(3);
list.Add(4);

list2.Add("字符串");
List<string> listStr = new List<string>();
listStr.Add("123");
listStr.Add("456");
```
批量添加
```C#
list2.AddRange(listStr);
list2.AddRange("listStr","123");
```

插入
```C#
list.Insert(0,999);
Console.WriteLine(list[0]);
```





