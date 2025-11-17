## 回顾
[索引器](../Csharp核心/面向对象_封装/索引器.md)

## ArrayList的本质
ArrayList是一个C#为我们==**封装好的类**==
它的本质是一个`object`类型的数组
`ArrayList`类帮助我们实现了很多方法
比如数组的**增删改查**

### 声明
需要引用命名空间`using System.Collections;`
```C#
ArrayList array = new ArrayList();
```

### 增删改查

#### 增
```C#
array.Add(1);
array.Add("114514");
array.Add(true);
array.Add(new object());
array.Add(new Test());
array.Add(1);
```

范围增加(批量增加 把另一个list容器里面的内容加到后面
```C#
ArrayList array2 = new ArrayList();
array2.Add(123);
array.AddRange(array2);
```

插入
```C#
//参数一:位置
//参数二:内容 
array.Insert(0,"12345");
Console.WriteLine(array[0]);
```

#### 删

```C#
//移除指定元素 从头开始找 找到就删除
array.Remove(1);
//移除指定位置的元素
array.RemoveAt(0);
//清空
//array.Clear();
```


#### 查

```C#
//得到指定位置的元素
Console.WriteLine(array[0]);

//查找元素是否存在
if (array.Contains(1))
{
    Console.WriteLine("存在1");
}

//正向查找元素位置
//找到的返回值 是位置 找不到返回 -1
int index = array.IndexOf(1);
Console.WriteLine(index);
Console.WriteLine(array.IndexOf(false));

//反向查找元素位置
//返回从头开始的索引值
index = array.LastIndexOf(true);
Console.WriteLine(index);
```



