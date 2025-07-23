#if函数语法
```XML
<!-- 统计员工的性别信息 -->
<select id="countEmpGenderData" resultType="java.util.Map">
    select
    if(gender = 1, '男', '女') as name,
    count(*) as value
    from emp group by gender ;
</select>
```

if函数语法：`if(条件, 条件为true取值, 条件为false取值)`
ifnull函数语法：`ifnull(expr, val1)` 如果expr不为null，取自身，否则取val1