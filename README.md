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