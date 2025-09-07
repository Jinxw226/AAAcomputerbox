#executeUpdate 
![[Pasted image 20250903132546.png]]

executeUpdate()方法用于执行INSERT、UPDATE或DELETE等DML语句,其返回值表示受影响的行数。在这个例子中,成功插入一条记录,所以返回值为1。

分析各选项:  
B选项(1)正确:因为该INSERT语句成功插入了一条记录,所以影响了1行数据,返回值为1。  
  
A选项(0)错误:如果SQL语句执行失败或没有记录受影响才会返回0,但题目明确说明"成功插入数据",所以不会返回0。  
  
C选项(true)错误:executeUpdate()方法返回的是一个int类型的值,表示受影响的行数,而不是布尔类型。  
  
D选项(FALSE)错误:同C选项,executeUpdate()返回的是整数类型,不是布尔值。  
  
补充说明:  
- executeUpdate()方法返回值的具体含义:  
- 对于INSERT语句:返回新增的记录数  
- 对于UPDATE语句:返回更新的记录数  
- 对于DELETE语句:返回删除的记录数  
- 如果执行失败则会抛出SQLException异常,而不是返回特殊值