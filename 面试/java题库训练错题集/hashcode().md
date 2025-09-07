#hashcode 

**hashcode()** 方法是 Java 中用于生成对象哈希码的函数。哈希码是一个整数值，通过哈希函数计算得出，用于在哈希表中快速查找对象的位置。

hashcode() 的作用

哈希码的主要作用是提高查找效率。在哈希表中，哈希码用于确定对象的存储位置，从而加快查找速度。例如，在存储大量数据时，使用哈希码可以避免逐个比较所有数据，从而显著提高性能。

hashcode() 和 equals() 的关系

在 Java 中，**hashcode()** 和 **equals()** 方法密切相关。一般来说：

1. 如果两个对象的 **equals()** 方法返回 true，那么它们的 **hashcode()** 也应该相同。
2. 如果两个对象的 **hashcode()** 相同，它们的 **equals()** 方法不一定返回 true。

因此，重写 **equals()** 方法时，通常也需要重写 **hashcode()** 方法，以确保对象在哈希表中的正确行为。

hashcode() 的实现

Java 中的 **hashcode()** 方法可以根据对象的不同类型有不同的实现。例如，字符串的哈希码可以通过以下公式计算：

`s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]`

其中，_s[i]_ 是字符串的第 _i_ 个字符的 ASCII 码，_n_ 是字符串的长度，_^_ 表示求幂。空字符串的哈希值为 0。

以下是一个简单的示例，展示如何获取字符串的哈希码：

```java
public class Test {
	public static void main(String args[]) {
		String str = new String("www.runoob.com");
		System.out.println("字符串的哈希码为: " + str.hashCode());
	}
}
```

输出结果为：
字符串的哈希码为: 321005537