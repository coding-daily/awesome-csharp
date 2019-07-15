
![](https://raw.githubusercontent.com/coding-daily/awesome-csharp/master/logo-lg.png)

    C Sharp语法深入系列

### 目录

- .NET框架（CLR，BCL，FCL，CTS，CLS）
- C#基础语法（拆箱装箱、值类型与引用类型、String与字符操作、类抽象类接口委托事件、常量属性字段方法特性、抽象继承多态、泛型、关键字）
- 内存管理与GC垃圾回收 
- 内置数据结构（）
- 接口分析（IEnumerable、IEnumerable< T >、IComparable、IComparable< in T >、IFormattable、IFormatProvider、IConvertible、ICloneable、IEquatable< T >、IComparer< in T >、IEqualityComparer< in T >、IDisposable、IAsyncResult、ICollection< T >、IList< T >、IQueryable、IQueryProvider、IDictionary< TKey, TValue >、INotifyPropertyChanged、IEditableObject）
- Lambda、linq、SQL
- 进程与线程、多线程与异步
- 

------------

推荐阅读

[.NET面试题系列目录](https://www.cnblogs.com/haoyifei/p/5641115.html)

[.NET面试题解析](https://www.cnblogs.com/anding/p/5226343.html)

[DotNet进阶系列](https://www.cnblogs.com/yaopengfei/p/8853590.html)

--------------

IL学习

[30分钟？不需要，轻松读懂IL](https://www.cnblogs.com/brookshi/p/5225801.html)

[进阶篇：以IL为剑，直指async/await](https://www.cnblogs.com/brookshi/p/5240510.html)

[深入浅出.Net IL](https://www.cnblogs.com/jackson0714/p/4995980.html)

[你的C#代码是怎么跑起来的（一）](https://www.cnblogs.com/brookshi/p/5273281.html)

[你的C#代码是怎么跑起来的（二）](https://www.cnblogs.com/brookshi/p/5278284.html)

[c#内存管理概要](https://www.qingtingip.com/h_291669.html)

------------


基类（抽象类）还是接口？

接口：行为规范，表示能做什么事，成员包含方法、属性、索引器、不含字段和实现的方法
抽象类：字段、属性、实现的方法

1、IS-A对比CAN-DO关系 

IS-A代表属于，CAN-DO代表能做某事。  
如果派生类型属于基类型，那么就用基类；如果建立的是能做的关系就用接口 

2、易用性 

对于开发人员，定义从基类派生的类型通常比实现接口的所有方法要容易的多。基类可提供大量功能，所以派生类型可能只需要稍加改动即可。而提供接口的话，派生类型则需要实现所有成员。 

3、一致性实现 

无论接口协定订立的多好，都无法保证所有人100%的实现它，而如果基类正确的话，以后根据需要稍加修改即可。 

4、版本控制 

向基类添加一个方法，派生类将继承该方法。而如果向接口添加新成员，则会强迫接口的继承者更改源代码并重新编译。   


#### 泛型

原理：延时声明，在运行时进行编译。

四种：泛型方法、泛型类、泛型接口、泛型委托

泛型约束：... where T：< ... >

#### 委托与事件

Delegate：表示函数参数（签名）和返回值的类型   函数的指针|引用|类型

可以利用多播委托进行解耦和插件式开发。

默认委托：
- Func< T > 有返回值  Func< int,String >返回值类型为String，参数为int
- Action< T > 无返回值  Action< int,int>参数为两个int类型


-------------

#### 内存管理与GC垃圾回收

什么是垃圾？简单理解就是没有被引用的对象。



最常见的一类非托管资源如系统文件句柄，窗口句柄，网络连接，数据库连接，画刷，图标等。

这类资源，垃圾回收器在清理的时候会调用Object.Finalize()方法。默认情况下，方法是空的，对于非托管对象，需要在此方法中编写回收非托管资源的代码，以便垃圾回收器正确回收资源。

为了更方便的释放非托管资源，微软为非托管资源的回收专门定义了一个接口：IDisposable，接口中只包含一个Dispose()方法。任何包含非托管资源的类，都应该继承此接口，以确保非托管资源的正确释放。
在一个包含非托管资源的类中，资源释放的标准做法是：
- 继承IDisposable接口
- 实现Dispose()方法，在其中释放非托管资源，并将对象本身从垃圾回收器中移除（为了告诉垃圾回收器，此对象的资源我们已经自己释放了，它就没必要再对此对象进行回收了）；
- 实现类析构函数，在其中释放非托管资源。

C#调用C++或者C的DLL库中的函数也属于非托管资源。.NET环境下的DLL、exe叫做程序集，能够在CLR中被直接引用，非托管DLL(Dynamic Link Library)就是平常所的动态链接库等，其中就包括了封装所有Windows API函数的DLL文件。各种非托管DLL中的函数在公共语言运行库中不能直接被调用，而需要经过.Net框架提供的“平台调用”服务后才可以。
平台调用”是.Net框架为Visual Basic .Net、Visual C＃等.Net开发语言提供的一种服务，用以在托管代码中引入各种非托管DLL中封装的函数（其中包括Windows API函数）。“平台调用”依赖于元数据在运行时查找导出函数并封装其参数。

托管DLL文件，可以在.NET环境通过 “添加引用” 的方式，直接把托管DLL文件添加到项目中。然后通过 Using DLL命名空间，来调用相应的DLL对象 。

非托管DLL文件，在.NET环境应用时，通过 DllImport 调用。

在托管代码中使用“平台调用”服务调用非托管DLL中封装的函数时，“平台服务”将依次执行以下操作：

　　1． 查找包含该函数所在的DLL文件。

　　2． 如果找到，则将该DLL文件 加载到内存中。

　　3． 查找函数在内存中的地址并将其参数推到堆栈上，并封送所需的数据。

　　4． 将控制权转移给非托管函数。 这样整个函数调用完成。

------------

#### C#程序运行原理

![](https://raw.githubusercontent.com/coding-daily/awesome-csharp/master/images/C%20Sharp%E7%BC%96%E8%AF%913.png)

#### 同步块索引(synchronization block index)：

同步块索引，又被叫做对象头指针，位于对象地址的-4到0字节（以32位机型为例）。

同步块索引在线程同步中用来判断对象是被使用还是闲置。

当有线程要对某个对象操作时，检查其同步块索引的值，若为表示闲置的值，便进行操作。

然后在CLR的同步块数组中增加一块新的同步块，把此块的索引值写入同步块的索引值里，表示其被占用。

线程用完后，便把索引值改回表示闲置的值。

 

#### 方法表指针：

方法表指针指向类型对象。

类型对象是加载程序集时，在加载堆中创建的。

类型对象存储了静态字段和方法表，被所有该类型的实例共享。

方法表包括所有函数，包括静态函数和非静态函数。


------------

#### 堆栈（Stack）与堆（Heap）

栈是基于线程的，一个线程创建会分配一个默认1M大小的栈，由操作系统管理。

堆是基于进程的，一个进程分配一个堆。

------------

#### 进程与线程

进程：系统进行资源分配和调用的独立单位。

线程：CPU调度和分配的基本单位。

线程：
- Thread() 前台线程
- ThreadPool(线程池) 后台线程


------------

#### 多线程与异步

异步是最终目的，多线程只是我们实现异步的一种手段。

三种异步模式：
- 1，异步编程模型（APM）模式（IAsyncResult） 不推荐
- 2，基于事件的异步模式（EAP） 不推荐
- 3，基于任务的异步模式（TAP） 推荐
