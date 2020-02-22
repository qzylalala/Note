---
title: c++关键字 const 
---

#### 1. 定义常量

```C++
const int MAX_VAL = 23;
const double Pi = 3.14;
const char* NAME = "qzylalala"
```



#### 2. 定义常量指针

* 不可通过常量指针修改其指向的内容

  ```c++
  int n, m;
  const int* p = &n;
  *p = 5;             // 编译出错
  n = 4;              // 正确
  p = &m              // 正确，常量指针的指向可以变化
  ```

*  不能把常量指针赋值给非常量指针， 反过来可以

  ```c++
  const int* p1;
  int* p2;
  // 常量指针所指向的地方尽量不要修改，因此不能赋值给非常量指针
  p1 = p2;          // 正确
  p2 = p1;          // 编译错误
  
  p2 = (int *)p1;   // 正确， 强制类型转换
  ```

* 函数指针为常量指针时， 可避免函数内部不小心改变参数指针所指地方的内容

  ```c++
  void MyPrintf(const char* p) {
  	strcpy(p, "this");       // 试图修改常量指针p指向的内容， 编译出错
      printf("%s", p);         // 正确
  }
  ```

  

#### 3. 定义常引用

 	见引用部分