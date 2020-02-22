#### 1. string初始化

* `string`类是模板类：`typedef basic_string<char> string`

* 使用`string`类要包含头文件 `<string>`

* `string`对象初始化的方法

  ```markdown
  1. string s1("Hello");
  2. string month = "March";
  3. string s2(8, 'x');
  
  note:可以将字符赋值给string对象
       string s = 'c'   // 错误，不能用字符来初始化
       
       string s;
       s = 'n'          // 正确
  ```



#### 2. string的基本操作

* `string`对象的长度用成员函数`length()`读取；

  ``` c++
  string s("Hello");
  cout << s.length() << endl;   // 5 
  ```

* `string`类支持流读取运算符

  ```c++
  string stringObject;
  cin >> stringObject;
  ```

* `string`支持`getline()`函数读取

  ```c++
  string s;
  getline(cin, s);   // 读取一整行，赋值给s
  ```

* `string`赋值语句

  ```c++
  string s1("cat"), s2;
  s2 = s1;              // '='赋值
  s2.assign(s1)         // assign成员函数赋值
  s2.assign(s1, 1, 3)   // 从s1中下标为1的字符开始复制3个字符给s2
  ```

* 逐个访问`string`对象中的字符

  ```c++
  string s1("Hello");
  for (int i = 0; i < s1.length(); i++) {
      cout << s1.at(i) << endl;
  }
  // 成员函数 at 会做范围检查，若超出范围，会抛出 out_of_range 异常 
  ```

* `string`的连接

  ```c++
  string s1("good"), s2(" morning");
  
  // 1. 用 + 运算符连接字符串
  s1 += s2;                      //s1 : "good morning"
  // 2. 用成员函数 append 连接字符串
  s1.append(s2);                 //s1 : "good morning"
  
  s2.append(s1, 3, s1.size());   //从下标为3开始，s1.size()字符，字符串内没有
                                 //足够字符时， 则复制字符串最后一个字符
  ```

* `string` 的比较

  ```markdown
  1. 用关系运算符比较 string的大小， 返回值都是 bool 类型
  string s1("hello"), s2("hello), s3("hell");
  bool b = (s1 == s2);           // true
  bool b = (s1 == s3);           // false
  bool b = (s1 > s3);            // true
  bool b = (s1 != s3);           // true
  
  2. 用成员函数 compare 比较 string 的大小
  string s1("hello"), s2("hello), s3("hell");
  int f1 = s1.compare(s2);                  // 0
  int f2 = s1.compare(s3);                  // 1
  int f3 = s1.compare(s1);                  // -1
  int f4 = s1.compare(1, 2, s3, 0, 3);      // -1   s1 1-2; s3 0-3
  int f5 = s1.compare(0, s1.size(), s3);    // 1    s1 0-end
  ```

* `string` 的子串 `substr` 函数

  ```c++
  string s1("hello world"), s2; 
  s2 = s1.substr(4, 5);         // 从下标4开始 数5个字符
  cout << s2 << endl;           // "o wor"
  ```

* `string`交换 `swap`函数

  ```c++
  string s1("hello, world"), s2("really");
  s1.swap(s2);  // s1 与 s2 交换
  ```

* 寻找`string`中的字符 `find` `rfind` `find_first_of` `find_last_of`函数

  ```c++
  string s1("hello, world");
  s1.find("lo");   // 在 s1 中查找 "lo" 第一次出现的地方。
  				 // 若找到， 返回"1o"开始的位置， 否则返回 string::npos
  s1.find("ll", 1) // 第二个参数可以指定开始查找的位置
      
  s1.rfind("lo");  // 从后往前找， 其它与 find 函数一样
  
  s1.find_first_of("abcd");//查找 "abcd" 中任何一个字符第一次出现的地方
                           //若找到则返回找到字符的位置,否则返回string::npos
  s1.find_last_of("abcd"); //查找 "abcd" 中任何一个字符最后一次出现的地方
  						 //若找到则返回找到字符的位置,否则返回string::npos
  ```

* 删除`string`中的字符  `erase`函数

  ```c++
  string s1("Hello world");
  s1.erase(5);           // 去掉下标5及之后的字符  s1 -> hello
  s1.length();           // -> 5
  ```

* 替换`string`中的字符  `replace`函数

  ```c++
  string s1("Hello world");
  s1.replace(2, 3, "haha");      // 将s1中下标2开始的 3个字符换成 "haha"
  							   // s1 -> "hehaha world" 
  
  s1.replace(2, 3, "haha", 1, 2) //将s1中下标2开始的 3个字符换成 "haha" 中下标 1开始的2个字符
                                 // s1 -> heah world
  ```

* 在`string` 中插入字符 `insert`函数

  ```c++
  string s1("Hello world");
  string s2("show insert");
  s1.insert(5, s2);       //将s2插入s1下标5的位置 s1 -> "helloshow insert world"
  
  s1.insert(2, s2, 5, 3); //将s2中下标5开始的3个字符插入s1下标2的位置 
                          //s1 -> "heinsllo world"
  ```

* 将`string`转换成 c语言式 字符串  `c_str`  `data`函数

  ```c++
  string s1("hello world");
  printf("%s\n", s1.c_str());   // c_str()函数,返回传统的const char* 类型的字符串， 以'\0'结尾
  const char* p1 = s1.data();   // data函数返回char* 类型的字符串，对s1的修改可能会使p1出错
  for (int i = 0; i < s1.length(); i++) {
      printf("%c", *(p1 + 1));
  }
  // -> "hello world"
  ```



#### 3. 字符串流处理

* 字符串输入流 `istringstream`

  ```c++
  string input("Input test 123 4.7 A");
  istringstream inputString(input);
  string string1, string2;
  int i; double d; char c; long L;
  inputString >> string1 >> string2 >> i >> d >> c;
  // string1 -> Input
  // string2 -> test
  // i -> 123
  // d -> 4.7
  // c -> A
  if(inputString >> L) {
  	cout << "long\n";
  }
  else {
  	cout << "empty\n"; 
  }                              // 输出 -> empty
  ```

* 字符串输出流 `ostringstream`

  ```c++
  ostringstream outputString;
  int a = 10;
  outputString << "This" << a << "ok" << endl;
  cout << outputString.str();
  // 输出 -> This 10ok
  ```

  

