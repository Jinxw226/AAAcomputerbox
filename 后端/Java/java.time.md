#time包（java） 

java.time：Java 8引入的日期时间API（`java.time`包），具体功能是将一个字符串形式的日期解析为`LocalDate`对象。
1. `parse()`是一个静态方法，用于将字符串解析为`LocalDate`对象。
	- 第一个参数为需要解析的日期字符串
	- 第二个参数为注定日期字符串的格式
2.  **`DateTimeFormatter.ofPattern()`**
	- `DateTimeFormatter`是日期时间格式化类。
	- `ofPattern()`方法根据指定的模式字符串创建格式化器。这里的`"yyyyMMdd"`表示：
	    - `yyyy`：4位年份（如1990）
	    - `MM`：2位月份（01-12）
	    - `dd`：2位日期（01-31）
	`LocalDate date = LocalDate.parse(birthday,DateTimeFormatter.ofPattern("yyyyMMdd"));`
3. **`Period.between()`**
	- 用法：计算两个 `LocalDate` 之间的时间差，返回一个 `Period` 对象（表示“一段时期”，包含年、月、日的差值）。
	- `LocalDate.now()`：当前系统日期。
	`Period.between(LocalDate , LocalDate.now()).getYears();`
