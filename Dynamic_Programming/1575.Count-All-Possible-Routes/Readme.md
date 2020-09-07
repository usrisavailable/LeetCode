### 1575.Count-All-Possible-Routes

当我们考虑到达城市c有多少种方案的时候，势必会考虑之前可能在哪个城市？如果之前的城市是d，那么问题就转化为了“达到城市d多少种方案”，另外加上一个约束：有足够的剩余油量能够从d来到c。所以每到一个城市的剩余油量亦是一个关键因素。

本题最大的提示就是fuel的数据范围只有200，因此我们暴力遍历这个变量空间的所有值都是可行的。什么意思？就是我们可以定义状态dp[f][c]表示（从初始状态）到达城市c、剩余油料是f时，有多少种行程方案。因此我们可以根据上面的思路，遍历c之前的一站d。令d和c之间的油料消耗是g，那么说明前一站的状态就是dp[f+g][d]。如果知道有多少方案能够达到dp[f+g][d]，那么就说明有相同数量的方案可以达到dp[f][c]。所以状态转移方程是：
```cpp
for (int d=0; d<n; d++)
  g = dis(c,d);
  dp[f][c] += dp[f+g][d];
```
此外要注意d不能与c重复，此外f+g不能超过初始油量fuel.

最终的答案是```sum {dp[f][finish]}```，其中油量f可以是任意值。因为不同的方案，达到终点的油量都不一样。我们需要把每种方案都累加起来。