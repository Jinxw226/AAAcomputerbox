#Java类加载和实例化的执行顺序

![[Pasted image 20250903135651.png]]
1. 首先加载并执行父类的静态代码块  
2. 然后加载并执行子类的静态代码块  
3. 创建子类实例时,先执行父类的构造方法  
4. 最后执行子类的构造方法  
  
因此当执行new HelloB()时,输出顺序为:  
static A → static B → I'm A class → I'm B class