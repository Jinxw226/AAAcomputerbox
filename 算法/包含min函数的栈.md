#包含min函数的栈

时间复杂度O(1)

![[Pasted image 20250814171804.png]]

```cpp
#include<stack>
#include<iostream>

using namespace std;

class MinStack{
public:
  stack<int> stk,stk_min;

  MinStack(){

  }

  void push(int x){
    stk.push(x);
    if(stk_min.size()) x = min(stk_min.top(), x );
    stk_min.push(x);
  }
  
  void pop(){
    stk.pop();
    stk_min.pop();
  }

  int top(){
    return stk.top();
  }

  int getMin(){
    return stk_min.top();
  }
};
```