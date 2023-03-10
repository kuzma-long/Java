# 基础

## 面向对象三大特性

> 华为，万得

- **封装**

  封装把⼀个对象的属性私有化，同时提供⼀些可以被外界访问的属性的⽅法。

- **继承**

  继承是使⽤已存在的类的定义作为基础创建新的类，新类的定义可以增加新的属性或新的方法，也可以继承父类的属性和方法。通过继承可以很方便地进行代码复用。

> 关于继承有以下三个要点：

1. ⼦类拥有⽗类对象所有的属性和⽅法（包括私有属性和私有⽅法），但是⽗类中的私有属性和⽅法⼦类是⽆法访问，只是拥有。
2. ⼦类可以拥有⾃⼰属性和⽅法，即⼦类可以对⽗类进⾏扩展。
3. ⼦类可以⽤⾃⼰的⽅式实现⽗类的⽅法。

- **多态**

  所谓多态就是指程序中定义的引⽤变量所指向的具体类型和通过该引⽤变量发出的⽅法调⽤在编程时并不确定，⽽是在程序运⾏期间才确定，即⼀个引⽤变量到底会指向哪个类的实例对象，该引⽤变量发出的⽅法调⽤到底是哪个类中实现的⽅法，必须在由程序运⾏期间才能决定。

  在 Java 中有两种形式可以实现多态：继承（多个⼦类对同⼀⽅法的重写）和接⼝（实现接⼝并覆盖接⼝中同⼀⽅法）。

## 重载和重写的区别？

> 华为，美团

- 重写（Override）：指在子类中重新定义一个与父类中同名、同参数的方法，但是方法体实现不同，这样当使用子类对象调用该方法时，将调用子类中的方法而不是父类中的方法。重写的目的是为了实现多态性。
- 重载（Overload）：指在一个类中定义多个同名方法，但是参数列表不同（个数、类型、顺序），这样当调用该方法时，编译器根据实参的个数和类型的不同，选择匹配的方法进行调用。重载的目的是为了方便调用。

## JAVA支持多继承吗，如果想要多继承怎么办？

> 美团

Java不支持多继承，也就是说一个类不能直接继承多个父类。这是由Java语言设计者的意图决定的，因为多继承可能导致类之间的复杂关系和命名冲突。

如果需要实现多继承的功能，可以使用接口（interface）来代替继承。一个类可以实现多个接口，这样就可以达到类似于多继承的效果。

## final关键字的作用

> 蔚来

- final关键字可以用来标志其修饰的类,方法和变量不可变。
- 当final修饰类时,该类不能被继承,例如java.lang.Math类就是一个final类,它不能被继承。
- final修饰的方法不能被重写,如果出于某些原因你不希望子类重写父类的某个方法,就可以用final关键字修饰这个方法。
- 当final用来修饰变量时,代表该变量不可被改变,一旦获得了初始值,该final变量的值就不能被重新赋值。
- final既可以修饰成员变量（包括类变量和实例变量）,也可以修饰局部变量、形参。

## Java 是引用传递还是值传递

> 百度，度小满

Java 中的参数传递是按值传递。这意味着方法调用时，传递给方法的是实际参数的副本而不是实际参数本身。

在 Java 中，基本类型的参数传递是按值传递，例如 int、float、double 等。当方法修改这些参数的值时，原始变量的值不会受到影响，因为方法仅仅是在自己的作用域中修改了传递的值的副本。

对于对象类型，引用传递的概念很容易被误解为按引用传递，但实际上 Java 中的对象类型也是按值传递的。一个对象的引用作为参数传递给方法时，实际上传递的是这个对象的引用（地址）的副本，而不是对象本身。因此，在方法中改变对象的状态会影响到调用方法的对象，因为它们引用的是同一个对象。但是，如果在方法中重新分配了对象的引用，那么原始对象的引用并不会改变。

## java权限修饰符有哪些、区别

> 上海银行苏州研发中心

1、private修饰的成员方法或者成员变量只能在本类中访问。

2、default修饰的成员方法或者成员变量只能被本包中的类访问。

3、protected修饰的成员方法或者成员变量只能被本包中的类和不同包中的子类访问。

4、public修饰的成员方法或者成员变量可以被所有包中的所有类访问。

| 权限修饰符 | 同一个类 | 同一个包 | 不同包的子类 | 不同包的非子类 |
| ---------- | -------- | -------- | ------------ | -------------- |
| Private    | √        |          |              |                |
| Default    | √        | √        |              |                |
| Protected  | √        | √        | √            |                |
| Public     | √        | √        | √            | √              |

## 静态变量和实例变量的区别？

> 宁波银行总行

在语法定义上的区别：静态变量前要加static关键字，而实例变量前则不加。
在程序运行时的区别：实例变量属于某个对象的属性，必须创建了实例对象，其中的实例变量才会被分配空间，才能使用这个实例变量。静态变量不属于某个实例对象，而是属于类，所以也称为类变量，只要程序加载了类的字节码，不用创建任何实例对象，静态变量就会被分配空间，静态变量就可以被使用了。总之，实例变量必须创建对象后才可以通过这个对象来使用，静态变量则可以直接使用类名来引用。

## java如何高效拷贝数组?

> 华为

Java中可以使用System.arraycopy()方法来高效拷贝数组，该方法可以将源数组中的元素复制到目标数组中，它的原型为：public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)。

## Object 类有哪些方法？

> 百度，zoom

**对象比较**：

- `public native int hashCode()` ：native 方法，用于返回对象的哈希码，主要使用在哈希表中，比如 JDK 中的 HashMap。
- `public boolean equals(Object obj)`：用于比较 2 个对象的内存地址是否相等，String 类对该方法进行了重写用于比较字符串的值是否相等。

**对象拷贝**：

- `protected native Object clone() throws CloneNotSupportedException`：native 方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为 true，x.clone().getClass() == x.getClass() 为 true。Object 本身没有实现 Cloneable 接口，所以不重写 clone 方法并且进行调用的话会发生 CloneNotSupportedException 异常。

**对象转字符串：**

- `public String toString()`：返回类的名字@实例的哈希码的 16 进制的字符串。建议 Object 所有的子类都重写这个方法。

**多线程调度：**

- `public final native void notify()`：native 方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
- `public final native void notifyAll()`：native 方法，并且不能重写。跟 notify 一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
- `public final native void wait(long timeout) throws InterruptedException`：native 方法，并且不能重写。暂停线程的执行。注意：sleep 方法没有释放锁，而 wait 方法释放了锁 。timeout 是等待时间。
- `public final void wait(long timeout, int nanos) throws InterruptedException`：多了 nanos 参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上 nanos 毫秒。
- `public final void wait() throws InterruptedException`：跟之前的 2 个 wait 方法一样，只不过该方法一直等待，没有超时时间这个概念

**反射：**

- `public final native Class<?> getClass()`：native 方法，用于返回当前运行时对象的 Class 对象，使用了 final 关键字修饰，故不允许子类重写。

**垃圾回收：**

- `protected void finalize() throws Throwable` ：通知垃圾收集器回收对象。

## 接口和抽象类有什么共同点和区别？

> 宁波银行总行，小米，百度，同花顺，阿里云，美团

共同点：

1. 都不能被实例化，只能被继承或者实现。
2. 都可以包含抽象方法，子类或者实现类必须实现这些抽象方法。
3. 都可以用来实现多态。

区别：

1. 实现方式

接口是一种完全抽象的类，它只包含方法的声明而没有方法的实现，通过实现接口，可以让一个类具有某些行为，而不需要继承任何类。而抽象类是一种特殊的类，它可以包含抽象方法和具体方法，但不能被实例化，只能被继承。

2. 方法类型

接口中的所有方法都是抽象方法，而抽象类中可以包含抽象方法和具体方法。抽象方法只有方法的声明而没有方法体，需要子类实现具体的方法体，而具体方法则有具体的实现。在 Java 8 中，接口可以包含默认方法和静态方法，这些方法有具体的实现。

3. 继承关系

一个类可以实现多个接口，但只能继承一个抽象类。接口是一种行为契约，实现类需要满足接口的规范，而抽象类是一种类之间的继承关系，可以定义一些通用的属性和方法，让子类继承并实现这些方法。

4. 构造函数

接口中不能包含构造函数，因为接口不能被实例化，而抽象类可以包含构造函数，用于初始化抽象类的成员变量。

5. 访问修饰符

接口中的方法默认是公共、抽象和不可变的，不能有访问修饰符和非抽象的方法体，而抽象类中可以包含具体方法和抽象方法，可以使用访问修饰符控制方法的访问权限。

## String中equals与==的区别

> 美团

1. 当使用"=="比较两个String类型的变量时，比较的是两个变量的引用是否相等，也就是它们是否指向同一个对象。如果是同一个对象，则返回true，否则返回false。
2. 当使用equals()比较两个String类型的变量时，比较的是两个变量的内容是否相等，也就是比较它们所代表的字符串是否相等。如果内容相等，则返回true，否则返回false。

## 为什么重写 equals() 时必须重写 hashCode() 方法？

> 百度

因为两个相等的对象的 `hashCode` 值必须是相等。也就是说如果 `equals` 方法判断两个对象是相等的，那这两个对象的 `hashCode` 值也要相等。

如果重写 `equals()` 时没有重写 `hashCode()` 方法的话就可能会导致 `equals` 方法判断是相等的两个对象，`hashCode` 值却不相等。

## String、StringBuffer、StringBuilder 的区别？

> zoom

**可变性**

`String` 是不可变的。

`StringBuilder` 与 `StringBuffer` 都继承自 `AbstractStringBuilder` 类，在 `AbstractStringBuilder` 中也是使用字符数组保存字符串，不过没有使用 `final` 和 `private` 关键字修饰，最关键的是这个 `AbstractStringBuilder` 类还提供了很多修改字符串的方法比如 `append` 方法。

**线程安全性**

`String` 中的对象是不可变的，也就可以理解为常量，线程安全。`AbstractStringBuilder` 是 `StringBuilder` 与 `StringBuffer` 的公共父类，定义了一些字符串的基本操作，如 `expandCapacity`、`append`、`insert`、`indexOf` 等公共方法。`StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。`StringBuilder` 并没有对方法进行加同步锁，所以是非线程安全的。

**性能**

每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。`StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 `StringBuilder` 相比使用 `StringBuffer` 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

**对于三者使用的总结：**

1. 操作少量的数据: 适用 `String`
2. 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`
3. 多线程操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`

## 如何去除代码中的很长的if-else语句？

> 阿里

长的if-else语句会让代码难以维护，可以通过以下几种方法来优化：

