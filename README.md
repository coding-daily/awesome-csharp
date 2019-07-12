
![](https://raw.githubusercontent.com/coding-daily/awesome-csharp/master/logo-lg.png)

    C Sharp语法深入系列

### 目录

- .NET框架（CLR，BCL，FCL，CTS，CLS）
- C#基础语法（拆箱装箱、值类型与引用类型、String与字符操作、类抽象类接口委托事件、常量属性字段方法特性、抽象继承多态、泛型、关键字）
- 内存管理与GC垃圾回收
- 内置数据结构（）
- 接口分析（IEnumerable、IEnumerable<T>、IComparable、IComparable<in T>、IFormattable、IFormatProvider、IConvertible、ICloneable、IEquatable<T>、IComparer<in T>、IEqualityComparer<in T>、IDisposable、IAsyncResult、ICollection<T>、IList<T>、IQueryable、IQueryProvider、IDictionary<TKey, TValue>、INotifyPropertyChanged、IEditableObject）
- Lambda、linq、SQL
- 

基类还是接口？

1、IS-A对比CAN-DO关系 

IS-A代表属于，CAN-DO代表能做某事。  
如果派生类型属于基类型，那么就用基类；如果建立的是能做的关系就用接口 

2、易用性 

对于开发人员，定义从基类派生的类型通常比实现接口的所有方法要容易的多。基类可提供大量功能，所以派生类型可能只需要稍加改动即可。而提供接口的话，派生类型则需要实现所有成员。 

3、一致性实现 

无论接口协定订立的多好，都无法保证所有人100%的实现它，而如果基类正确的话，以后根据需要稍加修改即可。 

4、版本控制 

向基类添加一个方法，派生类将继承该方法。而如果向接口添加新成员，则会强迫接口的继承者更改源代码并重新编译。
