原理痛等分和子集
代码如下：
```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int length = stones.length;
        if(length == 1){
            return stones[0];
        }
        if(length == 0){
            return 0;
        }
        int sum = 0;
        for(int i = 0;i < length;i++){
            sum += stones[i];
        }
        int target = sum/2;
        int[] dp = new int[target+1];
        for(int i = 0;i < length;i++){
            for(int j = target;j >= stones[i];j-- ){
                dp[j] = Math.max(dp[j],dp[j-stones[i]]+stones[i]);
            }
        }
        int last = sum - dp[target];
        return last-dp[target];
    }
}
```