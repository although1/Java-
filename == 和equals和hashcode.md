# == 和equals和hashcode

## == 和equals的区别

== : 它的作用是判断两个对象的地址是不是相等。即判断两个对象是不是同一个对象(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)。

equals() : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况：

​	情况1：类没有覆盖 equals() 方法。则通过 equals() 比较该类的两个对象时，等价于通过“==”比较这两个对象。

​	情况2：类覆盖了 equals() 方法。一般，我们都覆盖 equals() 方法来比较两个对象的内容是否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

## 为什么重写equals方法和hashcode方法？

举个例子，创建一个HashMap<User,String> ， 其中User是个对象

```java
        Map<User,String> map = new HashMap<>();
        User user1 = new User(55,"任正非");
        User user2 = new User(55,"任正非");
        map.put(user1,"深圳");
        map.put(user2,"北京");
        System.out.println("user1的地址 "+user1); //collections.User@4f023edb
        System.out.println("user2的地址 "+user2); //collections.User@3a71f4dd
        System.out.println("user1的hashCode "+user1.hashCode()); //1325547227
        System.out.println("user2的hashCode "+user2.hashCode()); //980546781
        System.out.println("user1对比user2  =  "+user1.equals(user2)); //true

        Set<Map.Entry<User, String>> entries = map.entrySet();
        for (Map.Entry<User, String> entry : entries) {
            User key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key+"-->"+value);//collections.User@4f023edb-->深圳
												//collections.User@3a71f4dd-->北京
        }

```

注意任正非的那条，如果没有重写equals方法和hashcode方法，会打印出来两个任正非，一般情况下，我们会把姓名和年龄相同的人认为是同一个人，此时没有重写，比较的是两个User的地址值，而地址值不同，会认为是两个不同的Key，重写的目的是为了让地址和内容都相同

## 为什么重写equals方法必须要重写hashcode方法？

>  设计HashCode()时最重要的因素就是：无论何时，对同一个对象调用hashCode()都应该产生同样的值。如果在讲一个对象用put()添加进HashMap时产生一个hashCdoe值，而用get()取出时却产生了另一个hashCode值，那么就无法获取该对象了。所以如果你的hashCode方法依赖于对象中易变的数据，用户就要当心了，因为此数据发生变化时，hashCode()方法就会生成一个不同的散列码 
>
> ​																																	--《Java编程思想》

```java
	//User类中重写的部分  
	@Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return age == user.age &&
                Objects.equals(name, user.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(age, name);
    }
```

假如只重写equals而不重写hashcode，那么User类的hashcode方法就是Object默认的hashcode方法，由于默认的hashcode方法是根据对象的内存地址经哈希算法得来的，显然此时user1!=user2,故两者的hashcode不一定相等。 

还是以上面的HashMap的例子来说，如果只重写了equals，认为两个对象的内容相同，而两个对象的地址值，仍旧不同，这样其实是冲突的，仍会被认为是两个对象，重写hashCode的目的是为了让地址相同，此时地址内容都相同从而被认为是一个对象



```java
user1的地址 collections.User@1361f00
user2的地址 collections.User@1361f00
user1的hashCode 20324096
user2的hashCode 20324096
user1对比user2  =  true
collections.User@1361f00-->北京
```

