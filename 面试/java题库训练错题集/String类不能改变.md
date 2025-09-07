```java
public class Example{
	String str = new String("good");
	char[] ch = {'a' , 'b', 'c'};
	public static void main(String args[]){
		Example ex = new Example();
		ex.change(ex.str,ex.ch);
		System.out.print(ex.str + " and ");
		System.out.print(ex.ch);
	}
	public void change(String str,char ch[ ]){
		str = "test ok";
		ch[0] = 'g';
	}
}
```

输出为：good and gbc

1. 关于字符串str:  
- 在change方法中,参数str被赋值为"test ok"  
- 但这种改变不会影响原始的ex.str  
- 因为String是不可变类,方法中的str是一个新的引用  
- 所以原始的ex.str仍然保持"good"不变  
  
2. 关于字符数组ch:  
- 在change方法中,修改了ch[0]为'g'  
- 这个改变会影响到原始数组  
- 因为数组是引用类型,方法参数得到的是原始数组的引用  
- 所以原始数组的第一个字符被改为'g'

