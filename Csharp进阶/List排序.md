## List自带排序方法
[List](常用泛型数据结构类/List.md)
```C#
List<int> list = new List<int>();
list.Add(1);
list.Add(4);
list.Add(5);
list.Add(2);
list.Add(3);
list.Add(6);
for (int i = 0; i < list.Count; i++)
{
    Console.WriteLine(list[i]);
}
//list提供了排序方法
list.Sort();
for (int i = 0; i < list.Count; i++)
{
    Console.WriteLine(list[i]);
}
```
ArrayList中也有Sort排序方法

## 自定义类的排序
```C#
class Item : IComparable<Item>
{
    public int money;
    public Item(int money)
    { 
        this.money = money;
    }

    public int CompareTo(Item other)
    {
        //返回值的含义
        //小于0:
        //放在传入对象的前面
        //等于0:
        //保持当前位置不变
        //大于0:
        //放在传入对象的后面

        //简单理解: 传入对象的位置 就是0
        //如果你的返回值为负数 就放在它的左边 也就是前面
        //如果你的返回值是正数 就放在它的右边 也就是后面
        if (this.money > other.money)
        {
            return 1;
        }
        else
        {
            return -1;
        }

        return 0;
    }
}
```

```C#
List<Item> itemList = new List<Item>();
itemList.Add(new Item(1));
itemList.Add(new Item(0));
itemList.Add(new Item(11));
itemList.Add(new Item(13));
itemList.Add(new Item(14));
itemList.Add(new Item(15));
itemList.Add(new Item(199));
//排序方法
itemList.Sort();
for (int i = 0; i < itemList.Count; i++)
{
    Console.WriteLine(itemList[i].money);
}
```

## 通过委托函数进行排序
```C#
class ShopItem
{
    public int id;
    public ShopItem(int id)
    {
        this.id = id;
    }
}
```

```C#
static int SortShopItem(ShopItem a, ShopItem b)
{
    //传入的两个对象 为把列表中的两个对象
    //进行两两比较 用左边和右边的条件 比较
    //返回规则 0做标准 负数在左(前) 正数在右(后)排序
    if (a.id > b.id)
    {
        return -1;
    }
    else
    {
        return 1;
    }
    return 0;
}
```

```C#
        List<ShopItem> shopItems = new List<ShopItem>();
        shopItems.Add(new ShopItem(1));
        shopItems.Add(new ShopItem(4));
        shopItems.Add(new ShopItem(5));
        shopItems.Add(new ShopItem(9));
        shopItems.Add(new ShopItem(0));

        //重载Sort 通过委托进行排序
        shopItems.Sort(SortShopItem);
        //简写
        //匿名函数:
        shopItems.Sort(delegate(ShopItem a,ShopItem b)
        {
            if (a.id > b.id)
            {
                return 1;
            }
            else
            {
                return -1;
            }
        });
        //再简写:
        //lambad表达式 配合 三目运算符 完美呈现
        shopItems.Sort((a, b) =>
        {
            return a.id > b.id ? -1 : 1;
        });


        Console.WriteLine("-----fgx-----");
        for (int i = 0;i < shopItems.Count; i++)
        {
            Console.WriteLine(shopItems[i].id);
        }
```

---





