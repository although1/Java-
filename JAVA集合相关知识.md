# JAVA集合相关知识

### **12.Java中的集合类及关系图**

List和Set继承自Collection接口。

Set无序不允许元素重复。HashSet和TreeSet是两个主要的实现类。

List有序且允许元素重复。ArrayList、LinkedList和Vector是三个主要的实现类。

Map也属于集合系统，但和Collection接口没关系。Map是key对value的映射集合，其中key列就是一个集合。key不能重复，但是value可以重复。HashMap、TreeMap和Hashtable是三个主要的实现类。

SortedSet和SortedMap接口对元素按指定规则排序，SortedMap是对key列进行排序。

### **13.HashMap实现原理**

具体原理参考文章：

http://zhangshixi.iteye.com/blog/672697

http://www.admin10000.com/document/3322.html

### **14.HashTable实现原理**

具体原理参考文章：

http://www.cnblogs.com/skywang12345/p/3310887.html

http://blog.csdn.net/chdjj/article/details/38581035

### **15.HashMap和HashTable区别**

1）.HashTable的方法前面都有synchronized来同步，是线程安全的；HashMap未经同步，是非线程安全的。

2）.HashTable不允许null值(key和value都不可以) ；HashMap允许null值(key和value都可以)。

3）.HashTable有一个contains(Object

value)功能和containsValue(Object

value)功能一样。

4）.HashTable使用Enumeration进行遍历；HashMap使用Iterator进行遍历。

5）.HashTable中hash数组默认大小是11，增加的方式是old*2+1；HashMap中hash数组的默认大小是16，而且一定是2的指数。

6）.哈希值的使用不同，HashTable直接使用对象的hashCode； HashMap重新计算hash值，而且用与代替求模。

### **16.ArrayList和vector区别**

ArrayList和Vector都实现了List接口，都是通过数组实现的。

Vector是线程安全的，而ArrayList是非线程安全的。

List第一次创建的时候，会有一个初始大小，随着不断向List中增加元素，当List 认为容量不够的时候就会进行扩容。Vector缺省情况下自动增长原来一倍的数组长度，ArrayList增长原来的50%。

### **17.ArrayList和LinkedList区别及使用场景**

区别

ArrayList底层是用数组实现的，可以认为ArrayList是一个可改变大小的数组。随着越来越多的元素被添加到ArrayList中，其规模是动态增加的。

LinkedList底层是通过双向链表实现的， LinkedList和ArrayList相比，增删的速度较快。但是查询和修改值的速度较慢。同时，LinkedList还实现了Queue接口，所以他还提供了offer(),

peek(), poll()等方法。

使用场景

LinkedList更适合从中间插入或者删除（链表的特性）。

ArrayList更适合检索和在末尾插入或删除（数组的特性）。

### **18.Collection和Collections的区别**

java.util.Collection 是一个集合接口。它提供了对集合对象进行基本操作的通用接口方法。Collection接口在Java 类库中有很多具体的实现。Collection接口的意义是为各种具体的集合提供了最大化的统一操作方式。

java.util.Collections 是一个包装类。它包含有各种有关集合操作的静态多态方法。此类不能实例化，就像一个工具类，服务于Java的Collection框架。

### **19.Concurrenthashmap实现原理**

具体原理参考文章：

http://www.cnblogs.com/ITtangtang/p/3948786.html

http://ifeve.com/concurrenthashmap/