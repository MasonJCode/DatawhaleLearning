### 132 分割回文串II

#### 题目： 

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回符合要求的最少分割次数。

**示例:**

```
输入: "aab"
输出: 1
解释: 进行一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。
```

Java的charAt（）方法用于返回指定索引处的字符。索引范围从0到length（）-1.

```java
class Solution {
    public int minCut(String s) {
        int n = s.length();
		boolean[][] judge = new boolean[n][n];
// dp[i]表示s中第i个字符到第（n-1）个字符所构成的子串的最小分割次数
		int[] dp = new int[n]; 
		for (int i = n - 1; i >= 0; i--) {
			dp[i] = Integer.MAX_VALUE;
			for (int j = i; j < n; j++) {
				if (s.charAt(i) == s.charAt(j) && (j - i <= 1 || judge[i + 1][j - 1])) {
					judge[i][j] = true;
					if (j + 1 < n) {
						dp[i] = Math.min(dp[i], 1 + dp[j + 1]);
					}else{
						dp[i] = 0;
					}
				}
			}
		}
		return dp[0];


    }
}
```

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode132.png?raw=true"/>



**参考链接**

[https://blog.csdn.net/qq_41231926/article/details/85335825](https://blog.csdn.net/qq_41231926/article/details/85335825)

### 01背包问题

**问题描述：**

假设现有容量10kg的背包，另外有3个物品，分别为a1，a2，a3。物品a1重量为3kg，价值为4；物品a2重量为4kg，价值为5；物品a3重量为5kg，价值为6。将哪些物品放入背包可使得背包中的总价值最大？

动态规划法：

求背包能够获得的总价值-》求前i 个物体放入容量为m(kg)背包的最大价值c[i] [m] (使用数组存储)

c[i] [m] = max{c[i-1] [m-w[i]]+pi,c[i-1] [m]}

​	w[i] :  第i个物体的重量；

　　p[i] : 第i个物体的价值；

　　c[i] [m] ： 前i个物体放入容量为m的背包的最大价值；

　　c[i-1] [m] ： 前i-1个物体放入容量为m的背包的最大价值；

　　c[i-1] [m-w[i]] ： 前i-1个物体放入容量为m-w[i]的背包的最大价值；

具体代码：参见Day5笔记：https://github.com/MasonJCode/DatawhaleLearning/blob/master/Day5%E9%80%92%E5%BD%92%E5%8F%8ADP.md



**参考链接**

https://www.cnblogs.com/lfeng1205/p/5981198.html



