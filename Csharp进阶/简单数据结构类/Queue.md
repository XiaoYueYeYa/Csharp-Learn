## Queue本质 
`Queue`是一个C#为我们封装好的类
它的本质也是`Object[]`数组 只是封装了特殊的存储规则

`Queue`是**队列存储容器**
队列是一种**先进先出**的**数据结构**
先存入的数据先获取 后存入的数据后获取
==**先进先出**==

### 声明
需要引用命名空间`System.Collections;`
```C#
Queue queue = new Queue();
```

### 增取查改

#### 增
```C#
queue.Enqueue(new Test());
queue.Enqueue("123");
queue.Enqueue(1234);
queue.Enqueue(1.4f);
```

#### 取
队列中**不存在删除**的概念
只有取的概念 ==取出先加入的对象==
```C#
object v = queue.Dequeue();
Console.WriteLine(v);
v = queue.Dequeue();
Console.WriteLine(v);
```

#### 查
1.查看队列头部(第一个)元素但不会移除
```C#
v= queue.Peek();
Console.WriteLine(v);
v= queue.Peek();
Console.WriteLine(v);
```
2.查看某元素是否存在队列中
```C#
if (queue.Contains(1.4f))
{
    Console.WriteLine("存在");
}
```


#### 改
队列**无法改变其中元素** 只能进出队列
实在要改 **只有清除**
```C#
queue.Clear();
queue.Enqueue(1);
queue.Enqueue(3);
queue.Enqueue(2);
```

### 遍历
1.获取长度
```C#
Console.WriteLine(queue.Count);
```
2.用`foreach`遍历
```C#
foreach (var item in queue)
{
     Console.WriteLine(item);
}
```
3.还有一种遍历方式
将队列转换成`object[]`数组
```C#
object[] array = queue.ToArray();
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
```
4.while循环出列
```C#
while (queue.Count > 0)
{
    object o = queue.Dequeue();
    Console.WriteLine(o);
}
```

### 装箱拆箱
由于用[万物之父](../../Csharp核心/面向对象_继承/万物之父和装箱拆箱.md)来存储数据 自然存在装箱拆箱
当往里面进行值类型存储时就是在装箱
当将值类型对象取出来转换使用时 就存在拆箱

## Queue_练习
使用队列存储信息 一次性存10条信息
每隔一段时间打印一条信息控制台打印信息要有明显停顿感
```C#
static void Main(string[] args)
{
    Console.WriteLine("lesson03_Queue_练习");
    Queue queue = new Queue();

    for (int i = 1; i <= 10; i++)
    {
        queue.Enqueue("第"+i+"条" );
    }
    int num = 0;
    while (queue.Count > 0)
    {
        num++;
        if (num == 100000000)//可使用预处理器指令优化
        {
            num = 0;
            object o = queue.Dequeue();
            Console.WriteLine(o);
        }
    }
}
```
