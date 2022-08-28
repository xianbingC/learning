### 字符串

### 数组
#### 1. 合并两个有序数组
给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。

请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。
```
// 逆序遍历，比较两个数组的元素，每次取最大的那个元素，置于新的位置。
```

#### 2.子集II
给你一个整数数组 nums ，其中可能包含重复元素，请你返回该数组所有可能的子集（幂集）。

解集 不能 包含重复的子集。返回的解集中，子集可以按 任意顺序 排列。
```
// 回溯，每得到一种结果就加入结果集，去重在于，每次循环不能使用重复的元素。即nums[i] != nums[i - 1]，要注意最左边界条件。
```
#### 3.子集
给你一个整数数组 nums ，数组中的元素 互不相同 。返回该数组所有可能的子集（幂集）。

解集 不能 包含重复的子集。你可以按 任意顺序 返回解集。
```
// 和子集II思路一致，但不需要考虑去重。
```

#### 4.买卖股票的最佳时机
给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。
```
// 高点卖出，取当前利润与卖出后得到利润中的最大值；低点买入。
```

#### 5.买卖股票的最佳时机II
给你一个整数数组 prices ，其中 prices[i] 表示某支股票第 i 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 最多 只能持有 一股 股票。你也可以先购买，然后在 同一天 出售。

返回 你能获得的 最大 利润 。
```
// 定义最大总利润，当前买卖最大利润，当前价格
// 遍历股票，价值增长，则重新计算当前最大利润，价值-当前价格
// 当价值降低，则卖出股票，当前最大利润加到总利润中，并清0，更新当前价格=股票价值
// 遍历结束可能会出现股票还未卖出的情形，即当前买卖最大利润大于0，需注意。
```

### DFS&BFS
#### 1.复原IP地址
有效 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效 IP 地址。
给定一个只包含数字的字符串 s ，用以表示一个 IP 地址，返回所有可能的有效 IP 地址，这些地址可以通过在 s 中插入 '.' 来形成。你 不能 重新排序或删除 s 中的任何数字。你可以按 任何 顺序返回答案。
```
// 回溯，每次有三种组合，1位数，2位数和3位数；
// 字符串可以先保存至path数组中，当得到一个符合的结果时，再进行拼接
DFS(s, ret, path, cur) {
  if (cur < s.size()) ...
  if (cur < s.size() + 1 && s[cur] != '0')...
  if (cur < s.size() + 2 && s[cur ... cur + 2] <= 255 && s[cur] != '0')...
}
```

### 二叉树
#### 1.中序遍历
```
// 概念：先左子树，再根节点，最后右子树
// 1.递归
// 2.利用栈
while(!st.empty() || cur) {
  if (cur != NULL) {
    st.push(cur);
    cur = cur->left;
  } else {
    ret.push_back(st.top()->val);
    cur = st.top()->right;
    st.pop();
  }
}
```
#### 2.不同的二叉搜索树II
给你一个整数 n ，请你生成并返回所有由 n 个节点组成且节点值从 1 到 n 互不相同的不同 二叉搜索树 。可以按 任意顺序 返回答案。
```
for i in start...end
  left_trees = func(start, i - 1)
  right_trees = func(i + 1, end)
  for left_tree in left_trees
    for right_tree in right_trees
      root = new TreeNode(i)
      root->left = left_tree
      root->right = right_tree
      trees.push_back(root)
return trees
```
#### 3.不同的二叉搜索树
求二叉搜索树的种数
```
// 思路同上，需要用一个数组来记录相同结点数能够组成的种类数，从而实现减枝
if start > end:
  return 1
for i in start...end
  if i - 1 >= start && flag[i - 1 - start] != 0:
    left_num = flag[i - 1 - start]
  else
    left_num = TreeNums(start, i - 1, flag)
  if end >= i + 1 && flag[end - i - 1] != 0:
    right_num = flag[end - i - 1]
  else
    right_num = TreeNums(i + 1, end, flag)
  num += left_num * right_num
flag[end - start] = num;
return num
```
#### 4.验证二叉搜索树
给你一个二叉树的根节点 root ，判断其是否是一个有效的二叉搜索树。
```
// 思路1：更新最小边界和最大边界值，保证每次的值都在边界内即可，否则是无效BST
def func(root, min, max):
  if root == NULL:
    return true
  if root->val is not in (min,max):
    return false
  return func(root->left, min, root->val)
          && runc(root->right, root->val, max)
// 思路2：中序遍历是有序的，否则为无效BST
```

