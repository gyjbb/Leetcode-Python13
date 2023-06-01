# Leetcode-Python13

## 102. Binary Tree Level Order Traversal, ## 226. Invert Binary Tree, 101.Symmetric Tree

May 31, 2023  4h

This is the thirteenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The first challenges today is how to use queue to realize 层次遍历（迭代法）。 \
Then, in the second and third challenges, we reviewed how to use recursion递归 to solve problems, like in the last chapter Leetcode-Python12. \
In conclusion, recursion递归 needs to carefully consider the 深度前中后序；\
迭代 can also have 深度前中后序, besides, 迭代 has 广度优先遍历/层次遍历, and simply 迭代queue/stack.

深度优先遍历: **前序**遍历（递归法，迭代法), **中序**遍历（递归法，迭代法）, **后序**遍历（递归法，迭代法）\
广度优先遍历: 层次遍历（迭代法）\
递归法: 1.确定递归函数的参数和返回值; 2.确定终止条件; 3.确定单层递归的逻辑

## 102. Binary Tree Level Order Traversal
[leetcode](https://leetcode.com/problems/binary-tree-level-order-traversal/)\
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0102.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.md)\
[video](https://www.bilibili.com/video/BV1GY4y1u7b2/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
The recursion we learned in the last chapter is 深度优先搜索。\
**层序遍历二叉树**,相当于广度优先搜索. We can use **queue** to store the elements in each layer, and record the queue's size when we traverse each  layer of the binary tree.
```python
# ways 1: 迭代法, 广度优先遍历
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
[leetcode](https://leetcode.com/problems/invert-binary-tree/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0226.%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.md)\
[video](https://www.bilibili.com/video/BV1sP4y1f7q7/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
翻转二叉树 (优先掌握**递归**) \
Here we can use preorder/postorder traversal to solve this question, which is better than 中序。
```python
# ways 1: use recursion递归法 and preorder traversal:
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        root.left, root.right = root.right, root.left # 中
        self.invertTree(root.left)     # 左
        self.invertTree(root.right)    # 右
        return root
```
```python
# ways 2: 迭代法：postorder traversal：
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return None      
        stack = [root]        
        while stack:
            node = stack.pop()   
            node.left, node.right = node.right, node.left                   
            if node.left:
                stack.append(node.left)
            if node.right:
                stack.append(node.right)  
        return root
```
```python
# ways 3: 迭代法：广度优先遍历（层序遍历）：
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root: 
            return None

        queue = collections.deque([root])    
        while queue:
            for i in range(len(queue)):
                node = queue.popleft()
                node.left, node.right = node.right, node.left
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
        return root   
```

## 101.Symmetric Tree
[leetcode](https://leetcode.com/problems/symmetric-tree/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0101.%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.md)\
[video](https://www.bilibili.com/video/BV1ue4y1Y7Mf/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
对称二叉树 （优先掌握**递归**)\
Here the best way is **postorder traversal**, because we need to firstly collect the information of the **sub trees** of a node.\
```python
# ways 1: use recursion递归法 and postorder traversal:
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        return self.compare(root.left, root.right)
        
    def compare(self, left, right):
        #首先排除空节点的情况
        if left == None and right != None: return False
        elif left != None and right == None: return False
        elif left == None and right == None: return True
        #排除了空节点，再排除数值不相同的情况
        elif left.val != right.val: return False
        
        #此时就是：左右节点都不为空，且数值相同的情况
        #此时才做递归，做下一层的判断
        outside = self.compare(left.left, right.right) #左子树：左、 右子树：右
        inside = self.compare(left.right, right.left) #左子树：右、 右子树：左
        isSame = outside and inside #左子树：中、 右子树：中 （逻辑处理）
        return isSame
```
```python
# ways 2: use 迭代法queue, NOT 层次遍历（迭代法）or 前中后序的迭代写法 here!
import collections
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        queue = collections.deque()
        queue.append(root.left) #将左子树头结点加入队列
        queue.append(root.right) #将右子树头结点加入队列
        while queue: #接下来就要判断这这两个树是否相互翻转
            leftNode = queue.popleft()
            rightNode = queue.popleft()
            if not leftNode and not rightNode: #左节点为空、右节点为空，此时说明是对称的
                continue
            
            #左右一个节点不为空，或者都不为空但数值不相同，返回false
            if not leftNode or not rightNode or leftNode.val != rightNode.val:
                return False
            queue.append(leftNode.left) #加入左节点左孩子
            queue.append(rightNode.right) #加入右节点右孩子
            queue.append(leftNode.right) #加入左节点右孩子
            queue.append(rightNode.left) #加入右节点左孩子
        return True
```
```python
# ways 3: use 迭代法stack, similar to ways2 迭代法queue:
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        st = [] #这里改成了栈
        st.append(root.left)
        st.append(root.right)
        while st:
            rightNode = st.pop()
            leftNode = st.pop()
            if not leftNode and not rightNode:
                continue
            if not leftNode or not rightNode or leftNode.val != rightNode.val:
                return False
            st.append(leftNode.left)
            st.append(rightNode.right)
            st.append(leftNode.right)
            st.append(rightNode.left)
        return True
```
```python
# ways 4: 迭代法层次遍历
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        
        queue = collections.deque([root.left, root.right])
        
        while queue:
            level_size = len(queue)
            
            if level_size % 2 != 0:
                return False
            
            level_vals = []
            for i in range(level_size):
                node = queue.popleft()
                if node:
                    level_vals.append(node.val)
                    queue.append(node.left)
                    queue.append(node.right)
                else:
                    level_vals.append(None)
                    
            if level_vals != level_vals[::-1]:
                return False
            
        return True
```



#### 100.相同的树
#### 572.另一个树的子树



