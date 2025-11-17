### StringBuilder
[[String字符串]]

#### 基本概念

C#提供的一个用于处理字符串的公共类
==主要解决的问题是:==
**修改字符串而不创建新的对象** 需要频繁修改和拼接的字符串可以使用它 **可以提升性能**
使用前 **需要引用命名空间**

#### 初始化 直接指明内容

```c#
StringBuilder str = new StringBuilder("123123123");
//参数1:传入的内容
//参数2:单个房间的最大容量   不写 默认16
//StringBuilder str = new StringBuilder("123123123",100);
Console.WriteLine(str);//123123123
```

#### 容量

```c#
//StringBuilder 存在一个容量的问题 每次往里面增加时 会自动扩容 扩容*2(如默认16超出了 容量变成32 在超出了变64 依次*2... )
//获得容量
Console.WriteLine(str.Capacity);
//获得字符长度
Console.WriteLine(str.Length);
```

#### 增删改查替换

```c#
//增
str.Append("000");
Console.WriteLine(str);
Console.WriteLine(str.Length);
Console.WriteLine(str.Capacity);

str.AppendFormat("{0}{1}",100,100);
Console.WriteLine(str);
Console.WriteLine(str.Length);
Console.WriteLine(str.Capacity);

//插入
//参数1:插入的位置
//参数2:插入的内容
str.Insert(0, "Yue");
Console.WriteLine(str);

//删
//参数1:开始位置  参数2:删除的数量
str.Remove(0, 10);

//清空
str.Clear();

//查
str.Append("0100000");
Console.WriteLine(str[1]);
//改
str[0] = 'A';
Console.WriteLine(str);
//替换
str.Replace("1", "666");
Console.WriteLine(str);

//重新赋值 StringBuilder
//只能先清空 在拼接
str.Clear();
str.Append("123123");
Console.WriteLine(str);

//判断StringBuilder是否和某个字符串相等
if (str.Equals("123123"))
{
    Console.WriteLine("相等");
}
```

#### 描述string 和 stringBuilder的区别

1.`string`相对于`StringBuilder` 更容易产生垃圾 **每次修改拼接都会产生垃圾**
2.`string`相对`StringBuilder`更加灵活 因为**它提供了更多的方法**提供使用
**如何选择他们两个**
需要**频繁修改拼接的字符串**可以使用`StringBuilder`
**需要**使用`string`**独特的一些方法来处理一下特殊逻辑时**可以使用`string`

#### 如何优化内存

**内存优化** 从两个方面去解答
1.如何节约内存
2.如何尽量少的GC(垃圾回收)

**少new对象 少产生垃圾**
**合理使用static(静态)**
**合理使用string和StringBuilder**



---
