# Leetcode-Python13

## 102. Binary Tree Level Order Traversal

May 31, 2023  4h

This is the thirteenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about ~~need to delete later~~.


## 102. Binary Tree Level Order Traversal
[leetcode](https://leetcode.com/problems/binary-tree-level-order-traversal/)\
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0102.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.md)\
[video](https://www.bilibili.com/video/BV1GY4y1u7b2/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
The recursion we learned in the last chapter is 深度优先搜索。\
层序遍历二叉树,相当于广度优先搜索. We can use **queue** to store the elements in each layer, and record the queue's size when we traverse each  layer of the binary tree.
```python
# ways 1: 利用长度法
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        queue = collections.deque([root]) #put the root of binary tree into a queue
        result = []
        while queue:
            level = [] # create a list to store tree's this level's elements
            for _ in range(len(queue)):
                cur = queue.popleft()
                level.append(cur.val)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
            result.append(level)
        return result
```
```python
# ways 2: 递归法
#确定递归函数的参数和返回值
#确定终止条件
#确定单层递归的逻辑
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        levels = []
        self.helper(root,0,levels)
        return levels
    
    def helper(self, node,level,levels):
        if not node:
            return
        if len(levels) == level:
            levels.append([])
        levels[level].append(node.val)
        self.helper(node.left, level+1, levels)
        self.helper(node.right, level+1, levels)
```

#### 107. Binary Tree Level Order Traversal II
return levels[::-1] here
#### 199. Binary Tree Right Side View
```python
#This time we do not need to return a list of lists, just one final list of numbers needs to be returned here.
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        result = []
        queue = deque([root])
        while queue:
            result.append(queue[0].val)
            for _ in range(len(queue)):
                tmp = queue.popleft()
                if tmp.right:
                    queue.append(tmp.right)
                if tmp.left:
                    queue.append(tmp.left)
        return result
```
#### 637. Average of Levels in Binary Tree
```python
class Solution:
    def averageOfLevels(self, root: Optional[TreeNode]) -> List[float]:
        if not root:
            return 0
        queue = collections.deque([root])
        result = []
        while queue:
            level = []
            for _ in range(len(queue)):
                cur = queue.popleft()
                level.append(cur.val)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
            result.append(sum(level)/len(level))
        return result
```
#### 429, 515, 116, 117, 104, 111
- 429.N叉树的层序遍历
- 515.在每个树行中找最大值
- 116.填充每个节点的下一个右侧节点指针
- 117.填充每个节点的下一个右侧节点指针II
- 104.二叉树的最大深度
- 111.二叉树的最小深度

## 226. Invert Binary Tree
翻转二叉树 （优先掌握递归）\ 
[leetcode](https://leetcode.com/problems/invert-binary-tree/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0226.%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.md)\
[video](https://www.bilibili.com/video/BV1sP4y1f7q7/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\



## 101.
对称二叉树 （优先掌握递归）\
