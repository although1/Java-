# JAVA 线程相关

### 更多线程知识

 https://www.cnblogs.com/kexianting/p/8566318.html 

### 多线程的实现方式

继承Thread类、实现Runnable接口、使用ExecutorService、Callable、Future实现有返回结果的多线程。

### Runnable接口的优点

1、避免了单继承的局限性

2、增强了程序的拓展性，降低了程序的耦合性（解耦）

### 线程的状态转换

 https://www.cnblogs.com/nwnu-daizh/p/8036156.html 

### 如何停止一个线程

参考文章：

http://www.cnblogs.com/greta/p/5624839.html

### 什么是线程安全

线程安全就是多线程访问同一代码，不会产生不确定的结果。

### 如何保证线程安全

对非安全的代码进行加锁控制；

使用线程安全的类；

多线程并发情况下，线程共享的变量改为方法级的局部变量。

### synchronized如何使用

synchronized是Java中的关键字，是一种同步锁。它修饰的对象有以下几种：

1). 修饰一个代码块，被修饰的代码块称为同步语句块，其作用的范围是大括号{}括起来的代码，作用的对象是调用这个代码块的对象；

2). 修饰一个方法，被修饰的方法称为同步方法，其作用的范围是整个方法，作用的对象是调用这个方法的对象；

3). 修改一个静态的方法，其作用的范围是整个静态方法，作用的对象是这个类的所有对象；

4). 修改一个类，其作用的范围是synchronized后面括号括起来的部分，作用主的对象是这个类的所有对象。

### synchronized和Lock的区别

主要相同点：Lock能完成synchronized所实现的所有功能

主要不同点：Lock有比synchronized更精确的线程语义和更好的性能。Lock的锁定是通过代码实现的，而synchronized是在JVM层面上实现的，synchronized会自动释放锁，而Lock一定要求程序员手工释放，并且必须在finally从句中释放。Lock还有更强大的功能，例如，它的tryLock方法可以非阻塞方式去拿锁。Lock锁的范围有局限性，块范围，而synchronized可以锁住块、对象、类。

### 多线程如何进行信息交互

void notify() 唤醒在此对象监视器上等待的单个线程。

void notifyAll() 唤醒在此对象监视器上等待的所有线程。

void wait() 导致当前的线程等待，直到其他线程调用此对象的notify()方法或notifyAll()方法。

void wait(long timeout) 导致当前的线程等待，直到其他线程调用此对象的notify()方法或notifyAll()方法，或者超过指定的时间量。

void wait(long timeout, int nanos) 导致当前的线程等待，直到其他线程调用此对象的notify()方法或notifyAll()方法，或者其他某个线程中断当前线程，或者已超过某个实际时间量。

### sleep和wait的区别(考察的方向是是否会释放锁)

sleep()方法是Thread类中方法，而wait()方法是Object类中的方法。

sleep()方法导致了程序暂停执行指定的时间，让出cpu该其他线程，但是他的监控状态依然保持者，当指定的时间到了又会自动恢复运行状态，在调用sleep()方法的过程中，线程不会释放对象锁。而当调用wait()方法的时候，线程会放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象调用notify()方法后本线程才进入对象锁定池准备。

### wait和notify的使用细节

1、wait和notify方法必须要由同一个锁对象调用。因为：对应的锁对象可以通过notify唤醒使用同一个锁对象调用的wait方法后的线程。

2、wait方法和notify方法属于Object类。因为：锁对象可以是任意对象，而任意对象的所属类都是继承了Object类的

3、wait方法和notify方法必须要在同步代码块或同步方法中使用。因为：必须要通过锁对象调用这两个方法

### 多线程与死锁

死锁是指两个或两个以上的进程在执行过程中，因争夺资源而造成的一种互相等待的现象，若无外力作用，它们都将无法推进下去。

产生死锁的原因：

一.因为系统资源不足。

二.进程运行推进的顺序不合适。

三.资源分配不当。

### 如何才能产生死锁

产生死锁的四个必要条件：

一.互斥条件：所谓互斥就是进程在某一时间内独占资源。

二.请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。

三.不剥夺条件:进程已获得资源，在未使用完之前，不能强行剥夺。

四.循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

### 死锁的预防

打破产生死锁的四个必要条件中的一个或几个，保证系统不会进入死锁状态。

一.打破互斥条件。即允许进程同时访问某些资源。但是，有的资源是不允许被同时访问的，像打印机等等，这是由资源本身的属性所决定的。所以，这种办法并无实用价值。

