## 什么是lambad表达式
可以将**lambad表达式** 理解为**匿名函数的简写**
除了写法不同外
用上和**匿名函数一模一样**[匿名函数](匿名函数.md)
都是和委托或者事件 配合使用的

### lambad表达式语法
匿名函数
```C#
delegate(参数列表)
{
	//函数体
};
```
lambad表达式
```C#
(参数列表) =>
{
	//函数体
}
```

### 使用
//1.无参无返回
Action a = () =>
{
    Console.WriteLine("无参无返回值的lambad表达式");
};
//2.有参
Action<int> a2 = (int value) =>
{
    Console.WriteLine("有参数Lambad表达式{0}", value);
};
a2(123);

//3.甚至参数类型都可以省略 参数类型和委托或事件容器一致
Action<int> a3 = (value) =>
{
    Console.WriteLine("省略参数类型的写法{0}",value);
};
a3(123);

//4.有返回值
Func<string, int> a4 = (value) =>
{
    Console.WriteLine("有返回值有参数的表达式{0}", value);
    return 1;
};

Test test = new Test();
test.DoSomthing();

//其他传参使用等匿名函数一样
//缺点也是和匿名函数一样的