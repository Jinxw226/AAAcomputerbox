# 数组(Array)

- 特点：
```java
public class ArrayExample {  
    public static void main(String[] args) {  
        // 创建一个整数数组  
        int[] numbers = {1, 2, 3, 4, 5};  
 
        // 访问数组元素  
        for (int i = 0; i < numbers.length; i++) {  
            System.out.println("Element at index " + i + ": " + numbers[i]);  
        }  
    }  
}
```

- 固定大小：一旦创建，数组的大小不可更改。
- 快速访问：可以通过索引快速访问元素，时间复杂度为 O(1)。
- 同质性：数组只能存储同一类型的数据。
- 内存连续性：数组在内存中是连续存储的，适合需要频繁访问的场景。

- 使用场景:
	- 当需要存储固定数量的元素时。
	- 需要快速随机访问的场景。
- 优缺点:

- 优点：访问速度快，内存使用效率高。
缺点：大小固定，不支持动态扩展，插入和删除操作复杂。

# 列表(List)

```java
import java.util.ArrayList;  
import java.util.LinkedList;  
import java.util.List;  
 
public class ListExample {  
    public static void main(String[] args) {  
        // 使用 ArrayList  
        List<String> arrayList = new ArrayList<>();  
        arrayList.add("Apple");  
        arrayList.add("Banana");  
        arrayList.add("Cherry");  
 
        // 遍历 ArrayList  
        for (String fruit : arrayList) {  
            System.out.println(fruit);  
        }  
 
        // 使用 LinkedList  
        List<String> linkedList = new LinkedList<>();  
        linkedList.add("Dog");  
        linkedList.add("Cat");  
        linkedList.add("Rabbit");  
 
        // 遍历 LinkedList  
        for (String animal : linkedList) {  
            System.out.println(animal);  
        }  
    }  
}
```

- 实现类: ArrayList, LinkedList

- 特点:
	- 动态大小：可以根据需要增加或减少元素。
	- 接口：List 接口提供了多种操作方法，如添加、删除、查找等。
- ArrayList:
	- 基于动态数组实现。
	- 支持快速随机访问，时间复杂度为 O(1)。
	- 插入和删除操作较慢，尤其是在中间位置，时间复杂度为 O(n)。
- LinkedList:
	- 基于双向链表实现。
	- 插入和删除操作较快，时间复杂度为 O(1)（在已知位置的情况下）。
	- 随机访问速度较慢，时间复杂度为 O(n)。
- 使用场景:
	- ArrayList：需要频繁访问元素的场景。
	- LinkedList：需要频繁插入和删除元素的场景。
- 优缺点:
	- 优点：灵活性高，支持动态扩展。
	- 缺点：ArrayList 在插入和删除时性能较差，LinkedList 在随机访问时性能较差。

# 集合（Set）
```java
import java.util.HashSet;  
import java.util.LinkedHashSet;  
import java.util.Set;  
import java.util.TreeSet;  
 
public class SetExample {  
    public static void main(String[] args) {  
        // 使用 HashSet  
        Set<String> hashSet = new HashSet<>();  
        hashSet.add("Red");  
        hashSet.add("Green");  
        hashSet.add("Blue");  
        hashSet.add("Red"); // 重复元素不会被添加  
 
        System.out.println("HashSet: " + hashSet);  
 
        // 使用 LinkedHashSet  
        Set<String> linkedHashSet = new LinkedHashSet<>();  
        linkedHashSet.add("One");  
        linkedHashSet.add("Two");  
        linkedHashSet.add("Three");  
 
        System.out.println("LinkedHashSet: " + linkedHashSet);  
 
        // 使用 TreeSet  
        Set<String> treeSet = new TreeSet<>();  
        treeSet.add("Banana");  
        treeSet.add("Apple");  
        treeSet.add("Cherry");  
 
        System.out.println("TreeSet (sorted): " + treeSet);  
    }  
}
```

- 实现类: HashSet, LinkedHashSet, TreeSet

- 特点:
	- 不允许重复元素：集合中的元素是唯一的。
	- 接口：Set 接口提供了集合操作的方法。
- HashSet:
	- 基于哈希表实现。
	- 提供常数时间的性能用于基本操作（添加、删除、包含），时间复杂度为 O(1)。
	- 不保证元素的顺序。
- LinkedHashSet:
	- 继承自 HashSet，保持插入顺序。
	- 性能与 HashSet 相似。
- TreeSet:
	- 基于红黑树实现。
	- 元素按自然顺序排序，提供 O(log n) 的时间复杂度用于基本操作。
	- 支持范围查询和有序集合操作。
- 使用场景:
	- 需要存储唯一元素的场景。
	- 需要保持元素顺序或排序的场景。
- 优缺点:
	- 优点：自动去重，TreeSet 提供排序功能。
	- 缺点：HashSet 不保证顺序，TreeSet 性能较低。

# 映射（Map）

