# Start to learning algorithms
参考文档：https://labuladong.gitee.io/algo/

## Day 1 学习算法和刷题的框架思维
### 数据结构
数据结构的存储方式：数组和链表

基本数据结构：数组、栈、队列、链表、树、散列表、堆、图。

访问数据结构：递归、迭代
### 算法刷题原则
**先刷二叉树，培养框架思维**
```java
void traverse(TreeNode root) {
    // 前序遍历代码位置
    traverse(root.left)
    // 中序遍历代码位置
    traverse(root.right)
    // 后序遍历代码位置
}
```
## Day 2 动态规划解题套路框架
动态规划问题的一般形式就是求最值

核心问题是穷举：如何穷举->如何聪明地穷举

明确 base case -> 明确「状态」-> 明确「选择」 -> 定义 dp 数组/函数的含义

```java
# 初始化 base case
dp[0][0][...] = base
# 进行状态转移
for 状态1 in 状态1的所有取值：
    for 状态2 in 状态2的所有取值：
        for ...
            dp[状态1][状态2][...] = 求最值(选择1，选择2...)

```
## Day 3 回溯算法解题套路框架
解决一个回溯问题，实际上就是一个决策树的遍历过程

主要思考三个问题：

1、路径：也就是已经做出的选择。

2、选择列表：也就是你当前可以做的选择。

3、结束条件：也就是到达决策树底层，无法再做选择的条件。

```java
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return
    
    for 选择 in 选择列表:
        做选择
        backtrack(路径, 选择列表)
        撤销选择
```

核心部分：for 循环里面的递归，在递归调用之前「做选择」，在递归调用之后「撤销选择」

## Day 3 BFS 算法解题套路框架
DFS 算法就是回溯算法

问题的本质就是让你在一幅「图」中找到从起点 start 到终点 target 的最近距离。BFS 找到的路径一定是最短的，但代价就是空间复杂度比 DFS 大很多
```java
// 计算从起点 start 到终点 target 的最近距离
int BFS(Node start, Node target) {
    
    Queue<Node> q; // 核心数据结构
    Set<Node> visited; // 避免走回头路
    
    q.offer(start); // 将起点加入队列
    visited.add(start);
    int step = 0; // 记录扩散的步数

    while (q not empty) {
        int sz = q.size();
        /* 将当前队列中的所有节点向四周扩散 */
        for (int i = 0; i < sz; i++) {
            Node cur = q.poll();  // 将首个元素从队列中弹出
            /* 划重点：这里判断是否到达终点 */
            if (cur is target)
                return step;
            /* 将 cur 的相邻节点（子节点）加入队列 */
            for (Node x : cur.adj())
                if (x not in visited) {
                    q.offer(x); // 将相邻（子）元素加入队列
                    visited.add(x);
                }
        }
        /* 划重点：更新步数在这里 */
        step++;
    }
}

```

## Day 4 二分查找
最常用的二分查找场景：寻找一个数、寻找左侧边界、寻找右侧边界

写二分查找尽量不要出现 else，而是把所有情况用 else if 写清楚，这样可以清楚地展现所有细节

寻找一个数、寻找左侧边界的二分搜索 如[1,2,2,2,3,4]找到最左侧的2、寻找右侧边界的二分搜索

```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}

int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定左侧边界
            right = mid - 1;
        }
    }
    // 最后要检查 left 越界的情况
    if (left >= nums.length || nums[left] != target)
        return -1;
    return left;
}


int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定右侧边界
            left = mid + 1;
        }
    }
    // 最后要检查 right 越界的情况
    if (right < 0 || nums[right] != target)
        return -1;
    return right;
}
```