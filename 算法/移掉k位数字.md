#移掉k为数字
给定一个非负整数num，移除这个数中的k为数字，是的剩下的数字最小
 ![[移掉k位数字.png]]

```cpp
#include<iostream>

using namespace std;

int main(){
  string num;
  int k;
  cin >> num >> k;

  string res = "0";
  for(int i = 0 ;i < num.size(); i++){
    while( k && num[i] < res.back()){
      res.pop_back();
      k--;
    }
    res += num[i];
  }

  while(k --) res.pop_back();
  int i = 0;
  while(i < res.size() && res[i] == '0') i++;

  if(i == res.size()) puts("0");
  else cout<< res.substr(i) << endl;

  return 0;
}
```