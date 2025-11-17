## 回顾
[索引器](../Csharp核心/面向对象_封装/索引器.md)

## ArrayList的本质
ArrayList是一个C#为我们==**封装好的类**==
它的本质是一个`object`类型的数组
`ArrayList`类帮助我们实现了很多方法
比如数组的**增删改查**

### 声明
需要引用命名空间`using System.Collections;`
```C#
ArrayList array = new ArrayList();
```

### 增删改查

#### 增
```C#
array.Add(1);
array.Add("114514");
array.Add(true);
array.Add(new object());
array.Add(new Test());
array.Add(1);
```

范围增加(批量增加 把另一个list容器里面的内容加到后面
```C#
ArrayList array2 = new ArrayList();
array2.Add(123);
array.AddRange(array2);
```

插入
```C#
//参数一:位置
//参数二:内容 
array.Insert(0,"12345");
Console.WriteLine(array[0]);
```

#### 删

```C#
//移除指定元素 从头开始找 找到就删除
array.Remove(1);
//移除指定位置的元素
array.RemoveAt(0);
//清空
//array.Clear();
```


#### 查

```C#
//得到指定位置的元素
Console.WriteLine(array[0]);

//查找元素是否存在
if (array.Contains(1))
{
    Console.WriteLine("存在1");
}

//正向查找元素位置
//找到的返回值 是位置 找不到返回 -1
int index = array.IndexOf(1);
Console.WriteLine(index);
Console.WriteLine(array.IndexOf(false));

//反向查找元素位置
//返回从头开始的索引值
index = array.LastIndexOf(true);
Console.WriteLine(index);
```

#### 改
```C#
Console.WriteLine(array[0]);
array[0] = "改";
Console.WriteLine(array[0]);
```

### 遍历
长度:`array.Count`
容量:`array.Capacity`
避免产生过多的垃圾

```C#
for (int i = 0; i < array.Count; i++)
{
    Console.WriteLine(array[i]);
}
Console.WriteLine("-----迭代器华丽分割线-----");

//迭代器遍历
foreach (object item in array)
{
    Console.WriteLine(item);
}
```

### 装箱拆箱
[万物之父object中的方法](../Csharp核心/面向对象_相关/万物之父object中的方法.md)
`ArrayList`本质上是一个可以**自动扩容**的`object`数组
由于用万物之父来进行存储数据 自然存在装箱拆箱
当往其中进行值类型存储时就是在装箱 当将值类型对象取出来转换使用时 就存在拆箱
所以==ArrayList尽量少用== 之后会学习更好的数据容器

```C#
int a = 1;
array[0] = a;//装箱
a = (int)array[0];//拆箱
```



## 练习题

创建一个背包管理类 使用ArrayList存储物品
实现购买物品 卖出物品 显示物品的功能
购买与卖出物品会导致金钱变化

```C#
class BagMgr
{
    public int money;
    //背包的物品
    public ArrayList item;

    public BagMgr(int money)
    {
        this.money = money;
        item = new ArrayList();
    }

    //购买
    public void BuyItem(Item item)
    {
        //判断物品的数量 价格不是负数
        if(item.num <= 0 || item.price < 0)
        {
            Console.WriteLine("请输入正确的物品信息");
            return;
        }
        //计算价格
        if (this.money <item.price*item.num)
        {
            Console.WriteLine("当前余额不足:{0}",this.money);
            return;
        }
        //结算
        this.money -= item.price * item.num;
        Console.WriteLine("购买{0}{1}个花费{2}钱,当前剩余{3}元",item.name,item.num, item.price * item.num,this.money);

        //如果需要实现物品叠加 可以在前面先判断 是否有这个物品 然后加数量
        for (int i = 0; i < this.item.Count; i++)
        {
            if ((this.item[i] as Item).id == item.id)
            {
                //叠加数量
                (this.item[i] as Item).num += item.num;
                return;
            }
        }
        //把一组物品添加到list中
        this.item.Add(item);

    }
    //卖出
    public void SellItem(Item item)
    {
        for (int i = 0; i < this.item.Count; i++)
        {
            //如何判断 买的东西有没有
            //这是在判断 两个引用地址 指向的是不是同一个房间
            //所以我们要判断 买的物品 一般不这样判断
            //if (this.item[i] == item)
            //{

            //}
            //通过ID判断
            if ((this.item[i] as Item).id == item.id)
            {
                //分两种情况
                int num = 0;
                string name = (this.item[i] as Item).name;
                int price = (this.item[i] as Item).price;
                //1.比我身上少
                if ((this.item[i] as Item).num > item.num)
                {
                    num = item.num;
                    (this.item[i] as Item).num -= num;
                    Console.WriteLine("{0}剩余{1}个", name, (this.item[i] as Item).num);
                }
                else
                {
                    //2.购买比我身上多的数量
                    num = (this.item[i] as Item).num;
                    //买完了 就从身上移除
                    this.item.RemoveAt(i);
                    Console.WriteLine("{0}剩余0个",name);
                }

                int sellMoney = (int)(num * price * 0.8f);
                this.money += sellMoney;

                Console.WriteLine("卖了{0}{1}个,赚了{2}元钱",name,num,sellMoney);
                Console.WriteLine("剩余{0}元",this.money);
                return;

            }

        }

    } 
    public void SellItem(int id,int num =1)
    {
        //直接调用上面写好的方法
        //直接构造一个Item类 把ID和数量两个关键信息设置好即可
        Item item = new Item();
        item.id = id;
        item.num = num;
        SellItem(item);
    }
    //显示
    public void ShowItem()
    {
        Item item;
        for (int i = 0; i < this.item.Count; i++)
        {
            item = this.item[i] as Item;
            Console.WriteLine("有{0}{1}个",item.name,item.num);
        }
        Console.WriteLine("当前拥有{0}元钱", this.money);
    }
}
```

```C#
//背包物品类
class Item
{
    //物品唯一ID 来区分物品的种类
    public int id;
    //物品名字
    public string name;
    //价格
    public int price;
    //数量
    public int num;
    public Item()
    {

    }
    public Item(int id, string name, int price, int num)
    {
        this.id = id;
        this.name = name;
        this.price = price;
        this.num = num;
    }
}
```


```C#
 BagMgr bag = new BagMgr(99999);
 Item i = new Item(1,"药品",10,10);
 Item i2 = new Item(2,"大保健",52,1);
 Item i3 = new Item(3,"大宝剑",999,1);

 bag.BuyItem(i);
 bag.BuyItem(i2);
 bag.BuyItem(i3);

 bag.SellItem(i3);
 bag.SellItem(1,1);
 bag.SellItem(1,5);
 bag.SellItem(1,5);
 bag.SellItem(2,11);
```