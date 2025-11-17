### Vob

#### 总结:

==多态:==让**同一类型的对象** **执行相同行为时有不同的表现**
==解决的问题:==让**同一个对象有唯一的行为特征**
`virtual` **虚函数**
`override` **重写**
`base` **父类**
v和o一定是结合使用的 来实现多态
b是否使用根据实际需求 保留父类行为

#### 多态的概念
[[../面向对象]]
多态按字面的意思就是"**多种状态**"
让**继承同一父类的子类们** 在**执行相同方法时有不同的表现**(状态)
==主要目的==
同一父类的对象 **执行相同行为(方法)有不同的表现**
==解决的问题==
**同一个对象有唯一的行为特征**

#### 解决的问题

```c#
class Father
{
    public void Speak()
    {
        Console.WriteLine("父类的方法");
    }
}
class Son:Father
{
    public void Speak()
    {
        Console.WriteLine("子类的方法");
    }
}
```

```c#
Father f = new Son();
f.Speak();//父类的方法

(f as Son).Speak();//子类的方法
```

#### 多态的实现

我们目前已学过的多态了
编译时多态-**函数重载** 开始就写好的

==我们将学习的:==
运行时多态(vob 抽象函数 接口)
**vob**
v:`virtual`(<span id="虚函数">**虚函数**</span>)
o:`override`(**重写**)
b:`base`(**父类**)

```c#
class GameObject
{
    public string name;
    public GameObject(string name)
    {
        this.name = name;
    }
    //virtual虚函数 可以被之类重写
    public virtual void Atk() 
    {
        Console.WriteLine("游戏对象进行攻击");
    }
}

class Player : GameObject
{
    public Player(string name) : base(name)
    {

    }
    //override重写虚函数
    public override void Atk()
    {
        //base的作用:
        //代表父类 可以通过base来保留父类的行为
        base.Atk();//执行父类的方法
        Console.WriteLine("玩家对象进行攻击");
    }
}
class Monster : GameObject
{
    public Monster(string name):base(name)
    {

    }
    public override void Atk()
    {
        Console.WriteLine("怪物对象进行攻击");
    }
}
```

```c#
GameObject p = new Player("Yue");
p.Atk();//玩家对象进行攻击
(p as Player).Atk();//玩家对象进行攻击

GameObject m = new Monster("怪物");
m.Atk();//怪物对象进行攻击
(m as Monster).Atk();//怪物对象进行攻击
```



---
