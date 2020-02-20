---
title: Inverse Cascade
---

同样是`cs61a`课上的比较漂亮的代码，记录一下

```python
def inverse_cascade(n):
    grow(n)
    print(n)
    shrink(n)
    
def f_then_g(f, g, n):
    if n:
        f(n)
        g(n)

grow = lambda n: f_then_g(grow, print, n//10)
shrink = lambda n: f_then_g(print, shrink, n//10)

inverse_cascade(1234)
```



同样附上 [链接](http://pythontutor.com/visualize.html#mode=edit) 自己跑一下

