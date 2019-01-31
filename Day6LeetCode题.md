## LeetCode题

### 17、电话号码的字母组合

题目：

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**示例:**

```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**说明:**
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        HashMap<Integer, String[]> map=new HashMap<>();
        String[] str1={"a","b","c"};
        String[] str2={"d","e","f"};
        String[] str3={"g","h","i"};
        String[] str4={"j","k","l"};
        String[] str5={"m","n","o"};
        String[] str6={"p","q","r","s"};
        String[] str7={"t","u","v"};
        String[] str8={"w","x","y","z"};
        map.put(2, str1);
        map.put(3, str2);
        map.put(4, str3);
        map.put(5, str4);
        map.put(6, str5);
        map.put(7, str6);
        map.put(8, str7);
        map.put(9, str8);
        int len=digits.length();
        List<String> list=new ArrayList<>();
        for(int i=0;i<len;i++) {
            int flag2=Integer.parseInt(digits.substring(i, i+1));
            String[] tmp=map.get(flag2);
            List<String> list_tmp=new ArrayList<>();
            if(i!=0) {
                for(int j=0;j<list.size();j++) {
                    for(int k=0;k<tmp.length;k++) {
                        String f=list.get(j)+""+tmp[k];
                        System.out.println(f);
                        list_tmp.add(f);
                    }
                }
                res=list_tmp;
            }else {
                for(int k=0;k<tmp.length;k++) {
                    list.add(tmp[k]);
                }
            }

        }
        return list;


    }
}
```

![img](https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode17.png?raw=true)



+ 参考链接

[相由心生2020-CSDN博客](https://blog.csdn.net/u013360073/article/details/81482192)

[https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/submissions/](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/submissions/)

### 46、全排列

给定一个**没有重复**数字的序列，返回其所有可能的全排列。

**示例:**

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
         List<List<Integer>> listList = new ArrayList<>();
        //开始回溯
        backtracking(listList, nums, 0);
        return listList;
    }
    private static void backtracking(List<List<Integer>> listList, int[] nums, int i) {
        if (i == nums.length) {
            List<Integer> list = new ArrayList<>();
            for (int num : nums) list.add(num);
            listList.add(list);
        }
        for (int j = i; j < nums.length; j++) {
            //i、j互换（刚开始自己跟自己换）
            swap(nums, j, i);
            //往上回溯
            backtracking(listList, nums, i+1);
            //回溯完，i、j互换，一个循环结束，回到了最初的1,2,3
            swap(nums, j, i);
        }
    }
    private static void swap(int[] nums, int m, int n) {
        int temp = nums[m];
        nums[m] = nums[n];
        nums[n] = temp;

    }
}
```



![img](https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode46.png?raw=true)

+ 参考链接

[AlgerFan-CSDN博客](https://blog.csdn.net/qq_40914991/article/details/82055451)