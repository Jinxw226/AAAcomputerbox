好的，我们来分析这道关于Java7的单选题。

**正确答案是：D. SimpleDateFormat对象是线程不安全的**

---

### 选项逐条解析

#### **A. ConcurrentHashMap使用Synchronized关键字保证线程安全**
*   **说法错误**。
*   **解析**：在Java 7中，`ConcurrentHashMap` 的实现使用了一种叫做**分段锁（Segment Locking）** 的机制。它将整个Map分成多个段（Segment），每个段独立加锁。这样，不同的线程可以同时访问不同的段，从而极大地提高了并发性能。它**并没有**直接使用 `synchronized` 关键字来锁住整个对象，这是它与 `Hashtable` 最核心的区别（`Hashtable` 是使用 `synchronized` 方法保证线程安全的）。
*   **考点**：`ConcurrentHashMap` 在Java 7中的底层实现原理。

#### **B. HashMap实现了Collection接口**
*   **说法错误**。
*   **解析**：这是对Java集合框架层次的常见误解。
    *   `Collection` 接口的直接继承者是 `List`, `Set`, `Queue` 等接口，它代表的是一个对象的**集合**。
    *   `HashMap` 实现的是 `Map` 接口。`Map` 接口存储的是**键值对（Key-Value Pairs）**，它与 `Collection` 接口是**平级**的关系，都属于集合框架的根接口，但两者没有继承关系。
    *   你可以通过 `HashMap` 的 `keySet()`, `values()`, `entrySet()` 方法获取其键、值或键值对的 `Collection` 视图，但 `HashMap` 本身不是一个 `Collection`。
*   **考点**：Java集合框架的整体架构，`Map` 和 `Collection` 的区别。

#### **C. Arrays.asList方法返回java.util.ArrayList对象**
*   **说法错误**。
*   **解析**：这是一个非常经典的陷阱。`Arrays.asList(T... a)` 方法返回的确实是一个 `List` 对象，但它是一个**固定大小**的列表，其底层实现是 `Arrays` 类的一个私有静态内部类（`java.util.Arrays$ArrayList`），**而不是我们常用的 `java.util.ArrayList`**。
    *   这个内部类基于原始数组，所以它**不支持**添加（`add`）或删除（`remove`）操作，调用这些方法会抛出 `UnsupportedOperationException`。它只支持修改（`set`）和查询。
    *   真正的 `java.util.ArrayList` 是动态数组，支持增删改查。
*   **考点**：`Arrays.asList` 方法的返回值类型及其特性（固定大小列表）。

#### **D. SimpleDateFormat对象是线程不安全的**
*   **说法正确**。
*   **解析**：这是Java中一个非常著名的问题。`SimpleDateFormat` 类内部使用了一个 `Calendar` 对象来进行日期解析和格式化操作。这个 `Calendar` 对象的状态会在方法调用中被修改。如果多个线程共享同一个 `SimpleDateFormat` 实例，它们会并发地修改这个共享的 `Calendar` 对象的状态，从而导致**数据不一致、解析错误甚至程序崩溃**。
    *   **解决方案**：
        1.  **局部变量**：每次使用时在方法内部创建新的 `SimpleDateFormat`（不共享）。
        2.  **同步（Synchronized）**：使用 `synchronized` 关键字包装 `format`/`parse` 方法调用（性能差）。
        3.  **ThreadLocal**：为每个线程分配一个独立的实例（最佳方案）。
        4.  **使用新的DateTime API**（Java 8+）：`DateTimeFormatter` 是**线程安全**的，应作为新的首选。
*   **考点**：`SimpleDateFormat` 的线程安全性问题，这是多线程编程中的一个经典坑。

---

### 题目考查的知识点总结

这道题综合考查了Java 7中几个**非常重要且易错**的基础知识点：

1.  **并发集合的实现原理**：特别是 `ConcurrentHashMap` 与 `Hashtable` 在线程安全实现上的区别（分段锁 vs. 全局锁）。
2.  **集合框架的体系结构**：清晰区分 `Collection` 和 `Map` 两大体系。
3.  **常用工具类的细节**：`Arrays.asList` 方法返回的是一个不可变的视图列表，而非标准 `ArrayList`。
4.  **线程安全性与日期处理**：`SimpleDateFormat` 是典型的非线程安全类，这是编写多线程程序时必须牢记的一点。

这些知识点都是Java开发中的核心基础，无论是面试还是实际开发中都经常遇到。