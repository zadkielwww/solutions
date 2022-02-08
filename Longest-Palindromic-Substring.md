#### 最长回文子串问题。  
  
例题：[LeetCode #5](https://leetcode-cn.com/problems/longest-palindromic-substring/)  
参考：[Link](https://leetcode-cn.com/problems/longest-palindromic-substring/solution/bao-li-zhong-xin-kuo-san-dong-tai-gui-hu-qdvv/)  
  
- #### 方法1：dp  
  
首先我们假设一个回文串的左、右边界为 [0, n]，那么当 n > 1 时 [1, n - 1] 就必定是一个回文串（回文串的定义）。  
那么我们可以使用区间 dp，枚举每个子串的左右边界 [i, j]，若 Si == Sj 且 字符串[i + 1, j - 1] 是回文串，那么 字符串[i, j] 就是一个回文串。  
枚举长度 k，左边界 l，那么转移方程就是 f[l, l + k - 1] |= (S[l] == S[l + k - 1] && f[l + 1, l + k - 2])，其中 k > 2，边界需要处理一下 k = 1 和 k = 2 的情况。  
那么时间复杂度是 O(N^2)，空间复杂度也是 O(N^2)。  
  
- #### 方法2：中心扩展算法  
  
咕了。