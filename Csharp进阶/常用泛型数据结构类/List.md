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

#### 删
1.移除指定元素
```C#
list.Remove(1);
list.Remove(2);
```
2.移除指定位置的元素
```C#
list.RemoveAt(2);
```
3清空
```C#
list.Clear();
```

#### 查
1.得到指定位置的元素
```C#
Console.WriteLine(list[1]);
Console.WriteLine(list2[1]);
```
2.查看元素是否存在
```C#
if (list.Contains(1))
{
    Console.WriteLine("存在");
}
```
3.正向查找元素位置
找到返回位置 找不到 返回-1
```C#
int index = list.IndexOf(1);
Console.WriteLine(index);
```
4.反向查找元素位置
找到返回位置 找不到 返回-1
```C#
index = list.LastIndexOf(1);
Console.WriteLine(index);
```

#### 改
简单粗暴
```C#
Console.WriteLine(list[0]);
list[0] = 999;
Console.WriteLine(list[0]);
```


