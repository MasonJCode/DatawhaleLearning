## Day4 树的遍历

### 一、介绍

二叉树遍历分为三种：前序、中序、后序。

<img src="https://img-blog.csdn.net/20180507105447745"/>



前序遍历：先访问根节点-》再遍历左子树-》再遍历右子树（ABC）

中序遍历：先遍历左子树-》再访问根节点-》再遍历右子树（BAC）

后序遍历：先访遍历左子树-》再遍历右子树-》再访问根节点（BCA）

<img src="https://img-blog.csdn.net/20180822171020103?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbnNpb256/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70"/>

**层次遍历**：按层次遍历(ABCDEF)

## 二、LeetCode题

+ 98.验证二叉搜索树

  给定一个二叉树，判断其是否是一个有效的二叉搜索树。

  假设一个二叉搜索树具有如下特征：

  - 节点的左子树只包含**小于**当前节点的数。
  - 节点的右子树只包含**大于**当前节点的数。
  - 所有左子树和右子树自身必须也是二叉搜索树。

  **示例 1:**

  ```
  输入:
      2
     / \
    1   3
  输出: true
  ```

  **示例 2:**

  ```
  输入:
      5
     / \
    1   4
       / \
      3   6
  输出: false
  解释: 输入为: [5,1,4,null,null,3,6]。
       根节点的值为 5 ，但是其右子节点值为 4 。
  ```



解：

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    public TreeNode prev = null;
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        //首先找到最左节点的值
        TreeNode left = root;
        while (left.left != null) {
            left = left.left;
        }
        prev = left;
        return isValid(root);

    }
     private boolean isValid(TreeNode root) {
        if (root == null) return true;
        if (!isValid(root.left)) return false;
        if (root != prev && root.val <= prev.val) return false;
        prev = root;
        return isValid(root.right);
    }
}
```

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode98.png?raw=true"/>

**参考链接**

[https://www.cnblogs.com/ljdblog/p/6721418.html](https://www.cnblogs.com/ljdblog/p/6721418.html)



+ 102.二叉树的层次遍历

  给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

  例如:
  给定二叉树: `[3,9,20,null,null,15,7]`,

  ```
      3
     / \
    9  20
      /  \
     15   7
  ```

  返回其层次遍历结果：

  ```
  [
    [3],
    [9,20],
    [15,7]
  ]
  ```

  解：

  ```java
  /**
   * Definition for a binary tree node.
   * public class TreeNode {
   *     int val;
   *     TreeNode left;
   *     TreeNode right;
   *     TreeNode(int x) { val = x; }
   * }
   */
  class Solution {
      List<List<Integer>> list1 = new ArrayList<List<Integer>>();
      Queue<TreeNode> queue =new LinkedList<TreeNode>();
      public List<List<Integer>> levelOrder(TreeNode root) {       
          if(root==null){
               return list1;
           }
          //向队列添加一个元素
           queue.offer(root);
           while(!queue.isEmpty()){
               List<Integer> list2 = new ArrayList<Integer>();
               int size = queue.size();
               for(int i=0;i<size;i++){
                   //移除队首结点
                   TreeNode node = queue.remove();
                   list2.add(node.val);
                   //判断左子树是否存在非空结点
                   if(node.left!=null){
                       //入队左子树的结点
                       queue.offer(node.left);
                   }
                   //判断右子树是否存在非空结点
                   if(node.right!=null){
                       //入队右子树的结点
                       queue.offer(node.right);
                   }
               }
               list1.add(list2);
           }
           return list1;
      }
  }
  ```

  <img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode102.png?raw=true"/>

  **参考链接**

  [https://www.cnblogs.com/WalkerSteve/p/6606451.html](https://www.cnblogs.com/WalkerSteve/p/6606451.html)

  [Java中queue的使用](http://www.cnblogs.com/end/archive/2012/10/25/2738493.html)

  

+ 107.二叉树的层次遍历

  给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

  例如：
  给定二叉树 `[3,9,20,null,null,15,7]`,

  ```
      3
     / \
    9  20
      /  \
     15   7
  ```

  返回其自底向上的层次遍历为：

  ```
  [
    [15,7],
    [9,20],
    [3]
  ]
  ```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> list = new LinkedList<List<Integer>>();
        Queue<TreeNode> queue =new LinkedList<TreeNode>();
        if(root==null){
            return list;
        }
        queue.add(root);
        //记录每层结点个数
        int i = queue.size();
        TreeNode temp = null;
        List<Integer> level = new ArrayList<>();
        while(!queue.isEmpty()){
            if(i == 0){
                list.addFirst(level);
                i=queue.size();
                level=new ArrayList<>();
            }
            temp=queue.poll();
            level.add(temp.val);
            --i;
            if(temp.left !=null){
                queue.add(temp.left);
            }
            if(temp.right !=null){
                queue.add(temp.right);
            }
        }
        list.addFirst(level);
        return list;
    }
}
```

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode107.png?raw=true"/>

**参考链接**

[https://blog.csdn.net/crazy1235/article/details/51508308](https://blog.csdn.net/crazy1235/article/details/51508308)

