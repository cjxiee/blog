###


###


###


###


### Day4
  链表与指针的实现
  双指针解决链表问题
    
    21. 合并两个有序链表 
    19. 删除链表的倒数第 N 个结点
    86. 分隔链表  双指针 在合并之前需要清理pointer 2 末端的next 避免成环
    876. 链表的中间结点 双指针 fast快一步
    141. 环形链表 从dummy开始 iterate
    23. 合并K个升序链表 用 heapq 把list里的node存进去， 然后每次pop出最小值，然后把对应node的next存入 queue，所以 queue里面需要存入node在list里对应的index。

### Day5
  滑动窗口
  
    /* 滑动窗口算法框架 */
    void slidingWindow(string s, string t) {
        unordered_map<char, int> need, window;
        for (char c : t) need[c]++;

        int left = 0, right = 0;
        int valid = 0; 
        while (right < s.size()) {
            char c = s[right];
            // 右移（增大）窗口
            right++;
            // 进行窗口内数据的一系列更新

            while (window needs shrink) {
                char d = s[left];
                // 左移（缩小）窗口
                left++;
                // 进行窗口内数据的一系列更新
            }
        }
    }


### Day6
#### 数组双指针问题
  
  leetcode704 左右指针进行二分  leetcode34 左右边界
     
     二分模版 注意区间 还有返回值的判断
    int binarySearch(int[] nums, int target) {
        int left = 0, right = ...;

        while(...) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                ...
            } else if (nums[mid] < target) {
                left = ...
            } else if (nums[mid] > target) {
                right = ...
            }
        }
        return ...;
    }
      
      
  leetcode5 回文判断 分奇偶 从中间开始判断
  
  leetcode167 两数之和 左右指针 判断大小 缩小左右边界
  
### Day7
#### 前缀和
      
      303. 区域和检索 - 数组不可变
      304. 二维区域和检索 - 矩阵不可变
#### 差分数组   
      维护一个 差分数组 
      在区间上加减 只需操作对应的index即可
      通过当前值加上前值来还愿数组
