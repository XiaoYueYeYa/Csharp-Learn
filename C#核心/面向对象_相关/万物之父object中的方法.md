### 万物之父中的方法

#### 总结

1.虚方法 `toString` **自定字符串转换规则**
2.成员方法 `GetTyper` 反射相关
3.成员方法 `MemberwiseClone` **浅拷贝**
4.虚方法 `Equals` **自定义判断相同的规则**

#### object中的静态方法

**静态方法** `Equals` 判断两个对象是否相等
最终的判决权 交给左侧对象的`Equals`方法
不管**值类型还是引用类型都会按照左侧对象**`Equals`方法**规则来进行比较**

```c#
    class Test
    {
        public int i = 1;
        public Test2 t2 = new Test2();

        public Test Clone()
        {
            return MemberwiseClone() as Test;
        }

        public override string ToString()
        {
            return "自定义ToString()";
        }
    }
    class Test2
    {
        public int i = 2;
    }
```

```c#
//值类型
Console.WriteLine(Object.Equals(1, 1));
//引用类型
Test test = new Test();
Test test1 = new Test();
//Object.Equals可以直接省略Object
Console.WriteLine(Equals(test, test1));
```

静态方法`ReferenceEquals`
比较两个对象是否是相同的引用 **主要是用来比较引用类型的对象**
值类型对象返回值始终是`false`

```c#
test1 = test;
Console.WriteLine(Object.ReferenceEquals(test,test1));
```

#### object中的成员方法

普通方法`GetType()`
该方法在反射相关知识点是非常重要的方法 之后会具体的讲解这里返回的`Type`类型
该方法的主要作用就是获取对象运行时的类型`Type`
通过`Type`结合反射相关知识点可以做很多相关对象的操作

```c#
Test t = new Test();
Type type = t.GetType();
```

普通方法`MemberwiseClone()`
该方法用**于获取对象的浅拷贝** 意思就是会**返回一个新的对象**
但是**新对象中的引用变量会和老对象中一致**

```c#
public Test Clone()
{
    return MemberwiseClone() as Test;
}
```

```c#
Test t2 = t.Clone();
Console.WriteLine("克隆对象后");
Console.WriteLine("t.i = "+t.i);
Console.WriteLine("t.t2.i = "+t.t2.i);
Console.WriteLine("t2.i = "+t2.i);
Console.WriteLine("t2.t2.i = "+t2.t2.i);

t2.i = 20;
t2.t2.i = 21;
Console.WriteLine("改变克隆体信息后");
Console.WriteLine("t.i = " + t.i);
Console.WriteLine("t.t2.i = " + t.t2.i);
Console.WriteLine("t2.i = " + t2.i);
Console.WriteLine("t2.t2.i = " + t2.t2.i);
```

#### object中的虚方法

虚方法`Equals`
默认实现还是比较两者是否同一个引用,相当于`ReferenceEquals`
但是微软在所有值类型的基类`System.ValueType`中重写了该方法 **用来比较值相等**
我们也**可以重写该方法 定义自己的比较相等的规则**

虚方法`GetHashCode`
该方法是**获取对象的哈希码**
(一直通过算法算出的 表示对象的唯一编码 不同对象的哈希码有可能一样 具体值根据哈希算法决定)
我们**可以通过重写该函数来自定义对象的哈希算法** 正常情况下 我们使用的极少 基本不用

虚方法`ToString`
该方法**用于返回当前对象代表的字符串** 我们**可以重写它定义我们自己的对象转字符串规则**
该方法非常常用 当我们调用打印方法时 默认就是使用对象的`ToString`方法后打印出来的内容

```c#
public override string ToString()
{
    return "自定义ToString()";
}
```

```c#
Test t = new Test();
Console.WriteLine(t);//自定义ToString()
```



---
