# JAVA类加载过程

![image-20200314234203055](C:\Users\zyk\AppData\Roaming\Typora\typora-user-images\image-20200314234203055.png)



以上图为例，

第一步，要明确需要用到的内存区域为，栈（Stack），堆（Heap），方法区（Method Area）

第二步，加载方法到方法区，也就是上图中的方法区的所有内容

第三步，加载方法入栈，由于Demo01PhoneOne.class当中包含主方法，所以率先入栈

第四步，main入栈以后开始创建Phone one 对象，在堆中**new Phone();**   在栈和堆之间以0x666的地址相连

第五步，在堆中**new Phone();** 以后调用方法区的成员变量，成员方法进入堆中，成员变量赋初值（null,0.0,null），成员方法在堆中以地址值存在，以0x333在堆和方法区之间相连

第六步，在栈中**one.brand="苹果";** 这一步会跑到堆中，替换初值

第七步，**one.call(“乔布斯”);** 同样先跑到堆中找，发现是个方法，根据地址跑到方法区中，然后入栈，将“乔布斯”赋值，返回以后，该方法弹栈。

第八步，**one.sendMessage();**步骤同上，该方法弹栈以后，所有成员方法调用完毕，main方法弹栈。

# 构造函数在内存中的加载过程

[构造函数在内存中的加载过程](https://blog.csdn.net/weixin_42947972/article/details/101478230)

# JAVA类加载过程（静态代码块，构造函数，）

[Java类加载过程]: D:\dogdog\java\javatest\src\faceObject\demo06ClassLoading.java