#### 5.恢复二叉搜索树
给你二叉搜索树的根节点 root ，该树中的 恰好 两个节点的值被错误地交换。请在不改变其结构的情况下，恢复这棵树 。
```
// 对于BST，中序遍历，交换两个节点，会出现两种情况:
// (1) a[i] > a[i+1], a[j - 1] > a[j]
// (2) a[i] > a[j], i = j + 1
// 其中i和j发生了交换
// 即{1,4,3,2}，4和2发生了交换；{1,2,4,3}，4和3发生了交换
// 思路1：迭代法中序遍历，用数组记录下节点后，按上述方法找出交换的节点后进行恢复。
// 思路2：用两个节点记录下发生交换的节点即可。
```

#### 6.相同的树
给你两棵二叉树的根节点 p 和 q ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。
```
// 思路1：如题，递归
// 思路2：中序遍历和前序遍历或者中序遍历和后序遍历结果一致
```
#### 7.对称二叉树
给你一个二叉树的根节点 root ， 检查它是否轴对称。
```
// 思路1：递归
isSymmetric(left->right, right->left) && isSymmetric(left->left, right->right)
// 思路2：非递归
queue.push(root->left)
queue.push(root->right)
while (!queue.empty()):
  // 每次取出一对对称的节点
  l = queue.front()
  queue.pop()
  r = queue.front()
  queue.pop()
  if (l == NULL && r == NULL) {
    continue;
  }
  if (l == NULL || r == NULL) {
    return false;
  }
  if (l->val != r->val) {
    return false;
  }
  // 每次push进2对对称的结点
  queue.push(l->left)
  queue.push(r->right)
  queue.push(l->right)
  queue.push(r->left)
return true;
```
#### 8.层序遍历
```
// 利用队列先进后出的原则，每次push进左右结点。每次遍历一层之前，读取队列中元素个数，即为当前层的结点个数。
q.push(root)
while !q.empty():
  int n = q.size() // 即为当前层的结点数
  while n > 0:
    s = q.front()
    q.pop()
    tmp.push_back(s->val)
    if (s->left) {
      q.push(s->left)
    }
    if (s->right) {
      q.push(s->right)
    }
    --n
  ret.push_back(move(tmp))
```
#### 9.二叉树的锯齿形层序遍历
给你二叉树的根节点 root ，返回其节点值的 锯齿形层序遍历 。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。
```
// 思路1：同层次遍历，从右向左遍历时，对临时数组进行一次反转
// 思路2：使用两个栈，栈1每次从右向左入栈，栈2每次从左向右入栈，那么从栈1取出的顺序即为左向右遍历，而栈2正好相反。
```
#### 10.二叉树的深度
```
// 思路1：深度优先搜索（DFS）
// 思路2：广度优先搜索（BFS）
```
#### 11.从前序与中序遍历序列构造二叉树
```
// 前序遍历每次都认为是一个根节点
// 在中序遍历中找到该结点，
// 那么以该结点划分出其左子树和右子树的结点
// 通过结点数就能将前序遍历也能划分出左、右子树
// 从而实现递归求解
```
#### 12.从中序与后序遍历序列构造二叉树
```
// 后序遍历从后向前遍历，每个结点为根节点
// 在中序遍历中找到该节点
// 以该节点划分出根节点的左右子树
// 通过左子树或右子树结点数求出后序遍历中左右子树的集合
// 从而实现递归求解
```
#### 13.将有序数组转换为二叉搜索树
```
// 分治，每次都取区间的中间数作为一个结点。
def func(nums, l, r):
  if l > r:
    return NULL
  mid = (l + r) >> 1
  root = new TreeNode(nums[mid]);
  root->left = func(nums, l, mid - 1)
  root->right = func(nums, mid + 1, r)
  return root
```
#### 14.二叉树的高度
```
// 1.递归求解，左右子树最大高度+1
// 2.使用队列，进行广度搜索
```
#### 15.平衡二叉树
```
// 递归求高度，然后判断左右子树的高度是否满足，若不满足则返回。
```
#### 16.二叉树的最小深度
```
// 递归求高度
def func(root):
  if root == NULL:
    return 0
  l = func(root->left)
  r = func(root->right)
  if l == 0 or r == 0:
    return l + r + 1
  return min(l, r) + 1
```
#### 17.路径总和
给你二叉树的根节点 root 和一个表示目标和的整数 targetSum 。判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。如果存在，返回 true ；否则，返回 false 。
```
// 中序遍历递归
def func(root, sum):
  if root == NULL:
    return false;
  if root->val == sum && root->left == NULL && root->right == NULL:
    return true;
  return func(root->left, sum - root->val)
        or func(root->right, sum - root->val);

// 中序遍历迭代法
```
#### 18.路径总和II
求出所有路劲的集合
```
// 中序遍历迭代法，栈记录结点，根节点到当前结点的路径以及路径和
// 前序遍历递归
```