1.使用策略模式：将不同的分支逻辑封装到不同的策略类中，避免过长的if-else语句，让代码更加清晰。

2.使用工厂模式：将根据条件创建不同的对象的逻辑封装到工厂类中，避免if-else语句中的对象创建逻辑过于复杂。

3.使用映射表：将分支逻辑封装到一个Map中，通过Key-Value的方式来判断分支，可以有效避免冗长的if-else语句。

4.使用多态：将不同的分支逻辑封装到不同的类中，并让它们实现同一个接口，通过多态的方式来调用，可以有效避免if-else语句的臃肿。

5.使用注解：将不同的分支逻辑封装到不同的方法中，并使用注解来标记这些方法，通过反射的方式来调用相应的方法，可以避免过长的if-else语句。

通过使用以上优化方法，可以让代码更加简洁、易读、易维护。

## try-catch-finally 如何使用？

> 渤海银行总行

`try`块 ： 用于捕获异常。其后可接零个或多个 `catch` 块，如果没有 `catch` 块，则必须跟一个 `finally` 块。

`catch`块 ： 用于处理 try 捕获到的异常。

`finally` 块 ： 无论是否捕获或处理异常，`finally` 块里的语句都会被执行。当在 `try` 块或 `catch` 块中遇到 `return` 语句时，`finally` 语句块将在方法返回之前被执行。

**注意：不要在 finally 语句块中使用 return!** 当 try 语句和 finally 语句中都有 return 语句时，try 语句块中的 return 语句会被忽略。这是因为 try 语句中的 return 返回值会先被暂存在一个本地变量中，当执行到 finally 语句中的 return 之后，这个本地变量的值就变为了 finally 语句中的 return 返回值。

------

## finally 中的代码一定会执行吗？

> 渤海银行总行

不一定的！在某些情况下，finally 中的代码不会被执行。

就比如说 finally 之前虚拟机被终止运行的话，finally 中的代码就不会被执行。

另外，在以下 2 种特殊情况下，`finally` 块的代码也不会被执行：

1. 程序所在的线程死亡。
2. 关闭 CPU。

## 说一下JAVA中的泛型?

> 度小满，美团，阿里

Java中的泛型是一种类型参数化的机制，它可以让代码更加通用和灵活。在使用泛型时，可以在类、接口、方法中定义一些类型参数，这些类型参数可以在实例化时被具体类型所代替，从而实现类型安全的编程。

Java的泛型主要有以下几个方面的特点：

1. 类型安全：泛型可以让代码更加类型安全，避免了类型转换的错误。
2. 代码重用：泛型可以让代码更加通用，可以用同一套代码处理多种类型的数据，提高了代码的重用性。
3. 可读性：泛型可以让代码更加易读，因为在使用时可以清楚地知道每个变量的类型。
4. 限制性：泛型可以限制类型的范围，避免了不必要的类型转换和错误。

## JDK8 新特性有哪些？

> 邮储苏州研发，华为，唯品会

JDK 1.8是Java语言的一个重要版本，其中包含了许多新特性和改进。下面是JDK 1.8的一些主要新特性：

1. Lambda表达式：Lambda表达式是一种新的语法特性，它允许将代码作为数据进行传递，可以更加方便地处理集合和数组等数据结构。
2. Stream API：Stream API是一种新的集合处理方式，它可以方便地进行集合元素的筛选、排序、统计等操作，同时还可以并行处理数据，提高程序的执行效率。
3. 接口默认方法：JDK 1.8允许在接口中定义默认方法，这样可以减少代码的冗余，同时也方便了接口的扩展。
4. 方法引用：方法引用是一种新的语法特性，它可以通过方法名来引用一个已有的方法，避免了代码的重复编写。
5. 重复注解：JDK 1.8支持在同一个地方多次使用同一个注解，简化了代码的编写。
6. Optional类：Optional类是一个容器类，用于表示一个值可能存在或者不存在，可以避免null检查。
7. 时间日期API：JDK 1.8引入了新的时间日期API，提供了一种更加方便和易用的时间日期处理方式。
8. 并行数组操作：JDK 1.8提供了新的并行数组操作API，可以方便地对数组进行并行处理。

总之，JDK 1.8的新特性丰富了Java语言的功能和表现力，使得开发人员可以更加方便和高效地编写代码，并提高程序的性能和可维护性。

# 集合

## Java集合框架

> 华为，阿里云-3

Java集合框架包含两种类型的容器：Collection和Map。Collection接口用于存储对象，而Map接口用于存储键值对。

Java集合框架中的主要接口和类包括：

- Collection：接口，是List、Set和Queue接口的父接口。
  - List：接口，有序集合，可以包含重复的元素。
    - ArrayList：类，实现了List接口，用于创建动态数组。
    - LinkedList：类，实现了List接口，用于创建链表。
    - Vector：类，实现了List接口，线程安全，但效率较低。
    - Stack：类，继承自Vector类，用于创建栈。
  - Set：接口，无序集合，不包含重复的元素。
    - HashSet：类，实现了Set接口，用于创建哈希表。
    - TreeSet：类，实现了Set接口，用于创建有序集合。
  - Queue：接口，可以添加一个元素到队尾，或者删除队头的一个元素。
    - PriorityQueue：类，实现了Queue接口，用于创建优先队列。
- Map：接口，存储键值对。
  - HashMap：类，实现了Map接口，用于创建哈希表。
  - TreeMap：类，实现了Map接口，用于创建有序映射表。

## 说一说 PriorityQueue

> 华为

`PriorityQueue` 是在 JDK1.5 中被引入的, 其与 `Queue` 的区别在于元素出队顺序是与优先级相关的，即总是优先级最高的元素先出队。

这里列举其相关的一些要点：

- `PriorityQueue` 利用了二叉堆的数据结构来实现的，底层使用可变长的数组来存储数据
- `PriorityQueue` 通过堆元素的上浮和下沉，实现了在 O(logn) 的时间复杂度内插入元素和删除堆顶元素。
- `PriorityQueue` 是非线程安全的，且不支持存储 `NULL` 和 `non-comparable` 的对象。
- `PriorityQueue` 默认是小顶堆，但可以接收一个 `Comparator` 作为构造参数，从而来自定义元素优先级的先后。

## ArrayList扩容机制

> 德胧集团

添加元素时使用 ensureCapacityInternal() 方法来保证容量足够，如果不够时，需要使用 grow() 方法进行扩容，新容量的大小为 `oldCapacity + (oldCapacity >> 1)`，即 oldCapacity+oldCapacity/2。其中 oldCapacity >> 1 需要取整，所以新容量大约是旧容量的 1.5 倍左右。（oldCapacity 为偶数就是 1.5 倍，为奇数就是 1.5 倍-0.5）

扩容操作需要调用 `Arrays.copyOf()` 把原数组整个复制到新数组中，这个操作代价很高，因此最好在创建 ArrayList 对象时就指定大概的容量大小，减少扩容操作的次数。

```java
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}

private void ensureCapacityInternal(int minCapacity) {
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
    }
    ensureExplicitCapacity(minCapacity);
}

private void ensureExplicitCapacity(int minCapacity) {
    modCount++;
    // overflow-conscious code
    if (minCapacity - elementData.length > 0)
        grow(minCapacity);
}

private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}
```

## ArrayList 与 LinkedList 区别?

> 小米，字节，美团，华为，阿里

1. 数据结构：ArrayList基于动态数组实现，而LinkedList基于双向链表实现。
2. 随机访问效率：ArrayList的随机访问效率较高，因为它可以通过索引直接访问数组中的元素，而LinkedList的随机访问效率较低，因为它需要通过遍历链表来访问元素。
3. 插入和删除效率：LinkedList的插入和删除效率较高，因为它只需要修改相邻节点的指针，而ArrayList的插入和删除效率较低，因为它需要移动元素来填补空隙。
4. 内存空间占用：LinkedList的每个元素需要额外的空间来存储前驱和后继指针，因此它的内存空间占用比ArrayList大。

## HashMap 和 Hashtable 的区别

> 百度，华为，美团

1. 线程安全性：HashTable是线程安全的，而HashMap不是线程安全的。HashTable的方法都是同步的，因此在多线程环境下使用HashTable可以保证线程安全，但会导致性能降低。而HashMap则需要开发者自己保证线程安全，通常采用ConcurrentHashMap等线程安全的替代方案。
2. null值：HashTable不允许null作为key或value，否则会抛出NullPointerException。而HashMap则允许null作为key或value，但需要特别注意在遍历时可能会产生NullPointerException。
3. 效率：由于线程安全的实现机制不同，HashTable的性能通常比HashMap要差。HashTable的所有方法都是同步的，而HashMap的大部分方法都不需要同步，因此HashMap的性能通常比HashTable要好。
4. 迭代器：HashTable的迭代器（Enumeration）是不支持修改操作的，而HashMap的迭代器（Iterator）则支持修改操作。
5. 扩容机制：当存储空间不足时，HashTable会自动扩容为原来的两倍，而HashMap则会扩容为原来的两倍加一，这样可以更好地避免哈希冲突。此外，HashTable的初始容量为11，而HashMap的初始容量为16，这也导致了它们在扩容时处理方式的不同。
6. 继承关系：Hashtable是Dictionary类的子类，而HashMap继承自AbstractMap类。

## HashMap 和 TreeMap 区别

> 比亚迪，滴滴治理，浪潮，万得

#### 1）数据结构方面

HashMap是基于哈希表+数组来实现的，而TreeMap是基于红黑树实现的。

#### 2）效率方面

HashMap比TreeMap的性能更高。

HashMap的时间复杂度是O（1），它是通过哈希函数计算的哈希地址。

而TreeMap主要是保证数据平衡，时间复杂度是O（log2 n）。

#### 3）应用场景方面

HashMap是无序的，而TreeMap是有序的。

## HashMap 的底层数据结构

> 百度，小米，德胧集团，同花顺，快手，亚信

### JDK1.8 之前

JDK1.8 之前 `HashMap` 底层是 **数组和链表** 结合在一起使用也就是 **链表散列**。HashMap 通过 key 的 `hashcode` 经过扰动函数处理过后得到 hash 值，然后通过 `(n - 1) & hash` 判断当前元素存放的位置（这里的 n 指的是数组的长度），如果当前位置存在元素的话，就判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法解决冲突。

所谓扰动函数指的就是 HashMap 的 `hash` 方法。使用 `hash` 方法也就是扰动函数是为了防止一些实现比较差的 `hashCode()` 方法，换句话说使用扰动函数之后可以减少碰撞。

### JDK1.8 之后

