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
      
      
### Day8
#### 二分查找的应用
    遇到单调函数，求左右边界是可以使用
    注意如何转化提议很重要
    
    1011. 在 D 天内送达包裹的能力 一个数组 求最小用多大的容器能 能在规定容器个数内实现
    410. 分割数组的最大值 一个数组 规定了容器个数 求最小的容器容量容纳这些数
    875. 爱吃香蕉的珂珂 同理 一个数组 规定了时间 求每个小时最少吃多少能在规定时间内完成

            if (nums[mid] == target) {r护额
            if (nums[mid] == target) {

### Day8
#### 二叉堆 （优先级队列） 多链表排序， 寻找最值
    
    ***第一类，排序合并***
    23. 合并 K 个升序链表   链表中的值加入优先级队列 重新链接
    373. 查找和最小的 K 对数字  虽然是两个组数进行数对排序 但可以抽象成多个链表排序的问题  如 以第一个数组的值为第一个值的多条链表。 ***
    378. 有序矩阵中第 K 小的元素 同上
    313. 超级丑数.  维护prime的链表 和丑数的链表， （ugly[index] *prime, prime, index+1) 每次pop出一个最小值 然后把对应链表prime上的下一个 丑数值添加入heapq
    
<img width="704" alt="image" src="https://user-images.githubusercontent.com/89954165/195712845-6450b1fd-8b63-461f-910f-1fdf86622e12.png">

    ***再来看第二类，寻找第 k 个最大元素这类题：***
    215. 数组中的第 K 个最大元素 维护一个size 为k的最小二叉堆 最后会留下k个最大值
    
    451. 根据字符出现频率排序 字典排序 提取key 对key进行排序 
      list(freq.keys()).sort(key = lambda x: -freq[x]) #根据value对key进行降序排列
      

