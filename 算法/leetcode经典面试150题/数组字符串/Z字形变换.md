将一个给定字符串 `s` 根据给定的行数 `numRows` ，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 `"PAYPALISHIRING"` 行数为 `3` 时，排列如下：

P   A   H   N
A P L S I I G
Y   I   R

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"PAHNAPLSIIGYIR"`。

请你实现这个将字符串进行指定行数变换的函数：

string convert(string s, int numRows);

解法：
![[Pasted image 20250825154651.png]]
![[Pasted image 20250825154657.png]]
![[Pasted image 20250825154705.png]]
![[Pasted image 20250825154710.png]]
![[Pasted image 20250825154717.png]]
![[Pasted image 20250825154724.png]]
![[Pasted image 20250825154730.png]]
![[Pasted image 20250825154737.png]]
![[Pasted image 20250825154742.png]]

`vector<string> rows(numRows);`初始化名为rows的数组并且初始化元素为numRows个
flag表示上下方向-1表示向上 1表示向下
起始题目可以理解为从上到下在从下到上为每个rows数组放字符
当行索引 i 到天花板或者最低处则改变flag方向

最后拼接每一行的字符串就是需要的结果

注意：
## 📌 引用 vs 取地址符

| 特性     | 引用 (`&`在类型后)        | 取地址符 (`&`在变量前) |     |
| ------ | ------------------- | -------------- | --- |
| **位置** | `类型&`               | `&变量`          |     |
| **作用** | 创建别名                | 获取地址           |     |
| **示例** | `const string& row` | `&row`         |     |
### 方式一：使用拷贝（不推荐）
```cpp
for (string row : rows)  // 每次循环都会拷贝一个字符串
```
- **缺点**：性能差，每次循环都要复制整个字符串
- **内存开销**：O(n × 字符串平均长度)
### 方式二：使用引用（推荐）
```cpp
for (const string &row : rows)  // 只是别名，无拷贝
```
- **优点**：高性能，直接访问原字符串
- **内存开销**：O(1)，只是多一个指针大小

```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if(numRows < 2){
            return s;
        }
        vector<string> rows(numRows);
        int flag = -1,i = 0;
        for(char c : s){
            rows[i].push_back(c);
            if( i == 0 || i == numRows - 1){
                flag = -flag;
            }
            i = i + flag;
        }
        string res;
        for(const string& row : rows){
            res += row;
        }
        return res;
    }
};
```