相比于之前的版本， JDK1.8 之后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）时，会首先调用 `treeifyBin()`方法。这个方法会根据 HashMap 数组来决定是否转换为红黑树。只有当数组长度大于或者等于 64 的情况下，才会执行转换红黑树操作，以减少搜索时间。否则，就是只是执行 `resize()` 方法对数组扩容。

![jdk1.8之后的内部结构-HashMap](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/collection/jdk1.8_hashmap.png)

> TreeMap、TreeSet 以及 JDK1.8 之后的 HashMap 底层都用到了红黑树。红黑树就是为了解决二叉查找树的缺陷，因为二叉查找树在某些情况下会退化成一个线性结构。

## HashMap源码

> 快手

### put

#### 1.8

1. 如果table为空或者长度为0，则进行扩容操作。
2. 根据哈希值计算下标，如果对应下标正好没有存放数据，则直接插入即可。
3. 如果对应位置存在数据，且其hash值和key与插入的节点相等，那么直接进行替换。
4. 如果对应位置hash值和key与插入的节点不等
   - 如果该节点是红黑树节点，则插入红黑树
   - 如果是链表，遍历链表。
     - 如果遇到hash值和key与插入的节点相等，则覆盖链表节点。
     - 否则对该链表进行尾插法，插入后如果链表长度大于等于8，则需要调用treeifyBin把链表转换为红黑树。
5. 最后所有元素处理完成后，判断是否超过阈值`threshold`，超过则扩容。

```java
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}

/**
 * Implements Map.put and related methods.
 *
 * @param hash hash for key
 * @param key the key
 * @param value the value to put
 * @param onlyIfAbsent if true, don't change existing value
 * @param evict if false, the table is in creation mode.
 * @return previous value, or null if none
 */
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
               boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;
    // table未初始化或者长度为0，进行扩容
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;
    // (n - 1) & hash 确定元素存放在哪个桶中，桶为空，新生成结点放入桶中(此时，这个结点是放在数组中)
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    // 桶中已经存在元素（处理hash冲突）
    else {
        Node<K,V> e; K k;
        // 判断table[i]中的元素是否与插入的key一样，若相同那就直接使用插入的值p替换掉旧的值e。
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        // 判断插入的是否是红黑树节点
        else if (p instanceof TreeNode)
            // 放入树中
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        // 不是红黑树节点则说明为链表结点
        else {
            // 在链表最末插入结点
            for (int binCount = 0; ; ++binCount) {
                // 到达链表的尾部
                if ((e = p.next) == null) {
                    // 在尾部插入新结点
                    p.next = newNode(hash, key, value, null);
                    // 结点数量达到阈值(默认为 8 )，执行 treeifyBin 方法
                    // 这个方法会根据 HashMap 数组来决定是否转换为红黑树。
                    // 只有当数组长度大于或者等于 64 的情况下，才会执行转换红黑树操作，以减少搜索时间。否则，就是只是对数组扩容。
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        treeifyBin(tab, hash);
                    // 跳出循环
                    break;
                }
                // 判断链表中结点的key值与插入的元素的key值是否相等
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    // 相等，跳出循环
                    break;
                // 用于遍历桶中的链表，与前面的e = p.next组合，可以遍历链表
                p = e;
            }
        }
        // 表示在桶中找到key值、hash值与插入元素相等的结点
        if (e != null) { // existing mapping for key
            // 记录e的value
            V oldValue = e.value;
            // onlyIfAbsent为false或者旧值为null
            if (!onlyIfAbsent || oldValue == null)
                //用新值替换旧值
                e.value = value;
            // 访问后回调
            afterNodeAccess(e);
            // 返回旧值
            return oldValue;
        }
    }
    // 结构性修改
    ++modCount;
    // 实际大小大于阈值则扩容
    if (++size > threshold)
        resize();
    // 插入后回调
    afterNodeInsertion(evict);
    return null;
}
```

#### 1.7

- ① 如果定位到的数组位置没有元素 就直接插入。
- ② 如果定位到的数组位置有元素，遍历以这个元素为头结点的链表，依次和插入的 key 比较，如果 key 相同就直接覆盖，不同就采用头插法插入元素。

### get

![HashMap查找流程图](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/collection-14.png)

HashMap的查找就简单很多：

1. 使用扰动函数，获取新的哈希值
2. 计算数组下标，获取节点
3. 当前节点和key匹配，直接返回
4. 否则，当前节点是否为树节点，查找红黑树
5. 否则，遍历链表查找

```java
public V get(Object key) {
    Node<K,V> e;
    return (e = getNode(hash(key), key)) == null ? null : e.value;
}

/**
 * Implements Map.get and related methods.
 *
 * @param hash hash for key
 * @param key the key
 * @return the node, or null if none
 */
final Node<K,V> getNode(int hash, Object key) {
    Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
    if ((tab = table) != null && (n = tab.length) > 0 &&
        (first = tab[(n - 1) & hash]) != null) {
        // 数组元素相等
        if (first.hash == hash && // always check first node
            ((k = first.key) == key || (key != null && key.equals(k))))
            return first;
        // 桶中不止一个节点
        if ((e = first.next) != null) {
            // 在树中get
            if (first instanceof TreeNode)
                return ((TreeNode<K,V>)first).getTreeNode(hash, key);
            // 在链表中get
            do {
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    return e;
            } while ((e = e.next) != null);
        }
    }
    return null;
}
```

### hash

#### 1.8

```java
static final int hash(Object key) {
    int h;
    // key的hashCode和key的hashCode右移16位做异或运算
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```

#### 1.7

```java
static int hash(int h) {
    // This function ensures that hashCodes that differ only by
    // constant multiples at each bit position have a bounded
    // number of collisions (approximately 8 at default load factor).

    h ^= (h >>> 20) ^ (h >>> 12);
    return h ^ (h >>> 7) ^ (h >>> 4);
}
```

## 为什么HashMap链表转红黑树的阈值为8呢？

> 快手

红黑树节点的大小大概是普通节点大小的两倍，所以转红黑树，牺牲了空间换时间，更多的是一种兜底的策略，保证极端情况下的查找效率。

阈值为什么要选8呢？和统计学有关。理想情况下，使用随机哈希码，链表里的节点符合泊松分布，出现节点个数的概率是递减的，节点个数为8的情况，发生概率仅为`0.00000006`。

至于红黑树转回链表的阈值为什么是6，而不是8？是因为如果这个阈值也设置成8，假如发生碰撞，节点增减刚好在8附近，会发生链表和红黑树的不断转换，导致资源浪费。

## HashMap为什么用红黑树

> 百度

java8不是用红黑树来管理HashMap，而是在hash值相同的情况下（且重复数量大于8），用红黑树来管理数据。 红黑树相当于排序数据，可以自动的使用二分法进行定位，性能较高。一般情况下，hash值做的比较好的话基本上用不到红黑树。

红黑树牺牲了一些查找性能，但其本身并不是完全平衡的二叉树。因此插入删除操作效率略高于AVL树。

AVL树用于自平衡的计算牺牲了插入删除性能，但是因为最多只有一层的高度差，查询效率会高一些。

## HashMap 怎么扩容的？

> 字节tiktok

HashMap是基于数组+链表和红黑树实现的，但用于存放key值的桶数组的长度是固定的，由初始化参数确定。

那么，随着数据的插入数量增加以及负载因子的作用下，就需要扩容来存放更多的数据。而扩容中有一个非常重要的点，就是jdk1.8中的优化操作，可以不需要再重新计算每一个元素的哈希值。

因为HashMap的初始容量是2的次幂，扩容之后的长度是原来的二倍，新的容量也是2的次幂，所以，元素，要么在原位置，要么在原位置再移动2的次幂。

看下这张图，n为table的长度，图`a`表示扩容前的key1和key2两种key确定索引的位置，图`b`表示扩容后key1和key2两种key确定索引位置。

![扩容之后的索引计算](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/collection-25.png)

元素在重新计算hash之后，因为n变为2倍，那么n-1的mask范围在高位多1bit(红色)，因此新的index就会发生这样的变化：

![扩容位置变化](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/collection-26.png)

所以在扩容时，只需要看原来的hash值新增的那一位是0还是1就行了，是0的话索引没变，是1的化变成`原索引+oldCap`

## HashMap 为什么线程不安全？

> 阿里，字节tiktok

- 多线程下扩容死循环。JDK1.7 中的 HashMap 使用头插法插入元素，在多线程的环境下，扩容的时候有可能导致环形链表的出现，形成死循环。因此，JDK1.8 使用尾插法插入元素，在扩容时会保持链表元素原本的顺序，不会出现环形链表的问题。
- 多线程的 put 可能导致元素的丢失。多线程同时执行 put 操作，如果计算出来的索引位置是相同的，那会造成前一个 key 被后一个 key 覆盖，从而导致元素的丢失。此问题在 JDK 1.7 和 JDK 1.8 中都存在。
- put 和 get 并发时，可能导致 get 为 null。线程 1 执行 put 时，因为元素个数超出 threshold 而导致 rehash，线程 2 此时执行 get，有可能导致这个问题。这个问题在 JDK 1.7 和 JDK 1.8 中都存在。

## 如何设计线程安全的HashMap?

> 阿里，字节，蚂蚁

- 使用synchronized关键字来保证线程安全
- 使用Collections.synchronizedMap()方法将HashMap转换为线程安全的HashMap
- 使用java.util.concurrent包中的ConcurrentHashMap类来实现线程安全的HashMap。

## ConcurrentHashMap 和 Hashtable 的区别

> 小米，蚂蚁

1. 锁机制：ConcurrentHashMap引入了分段锁机制，不同的Segment上可以进行并发操作，这样可以降低锁的粒度，提高并发度；而Hashtable则是在每个方法上都加了同步锁，不同线程必须依次执行。
2. 空值：ConcurrentHashMap支持null键和null值，而Hashtable不支持。
3. 迭代器：ConcurrentHashMap的迭代器是弱一致性的，当迭代器创建后，如果对ConcurrentHashMap进行修改操作，可能会看到老的数据，因为迭代器只是获取到当前ConcurrentHashMap的快照，而Hashtable的迭代器是强一致性的。
4. 性能：在高并发的情况下，ConcurrentHashMap的性能优于Hashtable，因为ConcurrentHashMap引入了分段锁机制，可以提高并发度，而Hashtable的同步锁是对整个对象加锁，竞争激烈时性能较低。

**Hashtable** :

![Hashtable 的内部结构](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/collection/jdk1.7_hashmap.png)

**JDK1.7 的 ConcurrentHashMap** ：