#### 19.二叉树展开为链表
```
// 递归处理左、右结点
def func(root):
  if root == NULL:
    return NULL
  left = func(root->left)
  right = func(root->fight)
  tail = left
  while (tail && tail->right):
    tail = tail->right_tree
  if tail:
    root->right = left
    tail->right = right
  else:
    root->right = right
  root->left = NULL
  return root

```

### 链表
#### 1.链表反转I
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
##### 思路
1. 非递归
2. 递归
```
// 每次让s->next->next=s，s->next=null
```

#### 2.反转链表II
给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。
```
// left至right位置进行链表反转，然后将left-1位置的next指向right位置，让left-1位置的next->next指向right+1。
```

### 排序
#### 1.颜色分类
给定一个包含红色、白色和蓝色、共 n 个元素的数组 nums ，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。
我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

##### 思路
```
// 三指针
left = 0, cur = 0, r = n - 1;
```
### 位运算

### 股票

### 技巧

### 矩阵问题
#### 1.矩阵置零
给定一个 m x n 的矩阵，如果一个元素为 0 ，则将其所在行和列的所有元素都设为 0 。请使用 原地 算法。
##### 思路
```
// 利用第0行和第0列来做标记
```
### 动态规划
#### 解码方法
一条包含字母 A-Z 的消息通过以下映射进行了 编码 ：

'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
要 解码 已编码的消息，所有数字必须基于上述映射的方法，反向映射回字母（可能有多种方法）。例如，"11106" 可以映射为：

"AAJF" ，将消息分组为 (1 1 10 6)
"KJF" ，将消息分组为 (11 10 6)
注意，消息不能分组为  (1 11 06) ，因为 "06" 不能映射为 "F" ，这是由于 "6" 和 "06" 在映射中并不等价。

给你一个只含数字的 非空 字符串 s ，请计算并返回 解码 方法的 总数 。
```
if (s[i] != '0') {
  dp[i + 1] = dp[i]; // 一个数字对应一个字符
}
if (s[i - 1] != '0' && (s[i] - '0') * 10 + s[i] - '0' < 27) {
  dp[i + 1] += dp[i - 1]; // 两个数字对应一个字符
}
if (s[i] == '0' && (s[i - 1] > '2' || s[i - 1] == '0')) {
  return 0;     // 无解的情况，直接返回0
}
```
