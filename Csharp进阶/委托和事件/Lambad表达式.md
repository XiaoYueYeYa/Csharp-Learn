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
1.无参无返回
```C#
Action a = () =>
{
    Console.WriteLine("无参无返回值的lambad表达式");
};
```
2.有参
```C#
Action<int> a2 = (int value) =>
{
    Console.WriteLine("有参数Lambad表达式{0}", value);
};
a2(123);
```
3.甚至参数类型都可以省略 参数类型和委托或事件容器一致
```C#
Action<int> a3 = (value) =>
{
    Console.WriteLine("省略参数类型的写法{0}",value);
};
a3(123);
```
4.有返回值
```C#
Func<string, int> a4 = (value) =>
{
    Console.WriteLine("有返回值有参数的表达式{0}", value);
    return 1;
};

Test test = new Test();
test.DoSomthing();
```

其他传参使用等匿名函数一样
**缺点也是和匿名函数一样的**

### 闭包
内层的函数可以引用包含在它外层的函数变量
即使外层函数的执行已经终止
注意:
该变量提供的值并非变量创建时的值 而且在父函数范围内的最终值

```C#
class Test
{
    public event Action action;

    public Test()
    {
        int value = 20;
        //这里就形成了闭包
        //因为 当构造函数执行完毕时 其中声明的临时变量value的声明周期就改变了
        action = () =>
        {
            Console.WriteLine(value);
        };
        //该变量提供的值并非变量创建时的值 而且在父函数范围内的 最终值
        for (int i = 0; i <= 10; i++)
        {
            //此index 非彼index
            int index = i;
            action += () =>
            {
                //直接输出i只会输出i的最终值 10
                //想输出1~9需要把i装到同一代码块index里面
                Console.WriteLine(index);
            };
        }
    }

    public void DoSomthing()
    {
        action();
    }
}
```

## 总结
匿名函数的特殊写法 就是lambad表达式
固定写法 就是`(参数列表)=>{}`
参数列表 可以直接省略参数类型
主要在 委托传递和存储时 **为了方便**可以直接使用匿名函数或者lambad表达式

缺点:**无法指定移除**

---

## 练习
有一个函数 会返回一个委托函数 这个委托函数中只有一句打印代码
之后执行返回的委托函数时 可以打印出1~10
```C#
class Test
{
    public Action Action()
    {

        return () =>
        {
            for (int i = 0; i <= 10; i++)
            {
                Console.WriteLine(i);
            }
        };
    }

   
    public Action Abd()
    {
        Action abd = null;
        for (int i = 0; i <= 10; i++)
        {
            int index = i;
            abd += () =>
            {
                Console.WriteLine(index);
            };
        }
        return abd;
        
    }
}
```

```C#
//有一个函数 会返回一个委托函数 这个委托函数中只有一句打印代码
//之后执行返回的委托函数时 可以打印出1~10
Test test = new Test();
Action action = test.Action();
action();
Console.WriteLine("-----------------");
Action action2 = test.Abd();
action2();
Console.WriteLine("-------简写-------");
test.Abd()();
```



