# map



## map简介

map是STL的一个关联容器，它提供一对一的hash。

第一个可以称为关键字(key)，每个关键字只能在map中出现一次；
第二个可能称为该关键字的值(value)；

map以模板(泛型)方式实现，可以存储任意类型的数据，包括使用者自定义的数据类型。Map主要用于资料一对一映射(one-to-one)的情況，map內部的实现自建一颗红黑树，这颗树具有对数据自动排序的功能。在map内部所有的数据都是有序的，后边我们会见识到有序的好处。比如一个班级中，每个学生的学号跟他的姓名就存在著一对一映射的关系。

## map的功能

自动建立key － value的对应。key 和 value可以是任意你需要的类型。



## 头文件

> #include <map>



## map的构造

map<int, string> mapName;



## map的使用



### 插入

* 用insert函數插入pair

  > mapName.insert(pair<int, string>(000, "student_zero"));

* 第二种 用insert函数插入value_type数据

  > mapName.insert(map<int, string>::value_type(001, "student_one"));

* 第三种 用"array"方式插入

  > mapName[123] = "student_first";

### 查找

find()

### 删除

erase

### 大小

size



### 关键字

   begin()     返回指向map头部的迭代器

   clear(）    删除所有元素

   count()     返回指定元素出现的次数

   empty()     如果map为空则返回true

   end()      返回指向map末尾的迭代器

   equal_range()  返回特殊条目的迭代器对

   erase()     删除一个元素

   find()     查找一个元素

   get_allocator() 返回map的配置器

   insert()    插入元素

   key_comp()   返回比较元素key的函数

   lower_bound()  返回键值>=给定元素的第一个位置

   max_size()   返回可以容纳的最大元素个数

   rbegin()    返回一个指向map尾部的逆向迭代器

   rend()     返回一个指向map头部的逆向迭代器

   size()     返回map中元素的个数

   swap()      交换两个map

   upper_bound()  返回键值>给定元素的第一个位置

   value_comp()   返回比较元素value的函数





## 举例

```c++
#include <iostream>
#include <map>

using namespace std;

int main() {
    map<double, string> arr;
    arr[1.2] = "hello";
    arr[4.3] = "world";
    arr[-3.22] = "carrot";
    arr[121.1] = "world";
    for (auto iter = arr.begin(); iter != arr.end(); iter++) {
        cout << iter->first << " " << iter->second << endl;
    }


    double n;
    while (cin >> n) {
        if (n == 0) break;
        if (arr.find(n) != arr.end()) {
            cout << "find : " << arr[n] << endl;
        } else {
            cout << "NOT FOUND" << endl;
        }
    }
    return 0;
}

```