![Java7 ConcurrentHashMap 存储结构](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/collection/java7_concurrenthashmap.png)

`ConcurrentHashMap` 是由 `Segment` 数组结构和 `HashEntry` 数组结构组成。

`Segment` 数组中的每个元素包含一个 `HashEntry` 数组，每个 `HashEntry` 数组属于链表结构。

**JDK1.8 的 ConcurrentHashMap** ：

![Java8 ConcurrentHashMap 存储结构](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/collection/java8_concurrenthashmap.png)

JDK1.8 的 `ConcurrentHashMap` 不再是 **Segment 数组 + HashEntry 数组 + 链表**，而是 **Node 数组 + 链表 / 红黑树**。不过，Node 只能用于链表的情况，红黑树的情况需要使用 **`TreeNode`**。当冲突链表达到一定长度时，链表会转换成红黑树。

## HashMap、HashTable、ConcurrentHashMap区别选择

> 唯品会

HashMap、Hashtable和ConcurrentHashMap都是Java中的Map接口的实现，用于存储key-value键值对。它们之间的主要区别如下：

1. 线程安全性：HashMap是非线程安全的，而Hashtable是线程安全的，ConcurrentHashMap也是线程安全的。
2. Null键和值的支持：HashMap支持null键和null值，Hashtable不支持null键和null值，ConcurrentHashMap支持null键和null值（但不推荐使用）。
3. 效率：HashMap的效率比Hashtable高，因为Hashtable每次访问时都要进行同步操作，而ConcurrentHashMap在大多数情况下比Hashtable的效率更高。
4. 迭代器：HashMap和ConcurrentHashMap都支持fail-fast迭代器，而Hashtable不支持。
5. 继承关系：Hashtable是Dictionary的子类，而HashMap和ConcurrentHashMap都是AbstractMap的子类。

基于上述区别，选择哪种Map实现应该根据具体的应用场景来决定。如果需要线程安全的Map，可以选择Hashtable或ConcurrentHashMap，如果对线程安全性要求不高，可以选择HashMap。如果需要高并发的环境，可以选择ConcurrentHashMap。如果应用场景需要支持null键和值，那么只能使用HashMap或ConcurrentHashMap。如果需要快速失败的迭代器，那么只能使用HashMap或ConcurrentHashMap。

## HashMap和ConcurrentHashMap区别

> 阿里云，美团

1. 线程安全性：HashMap不是线程安全的，而ConcurrentHashMap是线程安全的。
2. 并发度：HashMap是单线程的，ConcurrentHashMap支持多线程并发访问，其并发度是通过将数据分成多个Segment（段）来实现的，每个Segment类似于一个小的HashMap，其中的元素可以被多个线程同时访问。
3. 读写操作：HashMap在进行并发读写操作时可能会出现死循环或数据丢失的情况，而ConcurrentHashMap则可以支持并发读写操作而不会出现这种情况。
4. 性能：在多线程并发访问的情况下，ConcurrentHashMap的性能优于HashMap。

------

# I/O

## IO 流简介

> 阿里云

Java IO（Input/Output）是Java中用于处理输入输出流的API。在Java IO中，输入流是用于从文件或其他来源读取数据的流，输出流是用于将数据写入文件或其他目标的流。Java IO提供了一组类和接口，用于读写数据并管理资源。

Java IO分为字节流和字符流两种：

1. 字节流：用于处理字节数据，如文件、图片、二进制文件等，常用的类有InputStream和OutputStream。
2. 字符流：用于处理字符数据，如文本文件，常用的类有Reader和Writer。

在Java IO中还有一些其他常用的类和接口：

1. File：表示文件或文件夹的抽象路径名，可以对文件或文件夹进行操作。
2. BufferedReader/BufferedWriter：对字符流进行缓冲处理，可以提高读写的效率。
3. ByteArrayInputStream/ByteArrayOutputStream：对字节数组进行操作的流。
4. DataInputStream/DataOutputStream：用于读写基本数据类型，如int、double等。
5. ObjectInputStream/ObjectOutputStream：用于读写Java对象。
6. FileReader/FileWriter：用于读写字符文件。
7. RandomAccessFile：可以对文件进行随机访问，读写文件的任意位置。

在Java IO中还有一些高级特性，如NIO（New IO）和NIO.2（Java 7引入的新特性），它们提供了更高效的IO操作和更多的功能，如非阻塞IO、文件系统访问等。

## 字节流

### InputStream（字节输入流）

`InputStream`用于从源头（通常是文件）读取数据（字节信息）到内存中，`java.io.InputStream`抽象类是所有字节输入流的父类。

`InputStream` 常用方法 ：

- `read()` ：返回输入流中下一个字节的数据。返回的值介于 0 到 255 之间。如果未读取任何字节，则代码返回 `-1` ，表示文件结束。
- `read(byte b[ ])` : 从输入流中读取一些字节存储到数组 `b` 中。如果数组 `b` 的长度为零，则不读取。如果没有可用字节读取，返回 `-1`。如果有可用字节读取，则最多读取的字节数最多等于 `b.length` ， 返回读取的字节数。这个方法等价于 `read(b, 0, b.length)`。
- `read(byte b[], int off, int len)` ：在`read(byte b[ ])` 方法的基础上增加了 `off` 参数（偏移量）和 `len` 参数（要读取的最大字节数）。
- `skip(long n)` ：忽略输入流中的 n 个字节 ,返回实际忽略的字节数。
- `available()` ：返回输入流中可以读取的字节数。
- `close()` ：关闭输入流释放相关的系统资源。

从 Java 9 开始，`InputStream` 新增加了多个实用的方法：

- `readAllBytes()` ：读取输入流中的所有字节，返回字节数组。
- `readNBytes(byte[] b, int off, int len)` ：阻塞直到读取 `len` 个字节。
- `transferTo(OutputStream out)` ： 将所有字节从一个输入流传递到一个输出流。

`FileInputStream` 是一个比较常用的字节输入流对象，可直接指定文件路径，可以直接读取单字节数据，也可以读取至字节数组中。

`FileInputStream` 代码示例：

