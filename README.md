# LeetCode
##### 11. 盛最多水的容器
  双指针，指向收尾，收缩
  
  
  收缩时考虑短板
  
  
  res = height[i] < height[j] ? 
                Math.max(res, (j - i) * height[i++]): 
                Math.max(res, (j - i) * height[j--]); 
                
---
##### 17. 电话号码的字母组合
  循环层数不确定，因此采用DFS来处理循环，到达末尾的条件用index做判断
  
---
##### 22. 括号生成
  采用DFS处理，若左括号剩余数量>0，直接DFS,加入右括号的条件为左括号数量小于右括号，否则为无效括号序列
  与T17的处理方法不同，即未采用for循环是因为，每次不一定加入一个右括号，而T17每次必定加入一个符号
  
---
##### 1139. 最大的以 1 为边界的正方形
  动态规划,dp[i][j][0]表示左侧连续1的个数，dp[i][j][1]表示上侧连续1的个数，因此可能的最大边长为min(dp[i][j][0],dp[i][j][1])，探测边长，若不满足条件则--后再次探测，探测条件为正方形的左下顶点的上侧连续1的个数和右上顶点的左侧连续1的个数。

  dp方程为：
  dp[i][j][0] =  dp[i][j-1][0]
  dp[i][j][1] =  dp[i-1][j][1]
  ，if(grid[i][j]==1)
  
---
##### 面试题 08.11. 硬币
  动态规划，完全背包
  
  dp[i][j]表示用前i个硬币，换总价值为j的所有结果，注意，dp[i][0]初始化为1
  
  dp[i][j] = dp[i-1][j],if j<value[i]
             dp[i-1][j]+dp[i][j-value[i]],if j>=value[i] (不选或选)
             
---
##### 1333. 餐厅过滤器
  结构体的快排，注意比较函数，小于代表从大到小排，大于代表从小到大排
  
---
##### 148. 排序链表
  链表排序，O(nlogn) O(1)空间，归并排序。
  
  找到中点的方法和尺取有异曲同工之妙。
  
---
##### 324. 摆动排序 II
  一开始的思路是从小到大进行排序，后半部分插入到前半部分。（注意vector的变化，size+1，插入后删除）
  存在的问题是，前半部分和后半部分的交界处若存在相同的元素，例如[1,2,2,3,3],会存在相等的情况
  改变思路，从大到小排序，这样插入尽可能使中间相等的元素分开
  算法可以更优...
  
---
##### 面试题 16.26. 计算器
  操作符栈和操作数栈
  
  扫描到操作符，计算前面所有*同等级和更高级*的操作符对应的表达式；扫描到操作数，循环扫描（注意不要扩到大循环范围，使用DFA会很麻烦，直接扫描到非数字结束）
  
  简单做法：
  
  只需要一个操作数栈。碰到乘除符号，由于为最高优先级，直接计算出结果；遇到负号，向操作数栈中加入-num。扫描完毕后，使用while循环计算出栈中所有数的和。

---
##### 1177. 构建回文串检测
  任意顺序的回文串，处理类似与“找到唯一一个出现奇数次的数字”，将每一个字符看作一个数字。由于此题需要处理很多遍，选择将扫描的结果记录下来，dp[i][j]表示第i个位置之前第j个字母出现的次数
  
  if s[i-1]-'a' == j  s[i][j] = s[i-1][j]+1;
  else  s[i][j] = s[i-1][j];

  每次查询的时候，字串的字母表情况为 s[end+1][j]-s[start][j]，偶数的消去，奇数的记录下来
  
  累计为奇数，为2k+1，则k=n即可变为回文串；累计为偶数，为2k，则n=k可变为回文串

---
##### 151. 翻转字符串里的单词
  识别字符串压栈，扫描结束后出栈，空间O(n)

  不占空间的做法为，先将整个字符串反转，然后将单词反转。空间O(1)
  
---
##### 951. 翻转等价二叉树
  对于两个指针，有两种情况，指向的值不等，返回false，相等的话，返回叶子结点的情况，翻转和不翻转

---
##### 1367. 二叉树中的列表
  BFS找到所有可能的起点，DFS找到终点。

---
##### 894. 所有可能的满二叉树
  递归处理。左侧i课子树的结果和右侧i颗子树的结果做双重循环，交换左右子树再保存一次，减少循环时间。
  另外，可以采用动态规划的思想，由于递归过程中有很多相同的结果，将这些结果记录下来，空间换时间

---
##### 652. 寻找重复的子树

>序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

有了序列化的思想之后，这道题目就迎刃而解了。遍历每一颗子树，生成对应的序列，在map中查找，次数为2，则加入ans中

---
##### 654. 最大二叉树
  每次找最大值的索引，左右两边再次递归。tip:为省空间和时间，每次传递left和right，而不是传递一个新的vector（新建对象耗时且占空间）
  
---
##### 1104. 二叉树寻路
  正常的二叉树的父节点 = 子节点/2. 而Z型的二叉树还存在一个对称的关系，即子节点/2 = sum - 父节点，sum的值为父亲节点所在层的任意两个字节之和。从叶子寻根，递归。

---
##### 1110. 删点成林
  遍历候选队列中的根节点，若其值在待删除的vector中则将子树加入候选队列，否则将树根加入结果中，并遍历整个树，不断处理子树
  
---
##### 1026. 节点与其祖先之间的最大差值
  就一个节点来说的最大差值，就是祖先的最大值或者最小值和自己的val的差值。记录祖先节点的最大最小值，并在调用时传递
  
---
##### 剑指 Offer 26. 树的子结构
  对于一个结点A来说，满足条件的情况有三种
  * A结点为B的结构的根节点 此种情况递归检查，A空false，B空true，值不等false，值等继续判断孩子
  * A的左孩子为B的结构的根节点
  * A的右孩子为B的结构的根节点
  
---
##### 863. 二叉树中所有距离为 K 的结点
  * 方法1：先DFS，map记录所有结点的父节点。从目标节点开始左右孩子，parent进行DFS。层次化遍历有两种方法：记录队列的大小，一个while里遍历某一层的数量，或者在每一层中间插入nullptr，到达相同的效果
  * 方法2：分为两棵树，一个棵树以目标节点为根节点，距离K，一棵树以目标节点的父亲为根节点，距离为K-1
  
---
##### 面试题 04.08. 首个共同祖先
  考虑三种情况
  * 结点p和结点q分别位于root的两侧，因此left和right均不为空，返回root
  * 结点p和结点q位于root的一侧，因此left和right只有一个不为空，返回非空结点
  * 结点p或结点q为root，直接返回root
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
