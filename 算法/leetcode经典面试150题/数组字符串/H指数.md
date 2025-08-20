**示例 1：**

**输入：**`citations = [3,0,6,1,5]`
**输出：**3 
**解释：**给定数组表示研究者总共有 `5` 篇论文，每篇论文相应的被引用了 `3, 0, 6, 1, 5` 次。
     由于研究者有 `3` 篇论文每篇 **至少** 被引用了 `3` 次，其余两篇论文每篇被引用 **不多于** `3` 次，所以她的 _h_ 指数是 `3`。

**示例 2：**

**输入：**citations = [1,3,1]
**输出：**1

解法：排序
初始化两个变量h = 0和数组大小citations.size()
现将数组进行排序，排序后从大往小开始遍历
如果citation[i] > h并且没有遍历完
h指数+1     
直到遍历完整个数组为止

注意while中的判断  语句citations[i] > h而不是大于等于  为了避免过度计数，如果3 = 3再过一遍while会导致h = 4结果错误

```cpp
#include<iostream>
#include<algorithm>
#include<vector>

using namespace std;

class Solution {
  public:
    int hIndex(vector<int>& citations){
      sort(citations.begin(),citations.end());
      for(int citation : citations){
        cout<<citation<<" ";
      }
      cout<<endl;
      int h = 0, i = citations.size() - 1;
      while(i >= 0 && citations[i] > h){
        cout<<"h: "<<h<<" i: "<<i<<" citation: "<<citations[i]<<endl;
        h++;
        i--;
      }
      return h;
    }
};

int main(){
  Solution s;
  vector<int> citations = {3,0,6,1,5};
  cout<<s.hIndex(citations)<<endl;
  return 0;
}
```

时间复杂度：O(n log n) + O(n) = O(n log n)
- O(n log n)：sort函数的时间复杂度

空间复杂度：由排序决定
- O(log n)：递归栈空间
- O(1)：常数空间