### string

#### 字符串指定位置获取

**字符串本质是char数组**

**转为char数组**
`ToCharArray();`

```c#
string str = "Jie";
Console.WriteLine(str[0]);//J
//转为char数组
char[] chars = str.ToCharArray();
Console.WriteLine(chars[1]);

for (int i = 0; i < str.Length; i++)
{
    Console.WriteLine(str[i]);
}
```

#### 字符串拼接

```c#
str = string.Format("{0}{1}", 1, 111);
Console.WriteLine(str);//1111
```

#### 正向查找字符位置

```c#
str = "我叫吊炸天";
int index = str.IndexOf("叫");//返回数组下标
Console.WriteLine(index);//1
//如果查找不到则返回-1
index = str.IndexOf('你');
Console.WriteLine(index);//-1
```

#### 反向查找指定字符串位置

```c#
str = "我是吊炸天吊炸天";
index = str.LastIndexOf("吊炸天");
Console.WriteLine(index);//5

index = str.LastIndexOf("屌炸天");
Console.WriteLine(index);//-1
```

#### 移除指定位置后的字符

```c#
str = "我是吊炸天吊炸天";
str.Remove(4);
Console.WriteLine(str);//我是吊炸天吊炸天
//需要赋值后才会改变 返回的是单独的一个字符串
str = str.Remove(4);
Console.WriteLine(str);//我是吊炸天

//执行两个参数进行移除
//参数1 开始位置
//参数2 移除的字符个数
str = "我是吊炸天吊炸天";
str = str.Remove(1, 1);
Console.WriteLine(str);//我吊炸天吊炸天
```

#### 替换指定字符串

```c#
str = "我是吊炸天吊炸天";
str.Replace("吊炸天", "废人弱");
Console.WriteLine(str);//我是吊炸天吊炸天
//重新赋值才会生效
str = str.Replace("吊炸天", "废人弱");
Console.WriteLine(str);//我是废人弱废人弱
```

#### 大小写转换

```c#
str = "asdasdasdasd";
//大写
str.ToUpper();
Console.WriteLine(str);//asdasdasdasd
str = str.ToUpper();
Console.WriteLine(str);//ASDASDASDASD
//小写
str = str.ToLower();
Console.WriteLine(str);//asdasdasdasd
```

#### 字符串截取

```c#
str = "我是吊炸天吊炸天";
Console.WriteLine(str);//我是吊炸天吊炸天
//截取从指定位置开始之后的字符串
str = str.Substring(2);
Console.WriteLine(str);//吊炸天吊炸天

//参数1 开始位置
//参数2 指定截取个数
//不会自动的帮助你判断是否越界 需要自己去判断
str = str.Substring(2, 2);//天吊
Console.WriteLine(str);
```

#### 字符串切割

```c#
str = "1_1,2_2,3_3,4_1,5_2";
string[] strs = str.Split(',');//使用,切割返回数组
for (int i = 0; i < strs.Length; i++)
{
    Console.WriteLine(strs[i]);//(依次打印)1_1    2_2		3_3		4_1		5_2
}
```



---
