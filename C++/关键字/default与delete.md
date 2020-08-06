https://blog.csdn.net/a1875566250/article/details/40406883?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param



# default关键字

首先我们有一个字符串类：

```cpp
class CString{   
    char* _str;

public:
   //构造函数
    CString(const char* pstr) : _str(nullptr) {
       UpdateString(pstr);
    }
	//析构函数
    ~CString()  {
        if (_str)
          free(_str);
    }

public:
    void UpdateString(const char* pstr) throw()  {
        if (pstr == nullptr)
            return;
        if (_str)
            free(_str);
        _str = (char*)malloc(strlen(pstr) + 1);
        strcpy(_str,pstr);
    }

public:
    char* GetStr() const throw() {
        return _str;
    }
};
```

我们可以这样使用：

```cpp
auto str = std::make_unique<CString>("123");

printf(str->GetStr());
```

但是这样是不行的：

```cpp
auto str = std::make_unique<CString>(); //失败，因为没有一个无参构造函数
```


好，我们用default来

```cpp
class CString{
    char* _str = nullptr;

public:
    CString() = default;

public:
    //构造函数
    CString(const char* pstr) : _str(nullptr){      
        UpdateString(pstr);
   }

    //析构函数
	 ~CString(){
        if (_str)            free(_str);
    }
public:
    void UpdateString(const char* pstr) throw() {
        if (pstr == nullptr)
           return;
        if (_str)
            free(_str);
        _str = (char*)malloc(strlen(pstr) + 1);
        strcpy(_str,pstr);
    }
public:
    char* GetStr() const throw(){
        return _str;
    }
};
```


于是我们可以这样使用了：

```cpp
auto str_def = std::make_unique<CString>();

str_def->UpdateString(“123”);
printf(str_def->GetStr() == nullptr ? "None":str_def->GetStr());
```

# delete关键字

假设我们有这样一个类，这个类是用于自动申请内存，进行RAII式管理：
（避免麻烦那些什么拷贝构造拷贝赋值移动构造什么的就不写了）

```cpp
template<typename T>
class CStackMemoryAlloctor{
    mutable T* _ptr;

public:
   explicit CStackMemoryAlloctor(size_t size) throw() : _ptr(nullptr){
        _ptr = (T*)malloc(size);
    }
    ~CStackMemoryAlloctor(){
        if (_ptr)
            free(_ptr);
    }

public:
   operator T*() const throw() {
        T* tmp = _ptr;
        _ptr = nullptr;
       return tmp;
    }

public:
    T* GetPtr() const throw(){
        return _ptr;
    }
};
```


我们这样使用这个类：

```cpp
CStackMemoryAlloctor<wchar_t> str(128);
wchar_t* pstr = str.GetPtr();
wcscpy(pstr,L"123\n");
wprintf(pstr);
```


但是别人也可以这样使用：

```cpp
auto p = std::make_unique<CStackMemoryAlloctor<wchar_t>>(128);
```


因为这个类依然可以进行默认new，我们不想让人家进行new怎么办，老办法就是这样：

```cpp
private:
    void* operator new(std::size_t)
    {
        return nullptr;
    }
```

把new设置为private了，就行了，但是这样如果别人尝试new，那看到的错误提示简直惨不忍睹。。。
于是C11的delete人性化多了：

```cpp
public:
    void* operator new(std::size_t) = delete;
```


当尝试new的时候，提示十分友好，这个方法已被删除。
这个delete可以用来删任何你不爽的东西，比如拷贝构造，赋值拷贝什么鸡巴毛的东西。