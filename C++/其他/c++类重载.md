# 1.map

```cpp
operator=
map& operator=( const map& other );
map& operator=( map&& other );(since C++11) 
map& operator=( map&& other ) noexcept(/* see below */);(since C++17)
map& operator=( std::initializer_list<value_type> ilist );(since C++11)
赋值运算符。将map中原来的元素全部清空后，然后将x中的元素拷贝到map中。

operator[]
T& operator[]( const Key& key );
T& operator[]( Key&& key );(since C++11)
返回对该值的引用，该值映射到一个等效于的键key，如果该键尚不存在，则执行插入。
T& operator[] ( const key_type& x ); 
当该操作作为右值的时候，会得到该键值对应的值。当该操作作为左值的时候，如果要插入的键不存在，则会将新的键值对插入到map中。如果插入的键存在，则会修改键所对应的值。

```



# 2.vector

```cpp
std::vector<T,Allocator>::operator=
vector& operator=( const vector& other );
vector& operator=( vector&& other );(since C++11) 
vector& operator=( vector&& other ) noexcept(/* see below */);(since C++17)
vector& operator=( std::initializer_list<T> ilist );(since C++11)


std::vector<T,Allocator>::operator[]
reference operator[]( size_type pos );(until C++20)
constexpr reference operator[]( size_type pos );(since C++20)
const_reference operator[]( size_type pos ) const;(until C++20)
constexpr const_reference operator[]( size_type pos ) const;(since C++20)
/*
operator[]和at的主要区别在于operator[]不做边界检查，而at会做边界检查。
由于operator[]不做边界检查， 那怕越界了也会返回一个引用，当然这个引用是错误的引用，如何不小心调用了这个引用对象的方法，会直接导致应用退出。
而由于at会做边界检查，如果越界，会抛出异常，应用可以try catch这个异常，应用还能继续运行。
*/

template <class T, class Alloc>
bool operator== (const vector<T,Alloc>& lhs, const vector<T,Alloc>& rhs);	Relational operators for vector
template <class T, class Alloc>
bool operator!= (const vector<T,Alloc>& lhs, const vector<T,Alloc>& rhs);
template <class T, class Alloc>
bool operator<  (const   vector<T,Alloc>& lhs, const vector<T,Alloc>& rhs);
template <class T, class Alloc>
bool operator<= (const vector<T,Alloc>& lhs, const vector<T,Alloc>& rhs);
template <class T, class Alloc>
bool operator>  (const vector<T,Alloc>& lhs, const vector<T,Alloc>& rhs);
template <class T, class Alloc>
bool operator>= (const vector<T,Alloc>& lhs, const vector<T,Alloc>& rhs);

```



# 3.stack

```cpp
std::stack<T,Container>::operator=

stack& operator=( const stack& other );
stack& operator=( stack&& other );(since C++11)
/*
1）复制分配运算符。 用其他内容替换内容。调用c = other.c;。 （隐式声明）
2）移动分配运算符。 使用移动语义将内容替换为其他内容。c = std :: move（other.c）; （隐式声明）
*/

operator==,!=,<,<=,>,>=,<=>(std::stack)

template< class T, class Container >
bool operator==( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );

template< class T, class Container >
bool operator!=( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );

template< class T, class Container >
bool operator<( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );

template< class T, class Container >
bool operator<=( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );

template< class T, class Container >
bool operator>( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );

template< class T, class Container >
bool operator>=( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );

template< class T, std::three_way_comparable Container >
std::compare_three_way_result_t<Container>
operator<=>( const std::stack<T,Container>& lhs, const std::stack<T,Container>& rhs );
/*
比较两个容器适配器的基础容器的内容。 通过将相应的运算符应用于基础容器来完成比较。
*/

```



# 4.queue

```cpp
std::queue<T,Container>::operator=

queue& operator=( const queue& other );
queue& operator=( queue&& other );(since C++11)
/*
1）复制分配运算符。 用其他内容替换内容。调用c = other.c;。 （隐式声明）
2）移动分配运算符。 使用移动语义将内容替换为其他内容。c = std :: move（other.c）; （隐式声明）
*/

/*
比较两个容器适配器的基础容器的内容。 通过将相应的运算符应用于基础容器来完成比较。
*/
operator==,!=,<,<=,>,>=,<=>(std::queue)

bool operator==( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

bool operator!=( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

bool operator<( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

bool operator<=( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

bool operator>( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

bool operator>=( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

std::compare_three_way_result_t<Container>
operator<=>( const std::queue<T,Container>& lhs, const std::queue<T,Container>& rhs );

```