二.打破不可抢占条件。即允许进程强行从占有者那里夺取某些资源。就是说，当一个进程已占有了某些资源，它又申请新的资源，但不能立即被满足时，它必须释放所占有的全部资源，以后再重新申请。它所释放的资源可以分配给其它进程。这就相当于该进程占有的资源被隐蔽地强占了。这种预防死锁的方法实现起来困难，会降低系统性能。

三.打破占有且申请条件。可以实行资源预先分配策略。即进程在运行前一次性地向系统申请它所需要的全部资源。如果某个进程所需的全部资源得不到满足，则不分配任何资源，此进程暂不运行。只有当系统能够满足当前进程的全部资源需求时，才一次性地将所申请的资源全部分配给该进程。由于运行的进程已占有了它所需的全部资源，所以不会发生占有资源又申请资源的现象，因此不会发生死锁。

四.打破循环等待条件，实行资源有序分配策略。采用这种策略，即把资源事先分类编号，按号分配，使进程在申请，占用资源时不会形成环路。所有进程对资源的请求必须严格按资源序号递增的顺序提出。进程占用了小号资源，才能申请大号资源，就不会产生环路，从而预防了死锁。

### 什么叫守护线程，用什么方法实现守护线程

守护线程是为其他线程的运行提供服务的线程。

setDaemon(boolean on)方法可以方便的设置线程的Daemon模式，true为守护模式，false为用户模式。

### Java线程池技术及原理

参考文章：

http://www.cnblogs.com/dolphin0520/p/3932921.html



### java并发包concurrent及常用的类

这个内容有点多，参考文章：

并发包诸类概览：http://www.raychase.net/1912

线程池：http://www.cnblogs.com/dolphin0520/p/3932921.html

锁：http://www.cnblogs.com/dolphin0520/p/3923167.html

集合：http://www.cnblogs.com/huangfox/archive/2012/08/16/2642666.html

### volatile关键字

用volatile修饰的变量，线程在每次使用变量的时候，都会读取变量修改后的最的值。volatile很容易被误用，用来进行原子性操作。

Java语言中的volatile变量可以被看作是一种“程度较轻的

synchronized”；与

synchronized 块相比，volatile 变量所需的编码较少，并且运行时开销也较少，但是它所能实现的功能也仅是synchronized的一部分。锁提供了两种主要特性：互斥（mutual

exclusion）和可见性（visibility）。互斥即一次只允许一个线程持有某个特定的锁，因此可使用该特性实现对共享数据的协调访问协议，这样，一次就只有一个线程能够使用该共享数据。可见性必须确保释放锁之前对共享数据做出的更改对于随后获得该锁的另一个线程是可见的，如果没有同步机制提供的这种可见性保证，线程看到的共享变量可能是修改前的值或不一致的值，这将引发许多严重问题。Volatile变量具有synchronized的可见性特性，但是不具备原子特性。这就是说线程能够自动发现volatile

变量的最新值。

要使volatile变量提供理想的线程安全，必须同时满足下面两个条件：对变量的写操作不依赖于当前值；该变量没有包含在具有其他变量的不变式中。

第一个条件的限制使volatile变量不能用作线程安全计数器。虽然增量操作（x++）看上去类似一个单独操作，实际上它是一个由读取－修改－写入操作序列组成的组合操作，必须以原子方式执行，而volatile不能提供必须的原子特性。实现正确的操作需要使x 的值在操作期间保持不变，而volatile

变量无法实现这点。

每一个线程运行时都有一个线程栈，线程栈保存了线程运行时候变量值信息。当线程访问某一个对象时候值的时候，首先通过对象的引用找到对应在堆内存的变量的值，然后把堆内存变量的具体值load到线程本地内存中，建立一个变量副本，之后线程就不再和对象在堆内存变量值有任何关系，而是直接修改副本变量的值，在修改完之后的某一个时刻（线程退出之前），自动把线程变量副本的值回写到对象在堆中变量。这样在堆中的对象的值就产生变化了。

read and load 从主存复制变量到当前工作内存

use and assign 执行代码，改变共享变量值

store and write 用工作内存数据刷新主存相关内容

其中use and

assign 可以多次出现，但是这一些操作并不是原子性，也就是在read load之后，如果主内存count变量发生修改之后，线程工作内存中的值由于已经加载，不会产生对应的变化，所以计算出来的结果会和预期不一样。