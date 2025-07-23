#case

**case流程控制函数：**
- 语法一：case when cond1 then res1 [ when cond2 then res2 ] else res end ;
- 含义：如果 cond1 成立， 取 res1。 如果 cond2 成立，取 res2。 如果前面的条件都不成立，则取 res。


- 语法二（仅适用于==等值匹配==）：case expr when val1 then res1 [ when val2 then res2 ] else res end ;
- 含义：如果 expr 的值为 val1 ， 取 res1。 如果 expr 的值为 val2 ，取 res2。 如果前面的条件都不成立，则取 res。

示例：
```sql
select  
    (case when job=1 then '班主任'  
        when job=2 then '讲师'  
        when job=3 then '学工主管'  
        when job=4 then '教研主管'  
        when job=5 then '咨询师' else '其他' end) pos,  
    count(*) num  
from emp group by job order by num;
```