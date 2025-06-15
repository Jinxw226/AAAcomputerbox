#mysql数据类型
- 选择数据类型原则：在满足业务需求的前提下，尽可能选择占用磁盘空间小的数据类型
## 数值类型
![[数据库数据类型之数值类型.png]]
- unsigned表示无符号类型，表示只能取0以及正数
- 不加默认为signed，表示可以取负数
```SQL
-- 年龄字段 ---不会出现负数, 而且人的年龄不会太大
   age tinyint unsigned

-- 分数 ---总分100分, 最多出现一位小数 4表示整个数字长度 1表示小数位个数
   score double(4,1)
```

## 字符串类型
![[数据库数据类型之字符串类型.png]]
- char 与 varchar 都可以描述字符串，
- char是==定长==字符串，指定长度多长，就占用多少个字符，和字段值的长度无关 。
- 而varchar是==变长==字符串，指定的长度为最大占用长度 。相对来说，char的性能会更高些。
```SQL
示例： 
    用户名 username ---长度不定, 最长不会超过50
    username varchar(50)
    身份证号 idcard ---长度固定为18
    idcard char(18)
    手机号 phone ---固定长度为11
    phone char(11)
```
- blob后缀存储的全是二进制形式的数据（如图片、音频和视频等）
- text后缀存储的全是文本数据

## 日期时间类型
![[数据库数据类型之日期时间类型.png]]
```SQL
示例: 
    生日字段  birthday ---生日只需要年月日  
    birthday date
    
    创建时间 createtime --- 需要精确到时分秒
    createtime  datetime
```