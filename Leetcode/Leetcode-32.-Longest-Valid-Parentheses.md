---
title: Leetcode  32. Longest Valid Parentheses
---

### 1. 问题描述

```markdown
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.
```

```markdown
Example 1:
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

```markdown
Example 2:
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
```

 [原题链接](https://leetcode.com/problems/longest-valid-parentheses/)



### 2. 题解代码

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        int n = s.length(), longest = 0;
        stack<int> tmp;
        for (int i = 0; i < n; i++) {
            if (s[i] == '(') 
                tmp.push(i);
            else {
                if (!tmp.empty()) {
                    if (s[tmp.top()] == '(') 
                        tmp.pop();
                    else tmp.push(i);
                }
                else 
                    tmp.push(i);
            }
        }
        if (tmp.empty()) 
            longest = n;
        else {
            int a = n, b = 0;
            while (!tmp.empty()) {
                b = tmp.top(); 
                tmp.pop();
                longest = max(longest, a - b - 1);
                a = b;
            }
            longest = max(longest, a);
        }
        return longest;
    }
};
```



### 3. 代码思路分析

* 第一部分

  ```c++
  for (int i = 0; i < n; i++) {
              if (s[i] == '(') 
                  tmp.push(i);
              else {
                  if (!tmp.empty()) {
                      if (s[tmp.top()] == '(') 
                          tmp.pop();
                      else tmp.push(i);
                  }
                  else 
                      tmp.push(i);
              }
          }
  ```

  扫一遍`string`

  1. 如果遇到`'('`则将其对应的索引`i`入栈
  2. 如果遇到`')'`  （栈空直接将索引`i`入栈）
     1. 若此时栈顶的索引所对应的字符为`'('`，我们就找到了一对匹配的字符，则出栈
     2. 否则， 我们将这个`'('`对应的索引`i`入栈



* 第二部分

  ```c++
  if (tmp.empty()) 
              longest = n;
          else {
              int a = n, b = 0;
              while (!tmp.empty()) {
                  b = tmp.top(); 
                  tmp.pop();
                  longest = max(longest, a - b - 1);
                  a = b;
              }
              longest = max(longest, a);
          }
  ```

  这里其实是解题思路的体现， 在第一部分操作结束后， 此时的栈中元素为那些无法matching的字符的索引(而且是递增的)， 此时栈中两相邻索引之间的索引所对应原`string`的部分就是一个__Valid Parentheses__。栈中相邻两索引设为a， b， 则`a - b - 1`是长度， 选择其中最大的即为所求

