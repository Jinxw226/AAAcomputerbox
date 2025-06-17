#throw #throws 
thow和throws适用于异常处理的两个关键字，他们在功能和使用场景上有所不同
## throw关键字
**throw** 关键字用于在程序中手动抛出一个异常。当某些条件不符合业务逻辑要求时，可以使用 **throw** 抛出一个异常。例如：
```java
public void checkAge(int age) {
	if (age < 0) {
		throw new IllegalArgumentException("年龄不能为负数");
	}
}
```
在这个例子中，如果年龄小于 0，就会抛出一个 _IllegalArgumentException_ 异常[1](https://blog.csdn.net/Y2000104/article/details/135356748)[2](https://blog.csdn.net/meism5/article/details/90414147)。

## throws 关键字
**throws** 关键字用于指定方法可能抛出的异常。它标识了哪些异常可以传递到方法的调用者，需要调用者进行相应的处理。例如：

```java
public void readFile() throws IOException {
	// 异常处理逻辑
}
```

在这个例子中，_readFile_ 方法声明它可能抛出 _IOException_ 异常[1](https://blog.csdn.net/Y2000104/article/details/135356748)[3](https://www.cainiaojc.com/java/java-throw-throws.html)。

区别与联系
- **throw** 关键字用于在方法内抛出异常，而 **throws** 关键字是在方法声明中指定可能抛出的异常。
- **throw** 关键字只能抛出一个异常对象，而 **throws** 关键字可以同时指定多个异常。
- **throw** 关键字会中断当前的执行流程，寻找合适的异常处理机制，而 **throws** 关键字将异常传递给调用者来处理