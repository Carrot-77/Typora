# 二、输入

### 1.cin 

cin是C++中最常用的输入语句，当遇到空格或者回车键即停止

```cpp
#include <iostream>
#include <string>
using namespace std;
int main()
{
   chara[50];
   cin>>a; 
   cout<<a<<endl;
   return0;
}
```

输入：abcd遇回车输出abcd

缺点：只能输入没有空格的字符串，当输入中含有空格，则只能输出空格之前的字符

输入：I love China输入空格时输入并未停止，遇回车输入停止，输出I，空格后面的均未输出。

### 2. gets

可以无限读取，以回车结束读取，C语言中的函数，在C++中运行会产生bug。

```cpp
#include <iostream>
#include <cstdio>
using namespace std;
int main()
{
   chara[50];
   cin>>a;
   gets(a);
   cout<<a<<endl;
   return0;
}
```

输入：I love China回车结束输入，输出结果为love China。首字符自动丢弃。

### 3.getline()

若定义变量为string类型，则要考虑getline()函数。用法如下：

```cpp
#include <iostream>
#include <string>
using namespace std;
int main()
{
   stringa;
   getline(cin,a);
   cout<<a<<endl;
   return0;
}
```

输入：I love China回车并未结束输入，需回车两次才能结束输入，输出结果为：I love China.

### 4.cin.get cin.getline

cin.get()函数可以接收空格，遇回车结束输入。

```cpp
#include <iostream>
using namespace std;
int main()
{
   chara[50];
   cin.get(a,50);
   cout<<a<<endl;
   return0;
}
```

输入：I love China回车结束输入，输出结果为I love China。

### 5. cin.getline

cin.getline()函数可以同cin.get()函数类似，也可接收空格，遇回车结束输入。

```cpp
include <iostream>
using namespace std;
int main()
{
   chara[50];
   cin.getline(a,50);
   cout<<a<<endl;
   return0;
}
```

输入：I love China回车结束输入，输出结果为I love China。