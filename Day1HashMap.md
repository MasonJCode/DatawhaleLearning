## 哈希表的学习
#### 哈希表的原理
哈希表就是一种以 键-值(key-indexed) 存储数据的结构，我们只要输入待查找的值即key，即可查找到其对应的值。
#### LeetCode题目练习
##### 1.两数之和
题目描述：
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9

所以返回 [0, 1]
##### 题解：(Java语言实现）
 ``` 
  /***
  给定的整数数组：int[] nums
  所要查找的元素int target
  ***/
  class Solution {
    public int[] twoSum(int[] nums, int target) {
    //创建新的哈希表
        Map<Integer,Integer>map = new HashMap<>();
		for(int i=0;i<nums.length;i++) {
    //第一次遍历，将元素放入哈希表中
			map.put(nums[i], i);
		}
		for(int i=0;i<nums.length;i++) {
    //第二次遍历，查找是否存在目标元素
			int n = target - nums[i];
       //确保存在的目标元素不是本身
			if(map.containsKey(n) && map.get(n)!=i) {
				int []m= {i,map.get(n)};
				return m;
			}
		}
		return null;
    }
} 
  ```
##### 202.快乐数
题目描述：编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，

然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，

那么这个数就是快乐数。
示例: 

输入: 19

输出: true

解释: 

12 + 92 = 82

82 + 22 = 68

62 + 82 = 100

12 + 02 + 02 = 1

##### 题解：(Java语言实现）
我们可以用set来记录所有出现过的数字，

然后每出现一个新数字，在set中查找看是否存在，

若不存在则加入表中，若存在则跳出循环，并且判断此数是否为1，

若为1返回true，不为1返回false，

``` 
  class Solution {
    public boolean isHappy(int n) {
         Set<Integer> set = new HashSet<>();
        while (n != 1 && !set.contains(n)) {
            set.add(n);
            int sum = 0;
            while (n != 0) {
                sum += Math.pow(n % 10, 2);
                n /= 10;
            }
            n = sum;
        }
        return n == 1;
    }
} 
 ```
 

  
