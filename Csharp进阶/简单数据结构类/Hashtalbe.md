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
