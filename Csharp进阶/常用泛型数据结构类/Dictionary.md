## Dictionary的本质
可以将`Dictionary`理解为 拥有泛型的`Hashtable`
它也是基于哈希代码组织起来的 **键/值对**
键值对类型从`Hashtable`的`object`变成可以自己指定的泛型

### 声明
 需要引用命名空间
 ```C#
 using System.Collections.Generic
 Dictionary<int,string> dictionary = new Dictionary<int,string>();
 ```

### 增删查改

#### 增
注意不能出现相同的键
```C#
dictionary.Add(1, "123");
dictionary.Add(2, "222");
dictionary.Add(3, "333");
dictionary.Add(4, "444");
```

#### 删
1.只能通过键去删除
删除不存在的键不会报错
```C#
dictionary.Remove(1);
dictionary.Remove(5);
```
2.清空
```C#
dictionary.Clear();
```


#### 查
1.通过键查看值
找不到会直接报错
```C#
Console.WriteLine(dictionary[2]);
Console.WriteLine(dictionary[5]);
Console.WriteLine(dictionary[1]);
```

2.查看是否存在
根据键检测
```C#
if (dictionary.ContainsKey(4))
{
    Console.WriteLine("存在");
}
```
根据值检测
```C#
if (dictionary.ContainsValue("123"))
{
    Console.WriteLine("存在");

}
```

#### 改
通过键修改
不存在的键不会报错会新建一个
```C#
Console.WriteLine(dictionary[4]);
dictionary[5] = "555";
Console.WriteLine(dictionary[5]);
```


### 遍历
获取长度
```C#
Console.WriteLine(dictionary.Count);
```
1.遍历所有键
```C#
foreach (int item in dictionary.Keys)
{
    //键
    Console.WriteLine(item);
    //值
    Console.WriteLine(dictionary[item]);
}
```
2.遍历所有值
```C#
Console.WriteLine("*****华丽分割线******");
foreach (string item in dictionary.Values)
{
    Console.WriteLine(item);
}
```
3.键值对 一起遍历
```C#
foreach (KeyValuePair<int,string> item in dictionary)
{
    Console.WriteLine("键:{0}  值:{1}",item.Key,item.Value);
}
```

---
## 练习

### 第一题
使用字典存储0~9的数字对应的大写文字(零 壹 贰 叁 肆 伍 陆 柒 捌 玖 拾)
提示用户输入不超过3位的数,提供一个方法 返回数的大写
如:306 返回参零陆
```C#
static string GetInfo(int num)
{
    Dictionary<int, string> dic = new Dictionary<int, string>();
    dic.Add(0, "零");
    dic.Add(1, "壹");
    dic.Add(2, "贰");
    dic.Add(3, "叁");
    dic.Add(4, "肆");
    dic.Add(5, "伍");
    dic.Add(6, "陆");
    dic.Add(7, "柒");
    dic.Add(8, "捌");
    dic.Add(9, "玖");

    string str = "";
    //得到百位数(如:123 里面的1)
    int b = num / 100;
    if (b != 0)
    {
        str += dic[b];
    }
    //得到十位数(如:123 里面的2)
    int s = num % 100 /10;
    if (s != 0 || str !=  "")
    {
        str += dic[s];
    }
    //得到个位数
    int g = num % 10;
    str += dic[g];

    return str;
}
```
[异常捕获](../../Csharp入门/异常捕获.md)
```c#
try
{
    Console.WriteLine("请输入不超过3位的数");
    Console.WriteLine(GetInfo(int.Parse(Console.ReadLine())));
}
catch 
{
    Console.WriteLine("请输入数字");
}
```

### 第二题
计算每个字母出现的次数"Welcome to Unity Worlo!"
使用字典存储 最后遍历整个字典 不区分大小写
```C#
Dictionary<char,int> dic = new Dictionary<char,int>();
string str = "Welcome to Unity Worlo!";
str = str.ToLower();//全部转换成小写(不区分大小写)
//string本质是char数组
for (int i = 0; i < str.Length; i++)
{
    if (dic.ContainsKey(str[i]))
    {
        //有这个键则直接+1
        dic[str[i]] += 1;
    }
    else
    {
        //没有则新建一个从1开始
        dic.Add(str[i], 1);
    }
}
//遍历
foreach (char item in dic.Keys)
{
    Console.WriteLine("字母:{0} 出现了{1}次", item, dic[item]);
}
```