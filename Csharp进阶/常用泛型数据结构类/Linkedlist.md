## LinkedList的本质

`LinkedList`是一个C#为我们封装好的类
它的本质是一个可变类型的**泛型双向链表**
### 声明
需要引用命名空间
```C#
using System.Collections.Generic
```

```C#
LinkedList<int> linkedList = new LinkedList<int>();
LinkedList<string> listedList2 = new LinkedList<string>();
```
链表对象 需要掌握两个类
一个是链表本身 一个是链表节点类`LinkedListNode`


### 增删查改

#### 增
1.在链表尾部添加元素
```C#
linkedList.AddLast(10);
```
2.在链表头部添加元素
```C#
linkedList.AddFirst(20);
```
3.在某个节点之后添加一个节点
要指定节点 先得得到一个节点
```C#
LinkedListNode<int> n = linkedList.Find(20);
linkedList.AddAfter(n, 11);
```
4.在某一个节点之前添加一个节点
要指定节点 先得到一个节点
```C#
linkedList.AddBefore(n, 12);
```

#### 删
1.移除头节点
```C#
linkedList.RemoveFirst();
```
2.移除尾部节点
```C#
linkedList.RemoveLast();
```
3.移除指定节点
无法通过位置直接移除
```C#
linkedList.Remove(20);
```
4.清空
```C#
linkedList.Clear();
```

#### 查
1.头节点
```C#
LinkedListNode<int> first = linkedList.First;
```
2.尾节点
```C#
LinkedListNode<int> last = linkedList.Last;
```
3.找到指定值的节点
**无法**直接**通过下标查找**获取中间元素
只有遍历查找指定位置元素
```C#
LinkedListNode<int> node = linkedList.Find(3);
Console.WriteLine(node.Value);
```
如果没有这个元素则返回`null`
4.判断是否存在
```C#
if (linkedList.Contains(1))
{
    Console.WriteLine("存在");
}
```

#### 改
要先得到再改 得到节点 在改变其中的值
```C#
Console.WriteLine(linkedList.First.Value);
linkedList.First.Value = 10;
linkedList.Find(3).Value = 10;
Console.WriteLine(linkedList.First.Value);
```
