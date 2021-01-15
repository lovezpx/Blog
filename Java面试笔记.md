# Java学习笔记

### 一、JAVA基础

#### 1、String类

<font color='green'>关键词:栈内存、堆内存、方法区常量池、对象比较、final</font>

String类被final修饰，意义在于安全性和稳定性。String不能被继承、修改，可以避免因为继承引起的安全隐患。

问题1：String a ="abc" String b="abc" String c=new String("abc"); String d="ab"+"c"之间用==比较的结果

答：

``` 
String a = "abc";
String b = "abc";
String c = new String("abc");
String d = "ab" +"c";

a == b //true;
a == c //false;
a == d //true;
b == c //false;
b == d //true;
c == d //false;

```

问题2：string、stringbuilder、stringbuffer区别

答：
<font color='orange'>

执行速度：StringBuilder > StringBuffer > String

String为字符串常量，而StringBuilder和StringBuffer均为字符串变量，即String对象一旦创建之后该对象是不可更改的，但后两者的对象是变量，是可以更改的。

StringBuilder是线程不安全的，而StringBuffer是线程安全的。

</font>

问题3：String 类的常用方法

答：
<font color='orange'>
public int length()//返回该字符串的长度。

public char charAt(int index)//返回字符串中指定位置的字符；注意字符串中第一个字符索引是0，最后一个是length()-1。

public String substring(int beginIndex)//该方法从beginIndex位置起，从当前字符串中取出剩余的字符作为一个新的字符串返回。

public String substring(int beginIndex, int endIndex)//该方法从beginIndex位置起，从当前字符串中取出到endIndex-1位置的字符作为一个新的字符串返回。

public int compareTo(String anotherString)//该方法是对字符串内容按字典顺序进行大小比较，通过返回的整数值指明当前字符串与参数字符串的大小关系。若当前对象比参数大则返回正整数，反之返回负整数，相等返回0。

public int compareToIgnore(String anotherString)//与compareTo方法相似，但忽略大小写。

public boolean equals(Object anotherObject)//比较当前字符串和参数字符串，在两个字符串相等的时候返回true，否则返回false。

public boolean equalsIgnoreCase(String anotherString)//与equals方法相似，但忽略大小写。

public String concat(String str)//将参数中的字符串str连接到当前字符串的后面，效果等价于"+"。

</font>

#### 2、HashMap类

<font color='green'>关键词:哈希表、哈希冲突、负载因子(loadFactor)、null键、null值、红黑树(JDK1.8)</font>

``` Map map = Collections.synchronizedMap(new HashMap()); ```

loadFactor负载隐私是表示Hash表中元素的填满的程度，如果机器内存足够，并想提高查询速度加载因子设置小一点；如果机器内存紧张，并且对查询速度没有特殊要求，加载因子设置大一点。默认0.75。

JDK1.8版本后，HashMap修改成"数组+链表或红黑树"实现的。

<font color='orange'>

二叉查找树特性：</br>
(1)左子树上所有结点的值均小于或等于根结点的值。</br>
(2)右子树上所有结点的值均大于或等于根结点的值。</br>
(3)左、右子树也分别为二叉排序树。</br>

红黑树特性：</br>
(1)每个节点要么是黑色，要么是红色。</br>
(2)根节点是黑色。</br>
(3)每个叶子节点（NIL）是黑色。</br>
(4)每个红色结点的两个子结点一定都是黑色。</br>
(5)任意一结点到每个叶子结点的路径都包含数量相同的黑结点。</br>

Hash冲突怎么办？哪些解决散列冲突的方法？：</br>

开放定址法、线性探测再散列、二次探测再散列、再哈希法、链地址法、建立公共溢出区

</font>

#### 3、List类

<font color='green'>关键词:线程安全、ArrayList、LinkedList、Vector</font>

ArrayList：线程不安全，默认初始尺寸10，每次扩容为原容量1.5倍。

LinkedList：线程不安全，双向链表，无固定容量无需扩容。

Vector：线程安全，特性类似ArrayList，默认初始尺寸10，每次扩容为原容量2倍。

#### 4、Set类

<font color='green'>关键词:HashSet、LinkedHashSet、TreeSet、ConcurrentHashSet</font>

HashSet：线程不安全，集合不存在重复数据，允许空数据，无序集合。

LinkedHashSet：线程不安全，有序集合。

