## Hashtalbe的本质
`Hashtable`(又称**散列表**)是==基于键的哈希值代码==组织起来的 ==**键/值对**==
它的主要哦作用是**提高数据查询的效率**
使用键来访问集合中的元素

### 声明
需要引用命名空间`System.Collections;`
```C#
Hashtable hashtable = new Hashtable();
```

### 增删改查

#### 增
==**注意:**==**不能出现相同的键**
```C#
hashtable.Add("键", "值");
hashtable.Add(1,"123");
hashtable.Add(true,false);
hashtable.Add(false,true);
```


#### 删
1.只能通过键去删除
```C#
hashtable.Remove(1);
```
2.删除不存在的键 没反应
```C#
hashtable.Remove(2);
```
3.或者直接清空
```C#
hashtable.Clear();
```

#### 查
1.通过键查看值
找不到返回空
```C#
Console.WriteLine(hashtable["键"]);
Console.WriteLine(hashtable[0]);//null
Console.WriteLine(hashtable[1]);
```
2.查看是否存在
根据键检测
```C#
if (hashtable.Contains(2))
{
    Console.WriteLine("存在键为2的值");
}
if (hashtable.ContainsKey(2))
{
    Console.WriteLine("存在键为2的值");
}
```
3.根据值检测
```C#
if (hashtable.ContainsValue("1"))
{
    Console.WriteLine("存在值为1的键值对");
}
```

#### 改
**只能改 键对应的值内容** 无法修改键
```C#
Console.WriteLine(hashtable[1]);
hashtable[1] = 100.4f;
Console.WriteLine(hashtable[1]);
```

### 遍历
得到键值对 对数(数量)
```C#
Console.WriteLine(hashtable.Count);
```
1.遍历所有键
```C#
foreach (object key in hashtable.Keys)
{
    Console.WriteLine("键:" + key);
    Console.WriteLine("值:"+hashtable[key]);
}
```

2.遍历所有值
```C#
foreach (object item in hashtable.Values)
{
    Console.WriteLine("值:" + item);
}
```

3.键值对一起遍历
```C#
foreach (DictionaryEntry item in hashtable)
{
    Console.WriteLine("键:" + item.Key + "值:" + item.Value);
}
```

4.迭代器遍历法
```C#
IDictionaryEnumerator myEnumerator = hashtable.GetEnumerator();
bool flag = myEnumerator.MoveNext();
while (flag)
{
    Console.WriteLine("键:" + myEnumerator.Key + "值:" + myEnumerator.Value);
    flag = myEnumerator.MoveNext();
}
```

### 装箱拆箱
由于用[万物之父](../../Csharp核心/面向对象_继承/万物之父和装箱拆箱.md)来存储数据 自然存在装箱拆箱
当往里面进行值类型存储时就是在装箱
当将值类型对象取出来转换使用时 就存在拆箱

## 练习
制作一个怪物管理器 提供创建怪物 移除怪物的方法
每个怪物都有自己的唯一ID
```C#
class MonsterMgr
{
    private static MonsterMgr instance = new MonsterMgr();
    private Hashtable monstersTable = new Hashtable();
    private MonsterMgr() 
    {
    
    }
    public static MonsterMgr Instance
    {
        get
        {
            return instance;
        }
    }

    private int monsterID = 0;
    public void AddMonster()
    {
        Monster monster = new Monster(monsterID);
        Console.WriteLine("创建了id为:{0}的怪物",monsterID);
        ++monsterID;
        //Hashtable 的键是不能重复的 所以一定是用唯一ID
        monstersTable.Add(monster.id, monster);
    }

    public void RemoveMonster(int key)
    {
        if (monstersTable.ContainsKey(key))
        {
            (monstersTable[key] as Monster).Dead();
            monstersTable.Remove(key);
        }
    }
}
```

```C#
class Monster
{
    public int id;
    public Monster(int id)
    {
        this.id = id;
    }
    public void Dead()
    {
        Console.WriteLine("怪物{0}死亡",id);
    }
}
```

```C#
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();
MonsterMgr.Instance.AddMonster();

MonsterMgr.Instance.RemoveMonster(0);
MonsterMgr.Instance.RemoveMonster(5);
```