```java
try (InputStream fis = new FileInputStream("input.txt")) {
    System.out.println("Number of remaining bytes:"
            + fis.available());
    int content;
    long skip = fis.skip(2);
    System.out.println("The actual number of bytes skipped:" + skip);
    System.out.print("The content read from file:");
    while ((content = fis.read()) != -1) {
        System.out.print((char) content);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

输出：

```text
Number of remaining bytes:11
The actual number of bytes skipped:2
The content read from file:JavaGuide
```

不过，一般我们是不会直接单独使用 `FileInputStream` ，通常会配合 `BufferedInputStream`（字节缓冲输入流，后文会讲到）来使用。

像下面这段代码在我们的项目中就比较常见，我们通过 `readAllBytes()` 读取输入流所有字节并将其直接赋值给一个 `String` 对象。

```java
// 新建一个 BufferedInputStream 对象
BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream("input.txt"));
// 读取文件的内容并复制到 String 对象中
String result = new String(bufferedInputStream.readAllBytes());
System.out.println(result);
```

`DataInputStream` 用于读取指定类型数据，不能单独使用，必须结合 `FileInputStream` 。

```java
FileInputStream fileInputStream = new FileInputStream("input.txt");
//必须将fileInputStream作为构造参数才能使用
DataInputStream dataInputStream = new DataInputStream(fileInputStream);
//可以读取任意具体的类型数据
dataInputStream.readBoolean();
dataInputStream.readInt();
dataInputStream.readUTF();
```

`ObjectInputStream` 用于从输入流中读取 Java 对象（反序列化），`ObjectOutputStream` 用于将对象写入到输出流(序列化)。

```java
ObjectInputStream input = new ObjectInputStream(new FileInputStream("object.data"));
MyClass object = (MyClass) input.readObject();
input.close();
```

另外，用于序列化和反序列化的类必须实现 `Serializable` 接口，对象中如果有属性不想被序列化，使用 `transient` 修饰。

### OutputStream（字节输出流）

`OutputStream`用于将数据（字节信息）写入到目的地（通常是文件），`java.io.OutputStream`抽象类是所有字节输出流的父类。

`OutputStream` 常用方法 ：

- `write(int b)` ：将特定字节写入输出流。
- `write(byte b[ ])` : 将数组`b` 写入到输出流，等价于 `write(b, 0, b.length)` 。
- `write(byte[] b, int off, int len)` : 在`write(byte b[ ])` 方法的基础上增加了 `off` 参数（偏移量）和 `len` 参数（要读取的最大字节数）。
- `flush()` ：刷新此输出流并强制写出所有缓冲的输出字节。
- `close()` ：关闭输出流释放相关的系统资源。

`FileOutputStream` 是最常用的字节输出流对象，可直接指定文件路径，可以直接输出单字节数据，也可以输出指定的字节数组。

`FileOutputStream` 代码示例：

```java
try (FileOutputStream output = new FileOutputStream("output.txt")) {
    byte[] array = "JavaGuide".getBytes();
    output.write(array);
} catch (IOException e) {
    e.printStackTrace();
}
```

类似于 `FileInputStream`，`FileOutputStream` 通常也会配合 `BufferedOutputStream`（字节缓冲输出流，后文会讲到）来使用。

```java
FileOutputStream fileOutputStream = new FileOutputStream("output.txt");
BufferedOutputStream bos = new BufferedOutputStream(fileOutputStream)
```

**`DataOutputStream`** 用于写入指定类型数据，不能单独使用，必须结合 `FileOutputStream`

```java
// 输出流
FileOutputStream fileOutputStream = new FileOutputStream("out.txt");
DataOutputStream dataOutputStream = new DataOutputStream(fileOutputStream);
// 输出任意数据类型
dataOutputStream.writeBoolean(true);
dataOutputStream.writeByte(1);
```

`ObjectInputStream` 用于从输入流中读取 Java 对象（`ObjectInputStream`,反序列化），`ObjectOutputStream`将对象写入到输出流(`ObjectOutputStream`，序列化)。

```java
ObjectOutputStream output = new ObjectOutputStream(new FileOutputStream("file.txt")
Person person = new Person("Guide哥", "JavaGuide作者");
output.writeObject(person);
```

## 字符流

不管是文件读写还是网络发送接收，信息的最小存储单元都是字节。 **那为什么 I/O 流操作要分为字节流操作和字符流操作呢？**

个人认为主要有两点原因：

- 字符流是由 Java 虚拟机将字节转换得到的，这个过程还算是比较耗时。
- 如果我们不知道编码类型就很容易出现乱码问题。

乱码问题这个很容易就可以复现，我们只需要将上面提到的 `FileInputStream` 代码示例中的 `input.txt` 文件内容改为中文即可，原代码不需要改动。

输出：

```java
Number of remaining bytes:9
The actual number of bytes skipped:2
The content read from file:§å®¶å¥½
```

可以很明显地看到读取出来的内容已经变成了乱码。

因此，I/O 流就干脆提供了一个直接操作字符的接口，方便我们平时对字符进行流操作。如果音频文件、图片等媒体文件用字节流比较好，如果涉及到字符的话使用字符流比较好。

字符流默认采用的是 `Unicode` 编码，我们可以通过构造方法自定义编码。顺便分享一下之前遇到的笔试题：常用字符编码所占字节数？`utf8` :英文占 1 字节，中文占 3 字节，`unicode`：任何字符都占 2 个字节，`gbk`：英文占 1 字节，中文占 2 字节。

### Reader（字符输入流）

`Reader`用于从源头（通常是文件）读取数据（字符信息）到内存中，`java.io.Reader`抽象类是所有字符输入流的父类。

`Reader` 用于读取文本， `InputStream` 用于读取原始字节。

`Reader` 常用方法 ：

- `read()` : 从输入流读取一个字符。
- `read(char[] cbuf)` : 从输入流中读取一些字符，并将它们存储到字符数组 `cbuf`中，等价于 `read(cbuf, 0, cbuf.length)` 。
- `read(char[] cbuf, int off, int len)` ：在`read(char[] cbuf)` 方法的基础上增加了 `off` 参数（偏移量）和 `len` 参数（要读取的最大字节数）。
- `skip(long n)` ：忽略输入流中的 n 个字符 ,返回实际忽略的字符数。
- `close()` : 关闭输入流并释放相关的系统资源。

`InputStreamReader` 是字节流转换为字符流的桥梁，其子类 `FileReader` 是基于该基础上的封装，可以直接操作字符文件。

```java
// 字节流转换为字符流的桥梁
public class InputStreamReader extends Reader {
}
// 用于读取字符文件
public class FileReader extends InputStreamReader {
}
```

`FileReader` 代码示例：

```java
try (FileReader fileReader = new FileReader("input.txt");) {
    int content;
    long skip = fileReader.skip(3);
    System.out.println("The actual number of bytes skipped:" + skip);
    System.out.print("The content read from file:");
    while ((content = fileReader.read()) != -1) {
        System.out.print((char) content);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

输出：

```text
The actual number of bytes skipped:3
The content read from file:我是Guide。
```

### Writer（字符输出流）

`Writer`用于将数据（字符信息）写入到目的地（通常是文件），`java.io.Writer`抽象类是所有字节输出流的父类。

`Writer` 常用方法 ：

- `write(int c)` : 写入单个字符。
- `write(char[] cbuf)` ：写入字符数组 `cbuf`，等价于`write(cbuf, 0, cbuf.length)`。
- `write(char[] cbuf, int off, int len)` ：在`write(char[] cbuf)` 方法的基础上增加了 `off` 参数（偏移量）和 `len` 参数（要读取的最大字节数）。
- `write(String str)` ：写入字符串，等价于 `write(str, 0, str.length())` 。
- `write(String str, int off, int len)` ：在`write(String str)` 方法的基础上增加了 `off` 参数（偏移量）和 `len` 参数（要读取的最大字节数）。
- `append(CharSequence csq)` ：将指定的字符序列附加到指定的 `Writer` 对象并返回该 `Writer` 对象。
- `append(char c)` ：将指定的字符附加到指定的 `Writer` 对象并返回该 `Writer` 对象。
- `flush()` ：刷新此输出流并强制写出所有缓冲的输出字符。
- `close()`:关闭输出流释放相关的系统资源。

`OutputStreamWriter` 是字符流转换为字节流的桥梁，其子类 `FileWriter` 是基于该基础上的封装，可以直接将字符写入到文件。

```java
// 字符流转换为字节流的桥梁
public class OutputStreamWriter extends Writer {
}
// 用于写入字符到文件
public class FileWriter extends OutputStreamWriter {
}
```

`FileWriter` 代码示例：

```java
try (Writer output = new FileWriter("output.txt")) {
    output.write("你好，我是Guide。");
} catch (IOException e) {
    e.printStackTrace();
}
```

## 字节缓冲流

IO 操作是很消耗性能的，缓冲流将数据加载至缓冲区，一次性读取/写入多个字节，从而避免频繁的 IO 操作，提高流的传输效率。

字节缓冲流这里采用了装饰器模式来增强 `InputStream` 和`OutputStream`子类对象的功能。

举个例子，我们可以通过 `BufferedInputStream`（字节缓冲输入流）来增强 `FileInputStream` 的功能。

```java
// 新建一个 BufferedInputStream 对象
BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream("input.txt"));
```

字节流和字节缓冲流的性能差别主要体现在我们使用两者的时候都是调用 `write(int b)` 和 `read()` 这两个一次只读取一个字节的方法的时候。由于字节缓冲流内部有缓冲区（字节数组），因此，字节缓冲流会先将读取到的字节存放在缓存区，大幅减少 IO 次数，提高读取效率。

### BufferedInputStream（字节缓冲输入流）

`BufferedInputStream` 从源头（通常是文件）读取数据（字节信息）到内存的过程中不会一个字节一个字节的读取，而是会先将读取到的字节存放在缓存区，并从内部缓冲区中单独读取字节。这样大幅减少了 IO 次数，提高了读取效率。

`BufferedInputStream` 内部维护了一个缓冲区，这个缓冲区实际就是一个字节数组，通过阅读 `BufferedInputStream` 源码即可得到这个结论。

```java
public
class BufferedInputStream extends FilterInputStream {
    // 内部缓冲区数组
    protected volatile byte buf[];
    // 缓冲区的默认大小
    private static int DEFAULT_BUFFER_SIZE = 8192;
    // 使用默认的缓冲区大小
    public BufferedInputStream(InputStream in) {
        this(in, DEFAULT_BUFFER_SIZE);
    }
    // 自定义缓冲区大小
    public BufferedInputStream(InputStream in, int size) {
        super(in);
        if (size <= 0) {
            throw new IllegalArgumentException("Buffer size <= 0");
        }
        buf = new byte[size];
    }
}
```

缓冲区的大小默认为 **8192** 字节，当然了，你也可以通过 `BufferedInputStream(InputStream in, int size)` 这个构造方法来指定缓冲区的大小。

### BufferedOutputStream（字节缓冲输出流）

`BufferedOutputStream` 将数据（字节信息）写入到目的地（通常是文件）的过程中不会一个字节一个字节的写入，而是会先将要写入的字节存放在缓存区，并从内部缓冲区中单独写入字节。这样大幅减少了 IO 次数，提高了读取效率

```java
try (BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("output.txt"))) {
    byte[] array = "JavaGuide".getBytes();
    bos.write(array);
} catch (IOException e) {
    e.printStackTrace();
}
```

类似于 `BufferedInputStream` ，`BufferedOutputStream` 内部也维护了一个缓冲区，并且，这个缓存区的大小也是 **8192** 字节。

## 字符缓冲流

`BufferedReader` （字符缓冲输入流）和 `BufferedWriter`（字符缓冲输出流）类似于 `BufferedInputStream`（字节缓冲输入流）和`BufferedOutputStream`（字节缓冲输入流），内部都维护了一个字节数组作为缓冲区。不过，前者主要是用来操作字符信息。

## 打印流

下面这段代码大家经常使用吧？

```java
System.out.print("Hello！");
System.out.println("Hello！");
```

`System.out` 实际是用于获取一个 `PrintStream` 对象，`print`方法实际调用的是 `PrintStream` 对象的 `write` 方法。

`PrintStream` 属于字节打印流，与之对应的是 `PrintWriter` （字符打印流）。`PrintStream` 是 `OutputStream` 的子类，`PrintWriter` 是 `Writer` 的子类。

```java
public class PrintStream extends FilterOutputStream
    implements Appendable, Closeable {
}
public class PrintWriter extends Writer {
}
```

## 随机访问流

这里要介绍的随机访问流指的是支持随意跳转到文件的任意位置进行读写的 `RandomAccessFile` 。

`RandomAccessFile` 的构造方法如下，我们可以指定 `mode`（读写模式）。

```java
// openAndDelete 参数默认为 false 表示打开文件并且这个文件不会被删除
public RandomAccessFile(File file, String mode)
    throws FileNotFoundException {
    this(file, mode, false);
}
// 私有方法
private RandomAccessFile(File file, String mode, boolean openAndDelete)  throws FileNotFoundException{
  // 省略大部分代码
}
```

读写模式主要有下面四种：

- `r` : 只读模式。
- `rw`: 读写模式
- `rws`: 相对于 `rw`，`rws` 同步更新对“文件的内容”或“元数据”的修改到外部存储设备。
- `rwd` : 相对于 `rw`，`rwd` 同步更新对“文件的内容”的修改到外部存储设备。

文件内容指的是文件中实际保存的数据，元数据则是用来描述文件属性比如文件的大小信息、创建和修改时间。

`RandomAccessFile` 中有一个文件指针用来表示下一个将要被写入或者读取的字节所处的位置。我们可以通过 `RandomAccessFile` 的 `seek(long pos)` 方法来设置文件指针的偏移量（距文件开头 `pos` 个字节处）。如果想要获取文件指针当前的位置的话，可以使用 `getFilePointer()` 方法。

`RandomAccessFile` 代码示例：

```java
RandomAccessFile randomAccessFile = new RandomAccessFile(new File("input.txt"), "rw");
System.out.println("读取之前的偏移量：" + randomAccessFile.getFilePointer() + ",当前读取到的字符" + (char) randomAccessFile.read() + "，读取之后的偏移量：" + randomAccessFile.getFilePointer());
// 指针当前偏移量为 6
randomAccessFile.seek(6);
System.out.println("读取之前的偏移量：" + randomAccessFile.getFilePointer() + ",当前读取到的字符" + (char) randomAccessFile.read() + "，读取之后的偏移量：" + randomAccessFile.getFilePointer());
// 从偏移量 7 的位置开始往后写入字节数据
randomAccessFile.write(new byte[]{'H', 'I', 'J', 'K'});
// 指针当前偏移量为 0，回到起始位置
randomAccessFile.seek(0);
System.out.println("读取之前的偏移量：" + randomAccessFile.getFilePointer() + ",当前读取到的字符" + (char) randomAccessFile.read() + "，读取之后的偏移量：" + randomAccessFile.getFilePointer());
```

输出：

```text
读取之前的偏移量：0,当前读取到的字符A，读取之后的偏移量：1
读取之前的偏移量：6,当前读取到的字符G，读取之后的偏移量：7
读取之前的偏移量：0,当前读取到的字符A，读取之后的偏移量：1
```

`input.txt` 文件内容变为 `ABCDEFGHIJK` 。

`RandomAccessFile` 的 `write` 方法在写入对象的时候如果对应的位置已经有数据的话，会将其覆盖掉。

```java
RandomAccessFile randomAccessFile = new RandomAccessFile(new File("input.txt"), "rw");
randomAccessFile.write(new byte[]{'H', 'I', 'J', 'K'});
```

假设运行上面这段程序之前 `input.txt` 文件内容变为 `ABCD` ，运行之后则变为 `HIJK` 。

`RandomAccessFile` 比较常见的一个应用就是实现大文件的 **断点续传** 。何谓断点续传？简单来说就是上传文件中途暂停或失败（比如遇到网络问题）之后，不需要重新上传，只需要上传那些未成功上传的文件分片即可。分片（先将文件切分成多个文件分片）上传是断点续传的基础。

`RandomAccessFile` 可以帮助我们合并文件分片，示例代码如下：

![img](https://img-blog.csdnimg.cn/20210609164749122.png)

![img](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/image-20220428104115362.png)

`RandomAccessFile` 的实现依赖于 `FileDescriptor` (文件描述符) 和 `FileChannel` （内存映射文件）。

## Java IO设计模式

> 阿里云

### 装饰器模式

**装饰器（Decorator）模式** 可以在不改变原有对象的情况下拓展其功能。

装饰器模式通过组合替代继承来扩展原始类的功能，在一些继承关系比较复杂的场景（IO 这一场景各种类的继承关系就比较复杂）更加实用。

对于字节流来说， `FilterInputStream` （对应输入流）和`FilterOutputStream`（对应输出流）是装饰器模式的核心，分别用于增强 `InputStream` 和`OutputStream`子类对象的功能。

我们常见的`BufferedInputStream`(字节缓冲输入流)、`DataInputStream` 等等都是`FilterInputStream` 的子类，`BufferedOutputStream`（字节缓冲输出流）、`DataOutputStream`等等都是`FilterOutputStream`的子类。

举个例子，我们可以通过 `BufferedInputStream`（字节缓冲输入流）来增强 `FileInputStream` 的功能。

`BufferedInputStream` 构造函数如下：

```java
public BufferedInputStream(InputStream in) {
    this(in, DEFAULT_BUFFER_SIZE);
}

public BufferedInputStream(InputStream in, int size) {
    super(in);
    if (size <= 0) {
        throw new IllegalArgumentException("Buffer size <= 0");
    }
    buf = new byte[size];
}
```

可以看出，`BufferedInputStream` 的构造函数其中的一个参数就是 `InputStream` 。

`BufferedInputStream` 代码示例：

```java
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("input.txt"))) {
    int content;
    long skip = bis.skip(2);
    while ((content = bis.read()) != -1) {
        System.out.print((char) content);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

这个时候，你可以会想了：**为啥我们直接不弄一个`BufferedFileInputStream`（字符缓冲文件输入流）呢？**

```java
BufferedFileInputStream bfis = new BufferedFileInputStream("input.txt");
```

如果 `InputStream`的子类比较少的话，这样做是没问题的。不过， `InputStream`的子类实在太多，继承关系也太复杂了。如果我们为每一个子类都定制一个对应的缓冲输入流，那岂不是太麻烦了。

如果你对 IO 流比较熟悉的话，你会发现`ZipInputStream` 和`ZipOutputStream` 还可以分别增强 `BufferedInputStream` 和 `BufferedOutputStream` 的能力。

```java
BufferedInputStream bis = new BufferedInputStream(new FileInputStream(fileName));
ZipInputStream zis = new ZipInputStream(bis);

BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(fileName));
ZipOutputStream zipOut = new ZipOutputStream(bos);
```

`ZipInputStream` 和`ZipOutputStream` 分别继承自`InflaterInputStream` 和`DeflaterOutputStream`。

```java
public
class InflaterInputStream extends FilterInputStream {
}

public
class DeflaterOutputStream extends FilterOutputStream {
}

```

这也是装饰器模式很重要的一个特征，那就是可以对原始类嵌套使用多个装饰器。

为了实现这一效果，装饰器类需要跟原始类继承相同的抽象类或者实现相同的接口。上面介绍到的这些 IO 相关的装饰类和原始类共同的父类是 `InputStream` 和`OutputStream`。

对于字符流来说，`BufferedReader` 可以用来增加 `Reader` （字符输入流）子类的功能，`BufferedWriter` 可以用来增加 `Writer` （字符输出流）子类的功能。

```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(fileName), "UTF-8"));
```

IO 流中的装饰器模式应用的例子实在是太多了，不需要特意记忆，完全没必要哈！搞清了装饰器模式的核心之后，你在使用的时候自然就会知道哪些地方运用到了装饰器模式。

### 适配器模式

**适配器（Adapter Pattern）模式** 主要用于接口互不兼容的类的协调工作，你可以将其联想到我们日常经常使用的电源适配器。

适配器模式中存在被适配的对象或者类称为 **适配者(Adaptee)** ，作用于适配者的对象或者类称为**适配器(Adapter)** 。适配器分为对象适配器和类适配器。类适配器使用继承关系来实现，对象适配器使用组合关系来实现。

IO 流中的字符流和字节流的接口不同，它们之间可以协调工作就是基于适配器模式来做的，更准确点来说是对象适配器。通过适配器，我们可以将字节流对象适配成一个字符流对象，这样我们可以直接通过字节流对象来读取或者写入字符数据。

`InputStreamReader` 和 `OutputStreamWriter` 就是两个适配器(Adapter)， 同时，它们两个也是字节流和字符流之间的桥梁。`InputStreamReader` 使用 `StreamDecoder` （流解码器）对字节进行解码，**实现字节流到字符流的转换，** `OutputStreamWriter` 使用`StreamEncoder`（流编码器）对字符进行编码，实现字符流到字节流的转换。

`InputStream` 和 `OutputStream` 的子类是被适配者， `InputStreamReader` 和 `OutputStreamWriter`是适配器。

```java
// InputStreamReader 是适配器，FileInputStream 是被适配的类
InputStreamReader isr = new InputStreamReader(new FileInputStream(fileName), "UTF-8");
// BufferedReader 增强 InputStreamReader 的功能（装饰器模式）
BufferedReader bufferedReader = new BufferedReader(isr);
```

`java.io.InputStreamReader` 部分源码：

```java
public class InputStreamReader extends Reader {
	//用于解码的对象
	private final StreamDecoder sd;
    public InputStreamReader(InputStream in) {
        super(in);
        try {
            // 获取 StreamDecoder 对象
            sd = StreamDecoder.forInputStreamReader(in, this, (String)null);
        } catch (UnsupportedEncodingException e) {
            throw new Error(e);
        }
    }
    // 使用 StreamDecoder 对象做具体的读取工作
	public int read() throws IOException {
        return sd.read();
    }
}
```

`java.io.OutputStreamWriter` 部分源码：

```java
public class OutputStreamWriter extends Writer {
    // 用于编码的对象
    private final StreamEncoder se;
    public OutputStreamWriter(OutputStream out) {
        super(out);
        try {
           // 获取 StreamEncoder 对象
            se = StreamEncoder.forOutputStreamWriter(out, this, (String)null);
        } catch (UnsupportedEncodingException e) {
            throw new Error(e);
        }
    }
    // 使用 StreamEncoder 对象做具体的写入工作
    public void write(int c) throws IOException {
        se.write(c);
    }
}
```

**适配器模式和装饰器模式有什么区别呢？**

**装饰器模式** 更侧重于动态地增强原始类的功能，装饰器类需要跟原始类继承相同的抽象类或者实现相同的接口。并且，装饰器模式支持对原始类嵌套使用多个装饰器。

**适配器模式** 更侧重于让接口不兼容而不能交互的类可以一起工作，当我们调用适配器对应的方法时，适配器内部会调用适配者类或者和适配类相关的类的方法，这个过程透明的。就比如说 `StreamDecoder` （流解码器）和`StreamEncoder`（流编码器）就是分别基于 `InputStream` 和 `OutputStream` 来获取 `FileChannel`对象并调用对应的 `read` 方法和 `write` 方法进行字节数据的读取和写入。

```java
StreamDecoder(InputStream in, Object lock, CharsetDecoder dec) {
    // 省略大部分代码
    // 根据 InputStream 对象获取 FileChannel 对象
    ch = getChannel((FileInputStream)in);
}
```

适配器和适配者两者不需要继承相同的抽象类或者实现相同的接口。

另外，`FutrueTask` 类使用了适配器模式，`Executors` 的内部类 `RunnableAdapter` 实现属于适配器，用于将 `Runnable` 适配成 `Callable`。

`FutureTask`参数包含 `Runnable` 的一个构造方法：

```java
public FutureTask(Runnable runnable, V result) {
    // 调用 Executors 类的 callable 方法
    this.callable = Executors.callable(runnable, result);
    this.state = NEW;
}
```

`Executors`中对应的方法和适配器：

```java
// 实际调用的是 Executors 的内部类 RunnableAdapter 的构造方法
public static <T> Callable<T> callable(Runnable task, T result) {
    if (task == null)
        throw new NullPointerException();
    return new RunnableAdapter<T>(task, result);
}
// 适配器
static final class RunnableAdapter<T> implements Callable<T> {
    final Runnable task;
    final T result;
    RunnableAdapter(Runnable task, T result) {
        this.task = task;
        this.result = result;
    }
    public T call() {
        task.run();
        return result;
    }
}
```

### 工厂模式

工厂模式用于创建对象，NIO 中大量用到了工厂模式，比如 `Files` 类的 `newInputStream` 方法用于创建 `InputStream` 对象（静态工厂）、 `Paths` 类的 `get` 方法创建 `Path` 对象（静态工厂）、`ZipFileSystem` 类（`sun.nio`包下的类，属于 `java.nio` 相关的一些内部实现）的 `getPath` 的方法创建 `Path` 对象（简单工厂）。

```java
InputStream is Files.newInputStream(Paths.get(generatorLogoPath))
```

### 观察者模式

NIO 中的文件目录监听服务使用到了观察者模式。

NIO 中的文件目录监听服务基于 `WatchService` 接口和 `Watchable` 接口。`WatchService` 属于观察者，`Watchable` 属于被观察者。

`Watchable` 接口定义了一个用于将对象注册到 `WatchService`（监控服务） 并绑定监听事件的方法 `register` 。

```java
public interface Path
    extends Comparable<Path>, Iterable<Path>, Watchable{
}

public interface Watchable {
    WatchKey register(WatchService watcher,
                      WatchEvent.Kind<?>[] events,
                      WatchEvent.Modifier... modifiers)
        throws IOException;
}
```

`WatchService` 用于监听文件目录的变化，同一个 `WatchService` 对象能够监听多个文件目录。

```java
// 创建 WatchService 对象
WatchService watchService = FileSystems.getDefault().newWatchService();

// 初始化一个被监控文件夹的 Path 类:
Path path = Paths.get("workingDirectory");
// 将这个 path 对象注册到 WatchService（监控服务） 中去
WatchKey watchKey = path.register(
watchService, StandardWatchEventKinds...);
```

`Path` 类 `register` 方法的第二个参数 `events` （需要监听的事件）为可变长参数，也就是说我们可以同时监听多种事件。

```java
WatchKey register(WatchService watcher,
                  WatchEvent.Kind<?>... events)
    throws IOException;
```

常用的监听事件有 3 种：

- `StandardWatchEventKinds.ENTRY_CREATE` ：文件创建。
- `StandardWatchEventKinds.ENTRY_DELETE` : 文件删除。
- `StandardWatchEventKinds.ENTRY_MODIFY` : 文件修改。

`register` 方法返回 `WatchKey` 对象，通过`WatchKey` 对象可以获取事件的具体信息比如文件目录下是创建、删除还是修改了文件、创建、删除或者修改的文件的具体名称是什么。

```java
WatchKey key;
while ((key = watchService.take()) != null) {
    for (WatchEvent<?> event : key.pollEvents()) {
      // 可以调用 WatchEvent 对象的方法做一些事情比如输出事件的具体上下文信息
    }
    key.reset();
}
```

`WatchService` 内部是通过一个 daemon thread（守护线程）采用定期轮询的方式来检测文件的变化，简化后的源码如下所示。

```java
class PollingWatchService
    extends AbstractWatchService
{
    // 定义一个 daemon thread（守护线程）轮询检测文件变化
    private final ScheduledExecutorService scheduledExecutor;

    PollingWatchService() {
        scheduledExecutor = Executors
            .newSingleThreadScheduledExecutor(new ThreadFactory() {
                 @Override
                 public Thread newThread(Runnable r) {
                     Thread t = new Thread(r);
                     t.setDaemon(true);
                     return t;
                 }});
    }

  void enable(Set<? extends WatchEvent.Kind<?>> events, long period) {
    synchronized (this) {
      // 更新监听事件
      this.events = events;

        // 开启定期轮询
      Runnable thunk = new Runnable() { public void run() { poll(); }};
      this.poller = scheduledExecutor
        .scheduleAtFixedRate(thunk, period, period, TimeUnit.SECONDS);
    }
  }
}
```

## 同步/异步/阻塞/非阻塞 IO 的区别？

> 字节

同步和异步是通信机制，阻塞和非阻塞是调用状态。

同步 IO 是用户线程发起 IO 请求后需要等待或轮询内核 IO 操作完成后才能继续执行。异步 IO 是用户线程发起 IO 请求后可以继续执行，当内核 IO 操作完成后会通知用户线程，或调用用户线程注册的回调函数。

阻塞 IO 是 IO 操作需要彻底完成后才能返回用户空间 。非阻塞 IO 是 IO 操作调用后立即返回一个状态值，无需等 IO 操作彻底完成。

## BIO、NIO、AIO

> 比亚迪，英雄游戏，小米

### BIO (Blocking I/O)

**BIO 属于同步阻塞 IO 模型** 。

同步阻塞 IO 模型中，应用程序发起 read 调用后，会一直阻塞，直到内核把数据拷贝到用户空间。

![图源：《深入拆解Tomcat & Jetty》](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6a9e704af49b4380bb686f0c96d33b81~tplv-k3u1fbpfcp-watermark.image)

在客户端连接数量不高的情况下，是没问题的。但是，当面对十万甚至百万级连接的时候，传统的 BIO 模型是无能为力的。因此，我们需要一种更高效的 I/O 处理模型来应对更高的并发量。

### NIO (Non-blocking/New I/O)

> 阿里云

NIO（Non-blocking I/O）是Java中提供的一种非阻塞式I/O机制。与传统的I/O模型相比，NIO模型具有更高的并发性能和可扩展性。

NIO模型的核心是Channel和Buffer。Channel代表一个打开的连接，可以对Channel进行读写操作。Buffer是一个容器，存储数据并进行读写操作。

NIO模型的主要特点如下：

1. 非阻塞式I/O：NIO模型通过使用Selector选择器，实现了异步非阻塞I/O。当数据准备好时，可以直接进行读取，而不需要一直等待数据准备好。
2. Channel和Buffer：NIO模型使用Channel和Buffer来处理数据，Channel负责读写数据，Buffer负责缓存数据。
3. 事件驱动机制：NIO模型使用Selector选择器和事件驱动机制，只有当数据准备好时，才会进行读取操作。
4. 多路复用：NIO模型可以使用一个线程处理多个Channel，提高了并发性能和可扩展性。

NIO模型的基本工作流程如下：

1. 创建Channel：通过SocketChannel或ServerSocketChannel创建一个Channel。
2. 创建Buffer：创建一个Buffer对象，用于缓存数据。
3. 注册Channel：将Channel注册到Selector选择器中。
4. 处理事件：Selector选择器不断轮询所有注册的Channel，当数据准备好时，触发事件并进行处理。
5. 处理请求：根据事件类型，进行读写操作。

NIO模型是Java中常用的I/O模型之一，主要应用于高并发、高性能的网络编程场景，如服务器端的网络编程、网络游戏等。

### AIO (Asynchronous I/O)

AIO 是 JDK7 引入的异步非阻塞 IO。服务器实现模式为一个有效请求对应一个线程，客户端的 IO 请求都是由操作系统先完成 IO 操作后再通知服务器应用来直接使用准备好的数据。适用连接数目多且连接时间长的场景。

异步是指服务端线程接收到客户端管道后就交给底层处理IO通信，自己可以做其他事情，非阻塞是指客户端有数据才会处理，处理好再通知服务器。

实现方式包括通过 Future 的 `get` 方法进行阻塞式调用以及实现 CompletionHandler 接口，重写请求成功的回调方法 `completed` 和请求失败回调方法 `failed`。

AIO 也就是 NIO 2。Java 7 中引入了 NIO 的改进版 NIO 2,它是异步 IO 模型。

异步 IO 是基于事件和回调机制实现的，也就是应用操作之后会直接返回，不会堵塞在那里，当后台处理完成，操作系统会通知相应的线程进行后续的操作。

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3077e72a1af049559e81d18205b56fd7~tplv-k3u1fbpfcp-watermark.image)

目前来说 AIO 的应用还不是很广泛。Netty 之前也尝试使用过 AIO，不过又放弃了。这是因为，Netty 使用了 AIO 之后，在 Linux 系统上的性能并没有多少提升。

最后，来一张图，简单总结一下 Java 中的 BIO、NIO、AIO。

![](https://images.xiaozhuanlan.com/photo/2020/33b193457c928ae02217480f994814b6.png)

## NIO 使用了内核的什么功能

> 阿里云

NIO使用了操作系统内核的I/O多路复用机制，具体来说，就是通过select、poll、epoll这些系统调用实现的。这些系统调用可以监控多个Socket，当其中有一个或多个Socket可读或可写时，就会通知应用程序进行处理。

在Java中，NIO使用的是Selector类来实现I/O多路复用。Selector内部使用的是底层操作系统的I/O多路复用机制，通过注册Channel来监听事件，当事件发生时，Selector就会通知应用程序进行处理。

在Linux系统中，select和poll是早期的I/O多路复用机制，它们都需要将Socket的文件描述符添加到一个集合中，然后通过系统调用来监听这个集合中的Socket。但是随着Socket数量的增加，这种方式的效率会变得越来越低。

为了解决这个问题，Linux内核引入了epoll机制。epoll与select/poll的不同之处在于，它不需要将Socket添加到集合中，而是使用一个文件描述符来管理所有的Socket，从而提高了效率。因此，在高并发的场景中，使用epoll比select和poll更加高效。Java中的NIO也可以使用epoll机制，但是需要在Linux操作系统上运行，并且需要设置一些系统参数。

## IO多路复用select、poll 和 epoll 

> 英雄游戏，字节tiktok，oppo，腾讯IEG

**select** 函数监视的文件描述符分3类，分别是writefds、readfds、和exceptfds。调用后select函数会阻塞，直到有描述符就绪（有数据 可读、可写、或者有except），或者超时（timeout指定等待时间，如果立即返回设为null即可），函数返回。当select函数返回后，可以通过遍历fdset，来找到就绪的描述符。

select本质上是通过设置或者检查存放fd标志位的数据结构来进行下一步处理。这样所带来的缺点是：

- 单个进程所打开的FD是有限制的，通过 `FD_SETSIZE` 设置，默认1024 ;
- 每次调用 select，都需要把 fd 集合从用户态拷贝到内核态，这个开销在 fd 很多时会很大；

- 对 socket 扫描时是线性扫描，采用轮询的方法，效率较低（高并发）

**poll **本质上和select没有区别，它将用户传入的数组拷贝到内核空间，然后查询每个fd对应的设备状态，如果设备就绪则在设备等待队列中加入一项并继续遍历，如果遍历完所有fd后没有发现就绪设备，则挂起当前进程，直到设备就绪或者主动超时，被唤醒后它又要再次遍历fd。这个过程经历了多次无谓的遍历。

**它没有最大连接数的限制**，原因是它是基于链表来存储的，但是同样有缺点：

- 每次调用 poll ，都需要把 fd 集合从用户态拷贝到内核态，这个开销在 fd 很多时会很大；
- 对 socket 扫描是线性扫描，采用轮询的方法，效率较低（高并发时）

**epoll**

服务器启动以后，服务端会去调用epoll_create，创建一个epoll实例，epoll实例中包含两个数据

1、红黑树（为空）：rb_root 用来去记录需要被监听的FD

2、链表（为空）：list_head，用来存放已经就绪的FD

创建好了之后，会去调用epoll_ctl函数，此函数会将需要监听的数据添加到rb_root中去，并且对当前这些存在于红黑树的节点设置回调函数，当这些被监听的数据一旦准备完成，就会被调用，而调用的结果就是将红黑树的fd添加到list_head中去(但是此时并没有完成)

当第二步完成后，就会调用epoll_wait函数，这个函数会去校验是否有数据准备完毕（因为数据一旦准备就绪，就会被回调函数添加到list_head中），在等待了一段时间后(可以进行配置)，如果等够了超时时间，则返回没有数据，如果有，则进一步判断当前是什么事件，如果是建立连接时间，则调用accept() 接受客户端socket，拿到建立连接的socket，然后建立起来连接，如果是其他事件，则把数据进行写出。

![image-20230214111415766](E:\Typora\image-20230214111415766.png)

![image-20230214111528297](E:\Typora\image-20230214111528297.png)

## epoll的ET和LT

> 腾讯IEG

![image-20230215132942774](E:\Typora\image-20230215132942774.png)

# 其他

## 序列化和反序列化是什么？

> 美团

序列化是指将对象的状态转换为可存储或传输的形式的过程，而反序列化则是将序列化的数据转换回原始对象的过程。序列化可以将对象的状态保存到文件中，或者将对象的状态通过网络传输到另一台计算机。反序列化则可以从文件中读取序列化的数据，或者从网络中接收序列化的数据，并将其转换回原始对象。

## 常见序列化协议有哪些？

> zoom

JDK 自带的序列化方式一般不会用 ，因为序列化效率低并且存在安全问题。比较常用的序列化协议有 Hessian、Kryo、Protobuf、ProtoStuff，这些都是基于二进制的序列化协议。

像 JSON 和 XML 这种属于文本类序列化方式。虽然可读性比较好，但是性能较差，一般不会选择。

## 为什么不推荐使用 JDK 自带的序列化？

> zoom

我们很少或者说几乎不会直接使用 JDK 自带的序列化方式，主要原因有下面这些原因：

- **不支持跨语言调用** : 如果调用的是其他语言开发的服务的时候就不支持了。
- **性能差** ：相比于其他序列化框架性能更低，主要原因是序列化之后的字节数组体积较大，导致传输成本加大。
- **存在安全问题** ：序列化和反序列化本身并不存在问题。但当输入的反序列化的数据可被用户控制，那么攻击者即可通过构造恶意输入，让反序列化产生非预期的对象，在此过程中执行构造的任意代码。

## Java动态代理

> 小米，阿里云-2

相比于静态代理来说，动态代理更加灵活。我们不需要针对每个目标类都单独创建一个代理类，并且也不需要我们必须实现接口，我们可以直接代理实现类( *CGLIB 动态代理机制*)。

**从 JVM 角度来说，动态代理是在运行时动态生成类字节码，并加载到 JVM 中的。**

说到动态代理，Spring AOP、RPC 框架应该是两个不得不提的，它们的实现都依赖了动态代理。

**动态代理在我们日常开发中使用的相对较少，但是在框架中的几乎是必用的一门技术。学会了动态代理之后，对于我们理解和学习各种框架的原理也非常有帮助。**

就 Java 来说，动态代理的实现方式有很多种，比如 **JDK 动态代理**、**CGLIB 动态代理**等等。

### JDK 动态代理

JDK动态代理是Java中实现代理模式的一种方式，它可以在运行时动态生成代理类和代理对象，无需手动编写代理类的代码。通过JDK动态代理，可以将代理类和被代理类解耦，提高代码的可维护性和灵活性。

JDK动态代理是基于接口的代理方式，它要求被代理类必须实现一个或多个接口。JDK动态代理通过反射机制来生成代理类和代理对象，代理类实现了被代理接口，代理对象则是代理类的实例。代理对象的方法调用会委托给代理类的invoke方法处理，invoke方法会将请求转发给被代理对象，同时还可以在调用前后添加一些额外的逻辑，比如记录日志、验证参数等。

下面是使用JDK动态代理的步骤：

1. 定义一个接口，声明被代理类需要实现的方法。
2. 定义一个代理类，实现InvocationHandler接口，并重写invoke方法，在invoke方法中添加额外的逻辑。
3. 在代理类中创建一个被代理对象的引用，用来实现方法调用时的转发。
4. 在客户端代码中，通过Proxy类的newProxyInstance方法创建一个代理对象，同时将代理类和被代理对象传入。
5. 通过代理对象调用方法，代理类的invoke方法会被调用，并在调用前后添加额外的逻辑。

下面是一个使用JDK动态代理的例子：

```Java
// 定义一个接口
public interface HelloService {
    public void sayHello(String name);
}

// 实现InvocationHandler接口
public class HelloServiceHandler implements InvocationHandler {
    private Object target;
    
    public HelloServiceHandler(Object target) {
        this.target = target;
    }
    
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("before invoking method " + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("after invoking method " + method.getName());
        return result;
    }
}

// 客户端代码
public class Client {
    public static void main(String[] args) {
        HelloService target = new HelloServiceImpl();
        HelloServiceHandler handler = new HelloServiceHandler(target);
        HelloService proxy = (HelloService) Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), handler);
        proxy.sayHello("world");
    }
}
```

在这个例子中，HelloServiceImpl实现了Hello Service接口，HelloServiceHandler实现了InvocationHandler接口。在客户端代码中，通过Proxy类的newProxyInstance方法创建一个代理对象proxy，并将代理类和被代理对象传入。调用代理对象的sayHello方法，代理类的invoke方法会被调用，并在调用前后添加了额外的逻辑。

### CGLIB 动态代理

CGLIB是一个强大的第三方动态代理库，它可以在运行时生成一个目标类的子类，并重写目标类中的方法，以便在执行目标类的方法之前或之后执行一些其他逻辑。CGLIB动态代理主要用于创建没有接口的Java类的代理。

相比于Java标准库自带的动态代理API，CGLIB的优点在于：

- 支持创建没有接口的代理类
- 支持代理类方法上的任意参数和返回值类型
- 比JDK动态代理更快，因为它不需要通过反射调用代理方法

使用CGLIB动态代理的基本步骤如下：

1. 创建一个实现了MethodInterceptor接口的拦截器类，该拦截器负责在目标方法执行前后添加逻辑。
2. 创建一个Enhancer对象，并设置被代理类的类对象和拦截器。
3. 通过Enhancer对象的create方法创建代理对象。

下面是一个使用CGLIB动态代理的示例代码：

```Java
public class UserServiceInterceptor implements MethodInterceptor {
    @Override
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("执行目标方法之前的逻辑...");
        Object result = proxy.invokeSuper(obj, args);
        System.out.println("执行目标方法之后的逻辑...");
        return result;
    }
}

