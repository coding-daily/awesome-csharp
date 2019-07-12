
![](https://raw.githubusercontent.com/coding-daily/awesome-csharp/master/logo-lg.png)

    C Sharp语法深入系列

### 目录

- .NET框架（CLR，BCL，FCL，CTS，CLS）
- C#基础语法（拆箱装箱、值类型与引用类型、String与字符操作、类抽象类接口委托事件、常量属性字段方法特性、抽象继承多态、泛型、关键字）
- 内存管理与GC垃圾回收 
- 内置数据结构（）
- 接口分析（IEnumerable、IEnumerable<T>、IComparable、IComparable<in T>、IFormattable、IFormatProvider、IConvertible、ICloneable、IEquatable<T>、IComparer<in T>、IEqualityComparer<in T>、IDisposable、IAsyncResult、ICollection<T>、IList<T>、IQueryable、IQueryProvider、IDictionary<TKey, TValue>、INotifyPropertyChanged、IEditableObject）
- Lambda、linq、SQL
- 进程与线程、多线程与异步
- 

------------

推荐阅读

[.NET面试题系列目录](https://www.cnblogs.com/haoyifei/p/5641115.html)

[.NET面试题解析](https://www.cnblogs.com/anding/p/5226343.html)

[DotNet进阶系列](https://www.cnblogs.com/yaopengfei/p/8853590.html)

------------


基类（抽象类）还是接口？

1、IS-A对比CAN-DO关系 

IS-A代表属于，CAN-DO代表能做某事。  
如果派生类型属于基类型，那么就用基类；如果建立的是能做的关系就用接口 

2、易用性 

对于开发人员，定义从基类派生的类型通常比实现接口的所有方法要容易的多。基类可提供大量功能，所以派生类型可能只需要稍加改动即可。而提供接口的话，派生类型则需要实现所有成员。 

3、一致性实现 

无论接口协定订立的多好，都无法保证所有人100%的实现它，而如果基类正确的话，以后根据需要稍加修改即可。 

4、版本控制 

向基类添加一个方法，派生类将继承该方法。而如果向接口添加新成员，则会强迫接口的继承者更改源代码并重新编译。   

-------------
什么是垃圾？简单理解就是没有被引用的对象。

最常见的一类非托管资源如文件句柄，窗口，网络连接，数据库连接，画刷，图标等。

这类资源，垃圾回收器在清理的时候会调用Object.Finalize()方法。默认情况下，方法是空的，对于非托管对象，需要在此方法中编写回收非托管资源的代码，以便垃圾回收器正确回收资源。

为了更方便的释放非托管资源，微软为非托管资源的回收专门定义了一个接口：IDisposable，接口中只包含一个Dispose()方法。任何包含非托管资源的类，都应该继承此接口，以确保非托管资源的正确释放。
在一个包含非托管资源的类中，资源释放的标准做法是：
- 继承IDisposable接口
- 实现Dispose()方法，在其中释放非托管资源，并将对象本身从垃圾回收器中移除（为了告诉垃圾回收器，此对象的资源我们已经自己释放了，它就没必要再对此对象进行回收了）；
- 实现类析构函数，在其中释放非托管资源。




