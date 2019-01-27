## Day2链表

### 一、链表

#### 1.概述

单链表是一种线性表的链式存储结构，因为此链表的每个结点中只包含一个指针域，所以叫 做单链表。

#### 2.单链表的图示
![image](https://github.com/MasonJCode/DatawhaleLearning/blob/master/%E5%8D%95%E9%93%BE%E8%A1%A8%E5%9B%BE%E7%A4%BA.png?raw=true)

#### 3.单链表的操作

+ 插入操作：

  将值为element的新节点插入到第index的位置上。

  首先要先找到索引为index-1的节点，然后生成一个数据为element的新节点newNode，

  并令index-1处节点的next指向新节点，新节点的next指向原来index处的节点。
  
  ![image](https://github.com/MasonJCode/DatawhaleLearning/blob/master/%E9%93%BE%E8%A1%A8%E6%93%8D%E4%BD%9C.png?raw=true)



+ 删除操作：

  删除第index个节点，第index节点是由index-1出的节点引用的，

  因此删除index的节点要先获取index-1处的节点，

  然后让index-1出节点的next引用到原index+1处的节点，并释放index处节点即可。
  ![Image](https://github.com/MasonJCode/DatawhaleLearning/blob/master/%E9%93%BE%E8%A1%A8%E5%88%A0%E9%99%A4.png?raw=true)
  



#### 4.参考链接

大话数据结构

[单链表-sihai的博客](https://blog.csdn.net/sihai12345/article/details/80721065)

## 二、LeetCode练习

### 1）142.环形链表II

##### 题目：给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

##### 为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**说明：**不允许修改给定的链表。

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

**示例 2：**

```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

**示例 3：**

```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)



- 解法一：

  ```java
  /**
   * Definition for singly-linked list.
   * class ListNode {
   *     int val;
   *     ListNode next;
   *     ListNode(int x) {
   *         val = x;
   *         next = null;
   *     }
   * }
   */
  public class Solution {
      public ListNode detectCycle(ListNode head) {
          if(head==null){
              return null;
          }
          ListNode fast;//快指针
          ListNode slow;//慢指针
          ListNode node;//指向链表头节点的node的节点
          node = fast = node =head;
          while(fast!=null&&fast.next!=null){
              fast = fast.next.next;
              slow = slow.next;
              if(fast == slow){
                  while(fast!=node){
                      fast = fast.next;
                      node = node.next;
                  }
                  return node;
              }
          }
          return null;
      }
  }
  ```

  <img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode142(1).png?raw=true"/>

- 解法二：

  用HashSet集合记录已经访问过的节点，如果指针指向的节点在集合中存在，那么这个节点就是入口。

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
    	if(head ==null){
            return null;
        }
        Set<ListNode>s = new HashSet<>();
        ListNode node=head;
        while(node!=null && node.next!=null && !s.contains(node)){
            s.add(node);
            node=node.next;
            if(s.contains(node)){
                return node;
            }
        }
        
        return null;
    ｝
｝
```

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/LeetCode142(2).png?raw=true"/>

### 2)   206.反转列表

##### 题目：反转一个单链表。

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

解：

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode first = head;
        //新建一个reverse节点存放反转后的结果
        ListNode reverse = null;
        //遍历输入链表开始处理每一个节点
        while(first != null){
        //创建新结点来存储firs结点的后继节点
            ListNode temp = first.next;
            //将first放到reverse头节点的头部
            first.next=reverse;
            //移动reverse链表的头指针，让它始终指向新链表的头部
            reverse = first;
            //继续处理原链表的节点
            first=temp;
        }
        return reverse;
    }
}
```

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/LeetCode206.png?raw=true"/>

### 3）参考链接

[https://www.cnblogs.com/springfor/p/3862125.html](https://www.cnblogs.com/springfor/p/3862125.html)

[https://blog.csdn.net/ds19980228/article/details/84096184](https://blog.csdn.net/ds19980228/article/details/84096184)

[https://www.cnblogs.com/tengdai/p/9279421.html](https://www.cnblogs.com/tengdai/p/9279421.html)

