## Day3队列与堆

### 一、基本知识

### 队列

队列(Queue)是只允许在一端进行插入操作，而在另一端进行删除操作的线性表。

允许插入的端是队尾，允许删除的端是队头。

队列是一种先进先出（First In First Out）的线性表，简称FIFO。

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/Queue.png?raw=true"/>

为了提高出队的性能，就有了循环队列。

我们把队列的这种头尾相接的顺序存储结构称为循环队列。

<img src="https://img-blog.csdn.net/2018031923101062"/>

front指向队头，rear指向对尾元素的下一个位置，元素出队时front往后移动.

如果到了对尾则转到头部，同理入队时rear后移，

如果到了对尾则转到头部，这样通过下标front出队时，就不需要移动元素了。

当队列为空时，front和rear相等。

按照循环操作rear依次后移，然后再从头开始，也是出现rear和front相等时，队列满。

但是这样跟空队列的情况相同了，为了区分这种情况，规定数组还有一个空闲的单元，

表示队列已满，因为rear可能在front的后面，也可能循环到front的前面，所以队列满的条件

就变成了(rear+1)%maxsize=front，

同时队列元素个数的计算就是(rear- front+maxsize)%maxsize

### 堆排序

**堆**是一棵**顺序存储**的**完全二叉树**

其中每个结点的关键字都**不大于**其孩子结点的关键字，这样的堆称为**小根堆**。

其中每个结点的关键字都**不小于**其孩子结点的关键字，这样的堆称为**大根堆**。

举例来说，对于n个元素的序列{R0, R1, ... , Rn}当且仅当满足下列关系之一时，称之为堆：

**(1) Ri <= R2i+1 且 Ri <= R2i+2 (小根堆)**

**(2) Ri >= R2i+1且 Ri >= R2i+2 (大根堆)**

其中i=1,2,…,n/2向下取整; 

<img src="https://images2015.cnblogs.com/blog/318837/201604/318837-20160422104522335-1248911478.png"/>



如上图所示，序列R{3, 8, 15, 31, 25}是一个典型的小根堆。

堆中有两个父结点，元素3和元素8。

元素3在数组中以R[0]表示，它的左孩子结点是R[1]，右孩子结点是R[2]。

元素8在数组中以R[1]表示，它的左孩子结点是R[3]，右孩子结点是R[4]，它的父结点是R[0]。可以看出，它们**满足以下规律**：

设当前元素在数组中以**R[i]**表示，那么，

(1) 它的**左孩子结点**是：**R[2\*i+1]**;

(2) 它的**右孩子结点**是：**R[2\*i+2]**;

(3) 它的**父结点**是：**R[(i-1)/2]**;

(4) R[i] <= R[2*i+1] 且 R[i] <= R[2i+2]。

先通过详细的实例图来看一下，如何构建初始堆。

设有一个无序序列 { 1, 3, 4, 5, 2, 6, 9, 7, 8, 0 }。

<img src="https://images2015.cnblogs.com/blog/318837/201604/318837-20160422104522991-406805984.png"/>



#### 堆排序

堆排序 （HeapSort），就是对简单选择排序进行的一种改进

针对前面提到的无序序列 { 1, 3, 4, 5, 2, 6, 9, 7, 8, 0 } 来加以说明。

<img src="https://images2015.cnblogs.com/blog/318837/201604/318837-20160422104524038-1723180638.png"/>



## 二、LeetCode239滑动窗口最大值

**题目：**

给定一个数组 *nums*，有一个大小为 *k* 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口 *k* 内的数字。滑动窗口每次只向右移动一位。

返回滑动窗口最大值。

**示例：**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**注意：**

你可以假设 *k* 总是有效的，1 ≤ k ≤ 输入数组的大小，且输入数组不为空。

**代码**

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums == null || nums.length == 0) 
            return new int[0];
        LinkedList<Integer> deque = new LinkedList<Integer>();
        int[] res = new int[nums.length + 1 - k];
        for(int i = 0; i < nums.length; i++){
            // 每当新数进来时，如果发现队列头部的数的下标，是窗口最左边数的下标，则扔掉
            if(!deque.isEmpty() && deque.peekFirst() == i - k)
                deque.poll()；
            // 把队列尾部所有比新数小的都扔掉，保证队列是降序的
            while(!deque.isEmpty() && nums[deque.peekLast()] < nums[i])
                deque.removeLast();
            // 加入新数
            deque.offerLast(i);
            // 队列头部就是该窗口内第一大的
            if((i + 1) >= k) 
                res[i + 1 - k] = nums[deque.peek()];
        }
        return res;
    }
}
```

<img src="https://github.com/MasonJCode/DatawhaleLearning/blob/master/leetcode239.png?raw=true"/>



#### 参考链接

大话数据结构

[数据结构系列，队列的基本操作](https://blog.csdn.net/lin20044140410/article/details/79617397)

[堆与堆排序-静默虚空](https://www.cnblogs.com/jingmoxukong/p/4303826.html)

[jmspan的博客](https://blog.csdn.net/jmspan/article/details/51073879)

[励志编程小能手的博客](https://blog.csdn.net/qq_38765867/article/details/84197314)

[香蕉君的博客](https://blog.csdn.net/qq_37957829/article/details/78989118)

[ethannnli](https://segmentfault.com/a/1190000003903509)