public class UserService {
    public void addUser(String name) {
        System.out.println("添加用户：" + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Enhancer enhancer = new Enhancer();
        enhancer.setSuperclass(UserService.class);
        enhancer.setCallback(new UserServiceInterceptor());
        UserService userService = (UserService) enhancer.create();
        userService.addUser("张三");
    }
}
```

在上述示例中，UserServiceInterceptor是一个实现了MethodInterceptor接口的拦截器类，它负责在目标方法执行前后添加逻辑。Main类中通过创建Enhancer对象，并设置被代理类的类对象和拦截器，最终通过Enhancer对象的create方法创建代理对象。当执行代理对象的addUser方法时，UserServiceInterceptor会先执行"执行目标方法之前的逻辑..."，然后调用目标方法，最后执行"执行目标方法之后的逻辑..."。

### JDK 动态代理和 CGLIB 动态代理对比

> 万得

**JDK 动态代理**

1. **Interface**：对于 JDK 动态代理，目标类需要实现一个 Interface。
2. **InvocationHandler**：InvocationHandler 是一个接口，可以通过实现这个接口，定义横切逻辑，再通过反射机制（invoke）调用目标类的代码，在次过程，可能包装逻辑，对目标方法进行前置后置处理。
3. **Proxy**：Proxy 利用 InvocationHandler 动态创建一个符合目标类实现的接口的实例，生成目标类的代理对象。

**CgLib 动态代理**

1. 使用 JDK 创建代理有一大限制，它只能为接口创建代理实例，而 CgLib 动态代理就没有这个限制。
2. CgLib 动态代理是使用字节码处理框架 **ASM**，其原理是通过字节码技术为一个类创建子类，并在子类中采用方法拦截的技术拦截所有父类方法的调用，顺势织入横切逻辑。
3. **CgLib** 创建的动态代理对象性能比 JDK 创建的动态代理对象的性能高不少，但是 CGLib 在创建代理对象时所花费的时间却比 JDK 多得多，所以对于单例的对象，因为无需频繁创建对象，用 CGLib 合适，反之，使用 JDK 方式要更为合适一些。同时，由于 CGLib 由于是采用动态创建子类的方法，对于 final 方法，无法进行代理。

区别：

1. **JDK 动态代理只能代理实现了接口的类或者直接代理接口，而 CGLIB 可以代理未实现任何接口的类。**另外， CGLIB 动态代理是通过生成一个被代理类的子类来拦截被代理类的方法调用，因此不能代理声明为 final 类型的类和方法。
2. 就二者的效率来说，大部分情况都是 JDK 动态代理更优秀，随着 JDK 版本的升级，这个优势更加明显。

------

## 动态代理与静态代理的区别

> 华为

动态代理与静态代理最大的区别在于实现方式不同，静态代理是在编译时就已经实现的代理，它是在程序运行前就已经存在的，它的实现需要实现一个接口，并且创建一个代理类。而动态代理是在运行时动态生成的，它的实现不需要实现接口，只需要指定一个实现类即可。

## Java反射机制及其实现原理

> 度小满，拼多多，万得，蚂蚁，阿里云，华为，阿里

Java反射机制是指程序在运行时能够动态地加载和使用类，获取类中的属性、方法、构造器等信息，并可以调用类中的方法、访问或修改类中的属性等。

反射机制的实现原理主要基于Java虚拟机（JVM）的Class对象和反射API中的相关类和接口，通过反射API中的Class、Method、Field、Constructor等类和接口，可以获取和操作Java程序运行时的各种元素。

具体实现原理如下：

1. 当Java程序被编译后，会生成相应的字节码文件，而每个字节码文件中都包含有一个或多个类的描述信息。
2. 在Java程序运行时，JVM会将这些字节码文件加载到内存中，同时生成对应的Class对象。
3. 通过反射API中的Class类的静态方法forName(String className)可以获取一个指定类的Class对象，从而可以通过该对象获取该类中的属性、方法、构造器等信息。
4. 通过反射API中的Method、Field、Constructor等类和接口，可以访问和操作类中的属性、方法、构造器等。

总之，Java反射机制基于Java虚拟机和反射API，可以在程序运行时获取和操作Java程序的各种元素，从而实现动态地加载和使用类。
