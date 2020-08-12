---
title: push_back与replace_back
---

 ### 主要区别

​	使用push_back()向容器中加入一个右值元素(临时对象)时，首先会调用构造函数构造这个临时对象，然后需要调用拷贝构造函数将这个临时对象放入容器中。原来的临时变量释放。这样造成的问题就是临时变量申请资源的浪费。 
​	引入了右值引用，转移构造函数后，push_back()右值时就会调用构造函数和转移构造函数,如果可以在插入的时候直接构造，就只需要构造一次即可。这就是c++11 新加的emplace_back。



### 代码观察

运行以下代码可以很清晰地观察到两者地不同

```c++
#include <iostream>
#include <cstring>
#include <vector>

using namespace std;

class A {
public:
    A(int i) {
        cout << "constructor function " << i << endl;
    }
    ~A(){};
    A(const A& other) : str(other.str){
        cout << "copy construct " << endl;
    }

public:
    string str;
};
 
int main()
{
    vector<A> vec;
    vec.reserve(10);
    for(int i=0;i<10;i++){
        //vec.push_back(A(i)); //调用了10次构造函数和10次拷贝构造函数,
        vec.emplace_back(i);  //调用了10次构造函数一次拷贝构造函数都没有调用过
    }
    system("pause");
}
```

