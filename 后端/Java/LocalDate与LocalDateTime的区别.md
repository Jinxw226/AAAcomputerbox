#localdate #localdatetime
- ==**LocalDate**== 仅包含日期信息，没有时间和时区的概念。它专门用于表示年、月、日信息，适用于那些不需要精确到时间的场景。例如，你可以使用_LocalDate.now()_获取当前日期，或者使用_LocalDate.of(year, month, day)_来创建一个特定的日期。

- ==**LocalDateTime**== 则包含了日期和时间信息，但同样不包含时区。它可以精确到纳秒，适用于需要同时表示日期和时间的场景。_LocalDateTime_可以通过_LocalDateTime.now()_获取当前的日期和时间，或者通过_LocalDateTime.of(year, month, day, hour, minute, second)_来创建一个特定的日期和时间。