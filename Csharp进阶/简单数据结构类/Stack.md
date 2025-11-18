## Stack的本质
[值类型和引用类型](../../Csharp基础/值类型和引用类型.md)
`Stack`(栈)是一个C#为我们封装好的类
它的本质也是`object[]`数组 只是封装了特殊的存储规则
`Stack`是**栈**存储容器 栈是一种==先进后出==的数据结构
先存入的数据后获取 后存入的数据线获取
**栈是先进后出**

### 声明
需要引用命名空间 `System.Collections`
```C#
Stack stack = new Stack();
```

### 增取查改

#### 增
**压栈**
```C#
stack.Push(stack);
stack.Push(1);
stack.Push("stack");
stack.Push(true);
stack.Push(1.2f);
stack.Push(new Test());
```

#### 取
栈中**不存在删除**的概念
只有取的概念
弹栈(**先进后出**)
```C#
 object v = stack.Pop();
 Console.WriteLine(v);

 v = stack.Pop();
 Console.WriteLine(v);
```

#### 查
1.栈无法查看指定位置的 元素
 **只能查看栈顶端的内容**(最后放入的数据)
 ```C#
v = stack.Peek();
Console.WriteLine(v);
v = stack.Peek();
Console.WriteLine(v);
 ```
2.查看某个元素是否存在于栈中(无法查看指定位置的元素)
```C#
if (stack.Contains("stack"))
{
    Console.WriteLine("存在");
}
```

#### 改
栈**无法改变**其中的元素 只能压(存)和弹(取)
实在要改 **只有清空**
```C#
stack.Clear();//清空

stack.Push(v);//重新添加..
stack.Push("1");
stack.Push(2);
stack.Push("哈哈哈");
```

### 遍历
1.获取长度
```C#
Console.WriteLine(stack.Count);
```
2.用`foreach`遍历
而且遍历出来的顺序 也是**从栈顶到栈底**
```C#
foreach (var item in stack)
{
    Console.WriteLine(item);
}
```
3.还有一只遍历方式`for`
将栈转换为`object`数组
遍历出来的顺序 也是从栈顶到栈底
```C#
object[] array = stack.ToArray();
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
```
4.循环弹栈
```C#
while (stack.Count > 0)
{
    object o = stack.Pop();
    Console.WriteLine(o);
}
Console.WriteLine(stack.Count);
```

### 装箱拆箱
由于用[万物之父](../../Csharp核心/面向对象_继承/万物之父和装箱拆箱.md)来存储数据 自然存在装箱拆箱
当往里面进行值类型存储时就是在装箱
当将**值类型对象取出来转换使用时 就存在拆箱**

## Stack_练习
写一个方法计算任意一个数的二进制
使用栈结构方式存储 之后打印出来