TreeSet：线程不安全，红黑树实现。

ConcurrentHashSet：线程安全。

#### 5、Queue类

<font color='green'>关键词:LinkList、PriorityQueue、ConcurrentLinkedQueue、BlockingQueue</font>

阻塞队列：

ArrayBlockingQueue ：一个由数组结构组成的有界阻塞队列。

LinkedBlockingQueue ：一个由链表结构组成的有界阻塞队列。

PriorityBlockingQueue ：一个支持优先级排序的无界阻塞队列。

DelayQueue：一个使用优先级队列实现的无界阻塞队列。

SynchronousQueue：一个不存储元素的阻塞队列。

LinkedTransferQueue：一个由链表结构组成的无界阻塞队列。

LinkedBlockingDeque：一个由链表结构组成的双向阻塞队列。

&emsp;|抛出异常|返回特殊值|一直阻塞|超时退出
-|-|-|-|-
插入方法|add(o)|offer(o)|put(o)|offer(o,timeout,timeunit)
移除方法|remove(o)|poll()|take(o)|poll(o,timeout,timeunit)
检查方法|element()|peek()|<center>---</center>|<center>---</center>

#### 6、Map类

<font color='green'>关键词:HashMap、HashTable、ConcurrentHashMap、TreeMap、LinkedHashMap、WeakHashMap</font>

HashMap：线程不安全。

HashTable：线程安全，不推荐使用。

ConcurrentHashMap：线程安全，类似HashMap，Entry超过8个自动从链表为红黑树。

TreeMap：线程不安全，Key默认按从小到大排序。

LinkedHashMap：线程不安全，有序，先进先出。

#### 7、反射机制

<font color='green'>关键词:ClassLoader、Class.forName</font>

Class.forName：将.class文件加载到jvm中，执行类中的static块，对其进行初始化。

ClassLoader：将.class文件加载到jvm中，不执行初始化。

#### 8、JAVA7、JAVA8的新特性

<font color='orange'>

JAVA7特性：

* 1、数值类型字面值可以用多个"_"分隔增加可读性。
* 2、可以使用字符串控制switch语句。
* 3、带资源的try语句，当资源不再使用时能够自行释放。
* 4、多重捕获异常(multi-catch)，本来不同的异常是由多个catch语句块来处理，现在可以把多个异常用一个catch语句块来处理，用’|’来表示多个异常
* 5、编译器会分析完整的try代码块以检查从catch块中什么类型的异常被抛出和重新抛出

JAVA8特性：

* 1、可以为接口添加static方法和默认实现。（方法接口）
* 2、新增@FunctionalInterface注解，属于标记注解，用来标记被注解的接口是函数式接口。
* 3、增加了类型注解，在之前注解只能用于声明，也就是方法、变量、类、接口声明的地方，java8开始在很多使用类型的其它地方也可以使用注解。
* 4、lambda表达式，函数式编程

</font>

#### 9、Java内存泄漏问题定位

<font color='green'>关键词:jmap、jstack</font>

#### 10、hashtable和hashmap的区别

HashTable是线程安全的，HashMap是线程不安全的。

#### 11、异常的结构，运行时异常和非运行时异常，各举个例子

