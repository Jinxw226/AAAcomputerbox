![[Pasted image 20250903141255.png]]
选项A正确：LinkedBlockingQueue是一个可选有界队列，确实不允许null值。当创建时不指定容量时为无界队列，指定容量时则为有界队列。且它的add()、put()等方法都会对null值进行检查并抛出NullPointerException。  
  
选项C正确：PriorityQueue是基于优先级堆的无界优先级队列，不允许插入null值，其入队(offer/add)和出队(poll/remove)操作的时间复杂度确实是O(log(n))，因为需要维护堆的特性。  
  
分析错误选项：  
  
选项B错误：LinkedBlockingQueue是线程==安全==的阻塞队列，它的操作都是通过ReentrantLock来保证线程安全。而PriorityQueue是==非线程安全==的。  
  
选项D错误：==ConcurrentLinkedQueue==遵循==FIFO==原则，但PriorityQueue不遵循FIFO原则。PriorityQueue是按照优先级来确定出队顺序，每次出队都会取出优先级最高（通常是最小值）的元素，而不是先进先出。