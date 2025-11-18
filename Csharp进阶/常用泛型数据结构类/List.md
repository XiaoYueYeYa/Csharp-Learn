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

### 遍历 
获取长度
```C#
Console.WriteLine(list.Count);
```
获取容量
```C#
Console.WriteLine(list.Capacity);
```

```C#
for (int i = 0; i < list.Count; i++)
{
    Console.WriteLine(list[i]);
}

foreach (int item in list)
{
    Console.WriteLine(item);
}
```

## 练习
### 第一题

建立一个整形`List `为他添加10~1
删除`List`中的第五个元素
遍历剩余元素并打印
```C#
List<int> list = new List<int>();
for (int i = 10; i > 0; i--)
{
    list.Add(i);
}

list.RemoveAt(4);

foreach (int item in list)
{
    Console.Write(item);
}
```


### 第二题

一个Monster基类 Boss和Gablin都继承它
在怪物类的构造函数中 将其存储到怪物List中
遍历列表可以让Boss和Gablin对象产生不同攻击
Monster.monster
[抽象类和抽象方法](../../Csharp核心/面向对象_多态/抽象类和抽象方法.md)
```C#
abstract class Monster
{
    //在怪物类的构造函数中 将(新的自己Monster)其存储到(怪物)List中
    //静态函数存在唯一性 只会new一次
    public static List<Monster> monsters = new List<Monster>();
    public Monster()
    {
        monsters.Add(this);
    }

    //遍历列表可以让Boss和Gablin对象产生不同攻击
    abstract public void Atk();
}
class Boss : Monster
{
    public override void Atk()
    {
        Console.WriteLine("Boss的攻击");
    }
}
class Gablin : Monster
{
    public override void Atk()
    {
        Console.WriteLine("哥布林的攻击");
    }
}
```

```C#
Boss b1 = new Boss();
Boss b2 = new Boss();
Gablin g1 = new Gablin();
Gablin g2 = new Gablin();

for (int i = 0; i < Monster.monsters.Count; i++)
{
    Monster.monsters[i].Atk();
}
Console.WriteLine("-----华丽分割线-----");
foreach (Monster item in Monster.monsters)
{
    item.Atk();
}
```