#ThreadLocal

- ThreadLocal 并不是一个Thread，而是Thread的局部变量。
- ThreadLocal为每个线程提供一份单独的存储空间，具有线程隔离的效果，不同的线程之间不会相互干扰。
![[ThreadLocal.png]]- 常见方法：
    -`public void set(T value)` 设置当前线程的线程局部变量的值
    - `public T get()` 返回当前线程所对应的线程局部变量的值
    - `public void remove()` 移除当前线程的线程局部变量


> [!NOTE]
> 在同一个线程/同一个请求中，进行数据共享就可以使用 ThreadLocal。