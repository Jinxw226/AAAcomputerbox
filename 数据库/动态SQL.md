#动态sql
- 动态SQL：**指的就是随着用户的输入或外部的条件的变化而变化的SQL语句。**
在这里呢，我们用到了两个动态SQL的标签：`<if>` `<where>`。 这两个标签的具体作用如下：

`<if>`：判断条件是否成立，如果条件为true，则拼接SQL。
`<where>`：根据查询条件，来生成where关键字，并会自动去除条件前面多余的and或or。

```XML
<!--定义Mapper映射文件的约束和基本结构-->
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.EmpMapper">
    <select id="list" resultType="com.itheima.pojo.Emp">
        select e.*, d.name deptName from emp as e left join dept as d on e.dept_id = d.id
        <where>
            <if test="name != null and name != ''">
                e.name like concat('%',#{name},'%')
            </if>
            <if test="gender != null">
                and e.gender = #{gender}
            </if>
            <if test="begin != null and end != null">
                and e.entry_date between #{begin} and #{end}
            </if>
        </where>
    </select>
</mapper>
```