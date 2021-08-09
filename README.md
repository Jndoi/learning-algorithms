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