# 5.map

```cpp
std::set<Key,Compare,Allocator>::operator=

set& operator=( const set& other );
set& operator=( set&& other );(since C++11) (until C++17)
set& operator=( set&& other ) noexcept(/* see below */);(since C++17)
set& operator=( std::initializer_list<value_type> ilist );(since C++11)
/*
1）复制分配运算符。将内容替换为其他内容的副本。如果std :: allocator_traits <allocator_type> :: propagate_on_container_copy_assignment :: value为true，则将目标分配器替换为源分配器的副本。如果目标分配器与源分配器的比较不相等，则使用目标分配器（* this）分配内存，然后在复制元素之前使用Other的分配器分配内存。 （自C ++ 11起）。
2）移动分配运算符。使用移动语义将内容替换为其他内容（即，其他中的数据从另一个中移入此容器）。之后，另一个处于有效但未指定的状态。如果std :: allocator_traits <allocator_type> :: propagate_on_container_move_assignment :: value为true，则将目标分配器替换为源分配器的副本。如果为false，并且源分配器和目标分配器的比较不相等，则目标无法获得源内存的所有权，必须单独移动每个元素，并根据需要使用其自己的分配器分配其他内存。在任何情况下，* this中最初存在的所有元素都会被破坏，或被逐元素移动分配所替代。
3）用初始化列表ilist标识的内容替换内容。
*/

operator==,!=,<,<=,>,>=,<=>(std::set)
  C++  Containers library std::set 
Defined in header <set>
template< class Key, class Compare, class Alloc >
bool operator==( const std::set<Key,Compare,Alloc>& lhs,
                 const std::set<Key,Compare,Alloc>& rhs );
(1)	
template< class Key, class Compare, class Alloc >
bool operator!=( const std::set<Key,Compare,Alloc>& lhs,
                 const std::set<Key,Compare,Alloc>& rhs );
(2)	(until C++20)
template< class Key, class Compare, class Alloc >
bool operator<( const std::set<Key,Compare,Alloc>& lhs,
                const std::set<Key,Compare,Alloc>& rhs );
(3)	(until C++20)
template< class Key, class Compare, class Alloc >
bool operator<=( const std::set<Key,Compare,Alloc>& lhs,
                 const std::set<Key,Compare,Alloc>& rhs );
(4)	(until C++20)
template< class Key, class Compare, class Alloc >
bool operator>( const std::set<Key,Compare,Alloc>& lhs,
                const std::set<Key,Compare,Alloc>& rhs );
(5)	(until C++20)
template< class Key, class Compare, class Alloc >
bool operator>=( const std::set<Key,Compare,Alloc>& lhs,
                 const std::set<Key,Compare,Alloc>& rhs );
(6)	(until C++20)
template< class Key, class Compare, class Alloc >
/* see below */ operator<=>( const std::set<Key,Compare,Alloc>& lhs,
                             const std::set<Key,Compare,Alloc>& rhs );
(7)	(since C++20)
/*
比较两组内容。

1-2）检查lhs和rhs的内容是否相等，即它们具有相同数量的元素，并且lhs中的每个元素在同一位置与rhs中的元素进行比较。
3-6）从字典上比较lhs和rhs的内容。比较由等效于std :: lexicographical_compare的函数执行。此比较将忽略集合的排序比较。
7）从字典上比较lhs和rhs的内容。就像通过在两个集合上调用std :: lexicographical_compare_three_way并使用函数对象执行合成的三向比较（参见下文）来执行比较。返回类型与合成三向比较的结果类型相同。此比较将忽略集合的排序比较。
给定两个常量E lvalues lhs和rhs分别作为左操作数和右操作数（其中E为Key），则合成的三向比较定义为：

如果满足std :: three_way_comparable_with <E，E>，等于lhs <=> rhs;
否则，如果通过operator <比较两个const E lvalues的格式正确，并且结果类型满足boolean-testable，则等于
lhs <rhs吗？ std :: weak_ordering :: less：
rhs <lhs？ std :: weak_ordering ::更大：
            std :: weak_ordering ::等效
否则，未定义综合三向比较，并且operator <=>不参与重载解析。
如果满足three_way_comparable_with或boolean-testable但未建模，则未定义operator <=>的行为，或者使用operator <但E和<不建立总顺序。
*/
```