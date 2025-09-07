#stream流
Stream流极大地简化了对集合的操作，提升了代码的执行效率。Stream流适用于多种场景，以下是一些常见的应用场景：

1. 集合元素的拼接
在处理集合时，常常需要将集合中的某个属性值拼接成一个字符串。使用Stream流可以简化这一过程。例如，将List中的某个属性值取出并拼接成字符串：
```java
List<Map<String, Object>> mapList = ...;
String ids = mapList.stream()
	.map(item -> item.get("id").toString())
	.collect(Collectors.joining(","));
```
这种方法避免了传统for循环的繁琐步骤。

2. 获取集合中的最大值或最小值
使用Stream流可以方便地获取集合中的最大值或最小值。例如，获取List中的最大值：
```java
List<Map<String, Integer>> mapList = ...;
Integer maxScore = mapList.stream()
	.map(t -> t.get("score"))
	.reduce(0, Integer::max);
```

3. 集合的过滤和映射

Stream流提供了filter和map方法，可以方便地对集合进行过滤和映射。例如，筛选出所有专业为计算机科学的学生姓名：

```java
List<Student> students = ...;
List<String> names = students.stream()
	.filter(student -> "计算机科学".equals(student.getMajor()))
	.map(Student::getName)
	.collect(Collectors.toList());
```

这种方法简化了对集合的操作。

4. 集合的分组

Stream流提供了Collectors.groupingBy方法，可以方便地对集合进行分组。例如，按学校对学生进行分组：

```java
List<Student> students = ...;
Map<String, List<Student>> groups = students.stream()
	.collect(Collectors.groupingBy(Student::getSchool));
```
这种方法类似于SQL中的GROUP BY操作。

5. 并行处理

Stream流支持并行处理，可以充分利用多核处理器的优势。例如，使用parallelStream方法启动并行流式处理：

```java
List<Student> students = ...;
students.parallelStream()
	.filter(student -> student.getAge() >= 18)
	.forEach(System.out::println);
```