![avatar](https://img-blog.csdn.net/20140825105709593?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVodWlfY3M=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

java.lang.Throwable作为所有异常的超类

RuntimeException运行时异常例如：NullPointerException、IndexOutOfBoundsException等。

非运行时异常例如：IOException、SQLException等。

> 常见RuntimeException：
>> ArrayStoreException 试图将错误类型的对象存储到一个对象数组时抛出的异常
>
>> ClassCastException 类型转换异常
>
>> IllegalArgumentException 抛出的异常表明向方法传递了一个不合法或不正确的参数
>
>> IndexOutOfBoundsException 数组越界异常
>
>> NoSuchElementException 表明枚举中没有更多的元素
>
>> NullPointerException 空指针异常

#### 12、Java 的引用类型有哪几种

<font color='green'>关键词:强引用、软引用、弱引用、虚引用、引用队列</font>

引用队列可以与软引用、弱引用以及虚引用一起配合使用，当垃圾回收器准备回收一个对象时，如果发现它还有引用，那么就会在回收对象之前，把这个引用加入到与之关联的引用队列中去。程序可以通过判断引用队列中是否已经加入了引用，来判断被引用的对象是否将要被垃圾回收，这样就可以在对象被回收之前采取一些必要的措施。

与软引用、弱引用不同，虚引用必须和引用队列一起使用。

#### 13、抽象类和接口的区别

> 抽象类可以有构造方法，接口中不能有构造方法。

> 抽象类中可以有普通成员变量，接口中没有普通成员变量

> 抽象类中可以包含非抽象的普通方法，接口中的所有方法必须都是抽象的，不能有非抽象的普通方法。

> 抽象类中的抽象方法的访问类型可以是public，protected和（默认类型,虽然 eclipse下不报错，但应该也不行），但接口中的抽象方法只能是public类型的，并且默认即为public abstract类型。

> 抽象类中可以包含静态方法，接口中不能包含静态方法

> 抽象类和接口中都可以包含静态成员变量，抽象类中的静态成员变量的访问类型可以任意，但接口中定义的变量只能是public static final类型，并且默认即为public static final类型。

> 一个类可以实现多个接口，但只能继承一个抽象类。

#### 14、java的基础类型和字节大小

> Java基本数据类型有8种：byte、short、int、long、float、double、boolean、char

分为4类：整数型、浮点型、布尔型、字符型。

整数型：byte、short、int、long

浮点型：float、double

布尔型：boolean

字符型：char

> 各数据类型所占字节大小

计算机的基本单位：bit（一个bit代表一个0或1）

byte：1byte = 8bit  1个字节是8个bit

short：2byte

int：4byte

long：8byte

float：4byte

double：8byte

boolean：1byte

char：2byte

#### 15、hashCode() 与 equals() 重写


---
### 二、Java IO

1、IO里面的常见类，字节流、字符流、接口、实现类、方法阻塞。

基于字节的io操作：

![avatar](https://img-blog.csdn.net/20180625160227750?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQzNzgxODE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![avatar](https://img-blog.csdn.net/20180625160250741?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQzNzgxODE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

基于字符的io操作：

![avatar](https://img-blog.csdn.net/20180625160305244?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQzNzgxODE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![avatar](https://img-blog.csdn.net/20180625160313169?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQzNzgxODE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

2、NIO

同步非阻塞，服务器实现一个连接一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4之后开始支持。

3、AIO

异步非阻塞，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由操作系统先完成了再通知服务器应用去启动线程进行处理，AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用操作系统参与并发操作，编程比较复杂，JDK1.7之后开始支持。

4、String编码UTF-8和GBK的区别。

字符均使用双字节来表示，只不过为区分中文，将其最高位都定成1。

至于UTF－8编码则是用以解决国际上字符的一种多字节编码，它对英文使用8位（即一个字节），中文使用24位（三个字节）来编码。对于英文字符较多的论坛则用UTF－8节省空间。

GBK包含全部中文字符；UTF-8则包含全世界所有国家需要用到的字符。

GBK是在国家标准GB2312基础上扩容后兼容GB2312的标准（好像还不是国家标准）

UTF-8编码的文字可以在各国各种支持UTF8字符集的浏览器上显示。
比如，如果是UTF8编码，则在外国人的英文IE上也能显示中文，而无需他们下载IE的中文语言支持包。 所以，对于英文比较多的论坛 ，使用GBK则每个字符占用2个字节，而使用UTF－8英文却只占一个字节。

UTF8是国际编码，它的通用性比较好，外国人也可以浏览论坛，GBK是国家编码，通用性比UTF8差，不过UTF8占用的数据库比GBK大。

5、什么时候使用字节流、什么时候使用字符流?

字节流和字符流的主要区别是什么呢？

一.字节流在操作时不会用到缓冲区（内存），是直接对文件本身进行操作的。而字符流在操作时使用了缓冲区，通过缓冲区再操作文件。
    
二.在硬盘上的所有文件都是以字节形式存在的（图片，声音，视频），而字符值在内存中才会形成。
    
上面两点能说明什么呢？
    
我们知道，如果一个程序频繁对一个资源进行IO操作，效率会非常低。此时，通过缓冲区，先把需要操作的数据暂时放入内存中，以后直接从内存中读取数据，则可以避免多次的IO操作，提高效率
    
真正存储和传输数据时都是以字节为单位的，字符只是存在与内存当中的，所以，字节流适用范围更为宽广

---
### 三、Java Web

1、session和cookie的区别和联系，session的生命周期，多个服务部署时session管理

对象|信息量大小|保存时间|应用范围|保存位置
-|-|-|-|-
Session|小量,简单的数据|用户活动时间+一段延迟时间（一般为20分钟）|单个用户|服务器端
Cookie|小量,简单的数据|根据需要设置|单个用户|客户端

Session从用户调用Servlet之后，由HttpServletRequest.getSession(true) 创建。Session存储在服务器端，一般为了防止在服务器的内存中（为了高速存取），Sessinon在用户访问第一次访问服务器时创建，需要注意只有访问JSP、Servlet等程序时才会创建Session，只访问HTML、IMAGE等静态资源并不会创建Session，可调用request.getSession(true)强制生成Session。

2、Setvlet的一些相关问题

servlet容器也叫web容器，比如tomcat。它的主要职责如下：

<li>提供通信支持（communication support）

> 容器为web服务器和servlet/jsp提供了便捷的通信方式。正是由于web容器，我们不再需在服务端创建一个服务端socket对象监听、解析任何请求以及生成响应。所有这些重要且复杂的工作统统由容器为我们完成，我们仅仅需要关注我们自己应用的业务逻辑而已。

<li>生命周期和资源管理（lifecycle and resource management）

> 容器管理所有servlet的生命周期，它还负责加载servlet到内存，初始化servler，执行servlet中的方法以及销毁servlet，容器同时还提供诸如JNDI（java命名与目录服务）的资源管理工具。

<li>多线程支持（multitheading support）

> 容器为每个请求创建一个新的线程并当请求结束时及时摧毁线程。servlet只有一个实例，容器并不会为每个请求生成单独的servlet，这必然节省了时间和空间。

<li>支持jsp(jsp support)

> jsp跟普通java类还是有区别的，web容器对此也是提供支持的。每个jsp页面在被容器编译后会生成对应的servlet，然后容器就像管理servlet一样管理它们。

<li>多任务（miscellaneous task）

> web容器管理资源池，做内存优化，运行gc，提供安全配置，提供多应用的支持，热部署，以及其他一些我们没法看到的工作。

3、webservice相关问题

> webservice是什么？
<li>基于WEB的服务，服务端整出一些资源让客户端应用访问（提供数据）
<li>webservice是一个跨语言跨平台的规范（抽象）
<li>是多个跨语言跨平台的应用间通信整合的方案（实际）

> wsdl（WebService Definition Language）是什么？
<li>webservice定义语言，对应.wsdl文档
<li>定义了webservice服务器端和客户端应用交互传递请求数据的格式和过程
<li>一个webservice对应一个唯一的wsdl文档

> SOAP（Simple Object Access Protocal）简单对象访问协议
<li>是一种简单的，基于HTTP和XML的协议，用于在WEB交换结构化(XML)的数据
<li>SOAP消息：请求消息和响应消息
<li>HTTP+XML片断


4、jdbc连接，forname方式的步骤，怎么声明使用一个事务。举例并具体代码

5、jsp和servlet的区别

> jsp经编译后就变成了Servlet。

> jsp更擅长表现于页面显示,servlet更擅长于逻辑控制。

> Servlet中没有内置对象，Jsp中的内置对象都是必须通过HttpServletResponse对象以及HttpServlet对象得到。

> Servlet则是个完整的Java类，这个类的Service方法用于生成对客户端的响应。

---
### 四、JVM

1、Java的内存模型以及GC算法

![avatar](https://images2015.cnblogs.com/blog/1196330/201707/1196330-20170723142133809-928230884.png)

2、jvm性能调优主要做什么

> 控制GC的行为。GC是一个后台处理，但是它也是会消耗系统性能的，因此经常会根据系统运行的程序的特性来更改GC行为。


> 控制JVM堆栈的大小。一般来说，JVM在内存分配上不需要你修改，(举例)但是当你的程序新生代对象在某个时间段产生的比较多的时候，就需要控制新生代的堆大小。同时,还要需要控制总的JVM大小避免内存溢出。

> 控制JVM线程的内存分配。如果是多线程程序，产生线程和线程运行所消耗的内存也是可以控制的，需要通过一定时间的观测后，配置最优结果。

3、介绍JVM中7个区域，然后把每个区域可能造成内存的溢出的情况说明

> java内存区域

    线程私有内存区域（三个）：程序计数器、本地方法栈、虚拟机栈
    --- 具有和线程相同的生命周期。
    
    线程共享区域（四个）：java堆、方法区、常量池、直接内存区
    --- 所有线程共享，在JVM启动时就会分配。
    
> 每个区域可能造成的异常

    1）程序计数器（唯一不会抛出OutOfMemoryError）：
    程序计数器是众多编程语言都共有的一部分，作用是标示下一条需要执行的指令的位置，分支、循环、跳转、异常处理、线程恢复等基础功能都是依赖程序计数器完成的。
    对于Java的多线程程序而言，不同的线程都是通过轮流获得cpu的时间片运行的，这符合计算机组成原理的基本概念，因此不同的线程之间需要不停的获得运行，挂起等待运行，所以各线程之间的计数器互不影响，独立存储。这些数据区属于线程私有的内存。

    2）Java虚拟机栈（栈溢出StackOverflowError、内存溢出OutOfMemoryError）：
    VM虚拟机栈也是线程私有的，生命周期与线程相同。虚拟机栈描述的是Java方法执行的内存模型：每个方法在执行的同时都会创建一个栈帧(Stack Frame)用于存储局部变量表、操作数栈、动态链接、方法出口等信息。每一个方法调用直至执行完的过程，就对应着一个栈帧在虚拟机栈中入栈到出栈的过程。

    由于栈帧的进出栈，显而易见的带来了空间分配上的问题。如果线程请求的栈深度大于虚拟机所允许的深度，将抛出StackOverFlowError异常；如果虚拟机栈可以扩展，扩展时无法申请到足够的内存，将会抛出OutOfMemoryError。显然，这种情况大多数是由于循环调用与递归带来的。

    3）本地方法栈（栈溢出StackOverflowError、内存溢出OutOfMemoryError）：
    本地方法栈与虚拟机栈的作用十分类似，不过本地方法是为native方法服务的。部分虚拟机（比如 Sun HotSpot虚拟机）直接将本地方法栈与虚拟机栈合二为一。与虚拟机栈一样，本地方法栈也会抛出StactOverFlowError与OutOfMemoryError异常。
    至此，线程私有数据区域结束，下面开始线程共享数据区。

    4）Java堆（内存溢出OutOfMemoryError）：
    Java堆是虚拟机所管理的内存中最大的一块，在虚拟机启动时创建，此块内存的唯一目的就是存放对象实例，几乎所有的对象实例都在堆上分配内存。JVM规范中的描述是：所有的对象实例以及数据都要在堆上分配。但是随着JIT编译器的发展与逃逸分析技术的逐渐成熟，栈上分配(对象只存在于某方法中，不会逃逸出去，因此方法出栈后就会销毁，此时对象可以在栈上分配，方便销毁)，标量替换(新对象拥有的属性可以由现有对象替换拼凑而成，就没必要真正生成这个对象)等优化技术带来了一些变化，目前并非所有的对象都在堆上分配了。
    当java堆上没有内存完成实例分配，并且堆大小也无法扩展是，将会抛出OutOfMemoryError异常。Java堆是垃圾收集器管理的主要区域。

    5）方法区（内存溢出OutOfMemoryError）：
    方法区与java堆一样，是线程共享的数据区，用于存储被虚拟机加载的类信息、常量、静态变量、即时编译的代码。JVM规范将方法与堆区分开，但是HotSpot将方法区作为永久代(Permanent Generation)实现。这样方便将GC分代收集方法扩展至方法区，HotSpot的垃圾收集器可以像管理Java堆一样管理方法区。但是这种方向已经逐步在被HotSpot替换中，在JDK1.7的版本中，已经把原本存放在方法区的字符串常量区移出。
    至此，JVM规范所声明的内存模型已经分析完毕，下面将分析一些经常提到的与内存相关的区域。

    6）运行时常量池（内存溢出OutOfMemoryError）：
    运行时常量池是方法区的一部分。Class文件中除了有类的版本、字段、方法、接口等信息外，还有一项信息是常量池(Constant Poll Table)用于存放编译期生成的各种字面量和符号引用，这部分内容将在类加载后进入方法区的运行时常量池存放。

4、介绍GC和GC Root不正常引用

> java内存区域

---
### 五、开源框架

1、hibernate和ibatis的区别

2、Mybatis连接池