```java
import java.util.HashMap;  
import java.util.LinkedHashMap;  
import java.util.Map;  
import java.util.TreeMap;  
 
public class MapExample {  
    public static void main(String[] args) {  
        // 使用 HashMap  
        Map<String, Integer> hashMap = new HashMap<>();  
        hashMap.put("Alice", 30);  
        hashMap.put("Bob", 25);  
        hashMap.put("Charlie", 35);  
 
        System.out.println("HashMap: " + hashMap);  
 
        // 使用 LinkedHashMap  
        Map<String, Integer> linkedHashMap = new LinkedHashMap<>();  
        linkedHashMap.put("One", 1);  
        linkedHashMap.put("Two", 2);  
        linkedHashMap.put("Three", 3);  
 
        System.out.println("LinkedHashMap: " + linkedHashMap);  
 
        // 使用 TreeMap  
        Map<String, Integer> treeMap = new TreeMap<>();  
        treeMap.put("Banana", 1);  
        treeMap.put("Apple", 2);  
        treeMap.put("Cherry", 3);  
 
        System.out.println("TreeMap (sorted): " + treeMap);  
    }  
}
```

- 实现类: HashMap, LinkedHashMap, TreeMap

- 特点:
	- 存储键值对：每个键唯一，值可以重复。
	- 接口：Map 接口提供了键值对操作的方法。
- HashMap:
	- 基于哈希表实现。
	- 提供常数时间的性能用于基本操作，时间复杂度为 O(1)。
	- 不保证元素的顺序。
- LinkedHashMap:
	- 继承自 HashMap，保持插入顺序。
	- 性能与 HashMap 相似。
- TreeMap:
	- 基于红黑树实现。
	- 键按自然顺序排序，提供 O(log n) 的时间复杂度用于基本操作。
	- 支持范围查询和有序映射操作。
- 使用场景:
	- 需要存储键值对的场景。
	- 需要保持键的顺序或排序的场景。
- 优缺点:
	- 优点：快速查找，TreeMap 提供排序功能。
	- 缺点：HashMap 不保证顺序，TreeMap 性能较低。

# 队列（Queue）
```java
import java.util.LinkedList;  
import java.util.Queue;  
 
public class QueueExample {  
    public static void main(String[] args) {  
        // 使用 LinkedList 作为队列  
        Queue<String> queue = new LinkedList<>();  
        queue.add("First");  
        queue.add("Second");  
        queue.add("Third");  
 
        // 遍历队列  
        while (!queue.isEmpty()) {  
            System.out.println("Processing: " + queue.poll());  
        }  
    }  
}
```

- 实现类: LinkedList, PriorityQueue, ArrayDeque

- 特点:
	- 先进先出（FIFO）：元素按照插入顺序处理。
	- 接口：Queue 接口提供了队列操作的方法。
- LinkedList:
	- 可以作为队列使用，支持动态大小。
	- 插入和删除操作较快，时间复杂度为 O(1)。
- PriorityQueue:
	- 根据优先级排序元素。
	- 不保证元素的插入顺序，时间复杂度为 O(log n)。
- ArrayDeque:
	- 双端队列，支持在两端插入和删除。
	- 性能优于 LinkedList。
- 使用场景:
	- 需要按照顺序处理元素的场景。
	- 需要优先级处理的场景。
- 优缺点:
	- 优点：灵活性高，支持动态扩展。
	- 缺点：PriorityQueue 不保证顺序。

# 栈（Stack）
```java
import java.util.Stack;  
 
public class StackExample {  
    public static void main(String[] args) {  
        // 使用 Stack  
        Stack<String> stack = new Stack<>();  
        stack.push("First");  
        stack.push("Second");  
        stack.push("Third");  
 
        // 遍历栈  
        while (!stack.isEmpty()) {  
            System.out.println("Popping: " + stack.pop());  
        }  
    }  
}
```

- 实现类: Stack, ArrayDeque

- 特点:
	- 后进先出（LIFO）：最后插入的元素最先被处理。
	- 接口：Stack 类提供了基本的栈操作。
- Stack:
	- 继承自 Vector，提供基本的栈操作。
	- 不推荐使用，因其继承自 Vector，性能较低。
- ArrayDeque:
	- 可以作为栈使用，性能更好。
	- 支持动态大小。
- 使用场景:
	- 需要后进先出处理的场景，如函数调用、表达式求值等。
- 优缺点:
	- 优点：简单易用，支持动态扩展。
	- 缺点：Stack 性能较低。

# 其他结构

- 链表 (Linked List):
	- 自定义实现，支持动态大小和快速插入/删除。
	- 适合需要频繁插入和删除的场景。
- 图 (Graph):
	- 自定义实现，通常使用邻接表或邻接矩阵表示。
	- 适合表示复杂关系的场景，如社交网络、地图等。
- 树 (Tree):
	- 自定义实现，常见的有二叉树、红黑树、AVL树等。
	- 适合需要分层结构的场景，如文件系统、数据库索引等。
