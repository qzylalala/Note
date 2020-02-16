---
title:Leetcode  42. Trapping Rain Water
---

### 1. 问题描述

```markdown
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.
```

```markdown
Example:
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

 ```markdown
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. 
 ```

[原题链接](https://leetcode.com/problems/trapping-rain-water/)



### 2. 题解代码

```c++
class Solution {
public:
    int trap(vector<int>& A) {
        int left = 0; int right = A.size() - 1;
        int res = 0;
        int maxleft = 0, maxright = 0;
        while(left <= right){
            if(A[left] <= A[right]){
                if(A[left] >= maxleft) 
                    maxleft = A[left];
                else 
                    res += maxleft-A[left];
                left++;
            }
            else{
                if(A[right] >= maxright) 
                    maxright = A[right];
                else 
                    res += maxright-A[right];
                right--;
            }
        }
        return res;
    }
};
```



### 3. 代码思路分析

* 首先这个图对分析问题很友好。可以看出，**处于极大位置的`height`对于计算`result`起到关键作用**。最终的`result`由所有相邻的两个极大之间能放的`area`之和构成
* 注意到`the width of each bar is 1`，两极大之间各个`bar`对`result`的贡献为`min(左极大， 右极大) - 该bar的height`
* 一个简单的想法是，从左到右一路读过去标识出极大值，计算出答案。这里选择从左，右同时向中间读取，代码会更简洁(不过效率似乎差不多)