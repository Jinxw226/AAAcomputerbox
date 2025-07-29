#Logback日志类型
日志级别指的是日志信息的类型，日志都会分级别，常见的日志级别如下（优先级由低到高）：
![[logback日志级别.png]]

可以在配置文件`logback.xml`中，灵活的控制输出那些类型的日志。（==大于等于配置的日志级别的日志才会输出==）
```XML
<!-- 日志输出级别 -->
<root level="info">
    <!--输出到控制台-->
    <appender-ref ref="STDOUT" />
    <!--输出到文件-->
    <appender-ref ref="FILE" />
</root>
```