> c专家编程 c缺陷与陷阱

https://blog.csdn.net/wxm349810930/article/details/52553578



https://blog.csdn.net/w_linux/article/details/80464866



http://c.biancheng.net/view/400.html



# 一、.string函数

### toupper tolower大小写转换
头文件：
```cpp
#include <algorithm>    // transform
```
transform 转换

```cpp
   transform(str.begin(), str.end(), str.begin(), ::toupper);
   transform(str.begin(), str.end(), str.begin(), ::tolower);
```


### string常用成员函数：
**assign函数**：

str.assign("ABC")——清空字符串，并设置为 "ABC"
str.assign("ABC",2)——清空字符串，并设置为"AB"，保留两个字符
str.assign("ABC",1,1)——清空字符串，设置为 "ABC" 中的从 位置1 开始，保留 1个 字符
str.assign(5，'A')——清空字符串，然后字符串设置为 5个 'A'
str.length()——求字符串长度
str.size()——和 length() 一样
str.capacity()——获取容量，包含了不用增加内存就能使用的字符数
str.reasize(10)——设置当前 str 的大小为10，若大小大与当前串的长度，\0 来填充
str.reasize(10,char c)——设置当前 str 的大小为10，若大小大与当前串的长度，字0符c 来填充
str.reserve(10)——设置str的容量 10，不会填充数据
str.swap(str1)——交换 str1 和 str 的字符串
str.push_back('A')——在str末尾添加一个字符  'A' ，参数必须是字符形式
str.append("ABC")——在str末尾添加一个字符串 "ABC"，参数必须是字符串形式

### insert函数方法： 

str.insert(2,3,'A')——在str下标为2的位置添加 3个 字符'A'
str.insert(2,"ABC")——在str下标为2的位置添加 字符串 "ABC"
str.insert(2,"ABC",1)——在str下标为2的位置添加 字符串 "ABC" 中 1个 字符
str.insert(2,"ABC",1,1)——在str下标为2的位置添加 字符串 "ABC" 中从位置 1 开始的 1 个字符
注：上个函数参数中加粗的 1 ，可以是 string::npos，这时候最大值，从 位置1 开始后面的全部字符

str.insert( iterator pos, size_type count, CharT ch )——在 str 中，迭代器指向的 pos位置 插入 count个 字符 ch
s4.insert(++str1.begin(),2,'a');        结果：s4：ABCD    ->    AaaBCD

str.insert( iterator pos, InputIt first, InputIt last )——在 str 中，pos位置 插入 str1 的 开始位置 到 结束为止
s4.insert(s4.begin(),str1.begin(),str1.end());        结果：s4：ABCD  str1：abc   ->    abcABCD

str.erase(2)——删除 下标2 的位置开始，之后的全删除
str.erase(2,1)——删除 下标2 的位置开始，之后的 1个 删除
str.clear()——删除 str 所有
str.replace(2,4,"abcd")——从 下标2 的位置，替换 4个字节 ，为"abcd"
str.empty()——判空

### 反转相关：
**(位于头文件<algorithm>)**

reverse(str.begin(),str.end())——str的开始 到 结束字符反转 
reverse(s4.begin(),s4.end());        结果：s4：ABCD   ->    DCBA

### 查找相关：
查找成功返回位置 ，查找失败，返回-1

**find函数：从头查找**

str.find('A')——查找 'A'
str.find("ABC")——查找 "ABC"
int n=s4.find("ABC");   s4：ABCD    ->   n = 0

str.find('B',1)——从 位置1 处，查找'B'
str.find("ABC",1,2)——从 位置1 处，开始查找 'ABC' 的前 2个 字符
rfind函数：从尾部查找

str.rfind('A')——查找 'A'
str.rfind("ABC")——查找 "ABC"
int n=s4.rfind("ABC");   s4：AAAABCD    ->   n = 3

str.rfind('B',1)——从 位置1 处，向前查找'B'
str.rfind("ABC",1,2)——从 位置1 处，开始向前查找 'ABC' 的前 2个 字符

**find_first_of()函数**：

**查找是否包含有子串中任何一个字符**

str.find_first_of("abBc")——查找 "abBc" 和str 相等的任何字符，"abBc" 中有就返回位置
str.find_first_of("abBc",1)——查找 "abBc" 和str 相等的任何字符，从 位置1 处，开始查找"abBc" 中的字符，"abBc" 中有的就返回位置
str.find_first_of("abBc",1,2)——查找 "abBc" 和str 相等的任何字符，从 位置1 处，开始查找"abBc" 的前 2个 字符，"abBc" 中有的就返回位置

**find_last_of()函数**：

find_first_not_of ()末尾查找, 从末尾处开始,向前查找是否包含有子串中任何一个字符

str.find_last_of("abBc")——查找 "abBc" 和str 相等的任何字符，向前查找，"abBc" 中有的返回位置
str.find_last_of("abBc",1)——查找 "abBc" 和str 相等的任何字符，从 位置1 处，开始向前查找"abBc" 中的字符，"abBc" 中有的就返回位置
str.find_last_of("abBc",10,2)——查找 "abBc" 和str 相等的任何字符，从 位置10 处，开始向前查找"abBc" 的前 2个 字符，"abBc" 中有的就返回位置

### 拷贝相关的：
**memcmp**
与strcpy相比，memcpy并不是遇到’\0’就结束，而是一定会拷贝完n个字节。memcpy用来做内存拷贝，你可以拿它拷贝任何数据类型的对象，可以指定拷贝的数据长度.
memcpy(d,s,strlen(s));//将s中的字符串复制到字符数组d中。
memcpy(d,s+14,4);//将s中第14个字符开始的4个连续字符复制到d中。(从0开始)

**substr**
str1=str.substr(2)——提取子串，提取出 str 的下标为2 到末尾，给 str1
str1=str.substr(2,3)——提取子串，提取出 str 的下标为2 开始，提取3个字节，给 str1

const char* s1=str.data()——将string类转为字符串数组，返回给s1
char* s=new char[10]

**copy**
str.copy(s,count,pos)——将 str 里的 pos 位置开始，拷贝 count个 字符,存到 s 里

### erase 删除
str.erase(6, 4);  // 从位置pos=6处开始，删除4个字符
    

### 比较相关的函数：

**compare函数**：完全相等返回0；完全不等返回小于0；部分相等返回大于0

示例对象：string str(“abcd”)

str.compare(“abcd”)——完全相等，返回0
str.compare(“dcba”)——返回一个小于0的值
str.compare(“ab”)——返回大于0的值
str.compare(str)——相等
str.compare(0,2,str,2,2)——用str的 下标0 开始的 2个字符 和 str的 下标2 开始的 2个 字符比较——就是用 "ab" 和 "cd”" 比较，结果小于零
str.compare(1,2,”bcx”,2)——用str的 下标1 开始的 2个字符 和 "bcx"的 前 2个 字符比较——就是用 "bc" 和 "bc”" 比较，结果是零



