# queue

头文件

\#include <queue>



### front()

返回 queue 中第一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。

### back()

返回 queue 中最后一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。

### push(const T& obj)

在 queue 的尾部添加一个元素的副本。这是通过调用底层容器的成员函数 push_back() 来完成的

### pop()

删除 queue 中的第一个元素。

### size()

返回 queue 中元素的个数。

### empty()

如果 queue 中没有元素的话，返回 true。

### emplace()

用传给 emplace() 的参数调用 T 的构造函数，在 queue 的尾部生成对象。

### swap(queue<T> &other_q)

将当前 queue 中的元素和参数 queue 中的元素交换。它们需要包含相同类型的元素。也可以调用全局函数模板 swap() 来完成同样的操作。


queue<T> 模板定义了拷贝和移动版的 operator=()，对于所保存元素类型相同的 queue 对象，它们有一整套的比较运算符，这些运算符的工作方式和 stack 容器相同。