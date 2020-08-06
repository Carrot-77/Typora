## auto用法



<font color=blue>auto 变量必须在定义时初始化，这类似于const关键字</font>



```c++
using namespace std;

//不能用于非静态的成员变量

//4.可以用于静态成员变量在内部初始化
class A {
public:
    static const auto x = 123;
};

//不能作为模板变量
/* int f(auto x, auto y) { */
/*     return x + y; */
/* } */

//1-3必须在编译期可以辨别变量类型
int main() {
    auto a = 123;
    //1.自动变量辨认
    cout << sizeof(a) << endl;
    map<int, int> arr;
    arr[23333] = 2;
    arr[233] = 9898;
    arr[999] = 10000;
    //2.遍历容器
    //for (map<int, int>::iterator iter = arr.begin(); iter != arr.end(); iter++) {
    for (auto iter = arr.begin(); iter != arr.end(); iter++) {
        cout << iter->first << " " << iter->second << endl;
    }
    //3.c++11for新用法
    for (auto x : arr) {
        cout << x.first << ", " << x.second << endl;
    }
    return 0;
}
```





## const



const修饰函数时还会参与到函数的重载中，即通过const对象、const指针或引用调用方法时，优先调用const方法。



<font color=blue>const 运行期常量</font>

```c++
int a = 10;
int &b = a;
 
auto c = b;//c的类型为int而非int&（去除引用）
auto &d = b;//此时c的类型才为int&
 
c = 100;//a =10;
d = 100;//a =100;
```



```c++
const int a1 = 10;
auto  b1= a1; //b1的类型为int而非const int（去除const）
const auto c1 = a1;//此时c1的类型为const int
b1 = 100;//合法
c1 = 100;//非法
```



```c++
const int a2 = 10;
auto &b2 = a2;//因为auto带上&，故不去除const，b2类型为const int
b2 = 10; //非法
```





## consexpr

<font color=blue>constexpr 严格的编译期常量</font>



* constexpr所修饰的变量一定是编译期可求值的，所修饰的函数在其所有参数都是constexpr时，一定会返回constexpr。

* constexpr还能用于修饰类的构造函数，即保证如果提供给该构造函数的参数都是constexpr，那么产生的对象中的所有成员都会是constexpr，该对象也就是constexpr对象了，可用于各种只能使用constexpr的场合。注意，constexpr构造函数必须有一个空的函数体，即所有成员变量的初始化都放到初始化列表中。



**constexpr的好处：**

1. 是一种很强的约束，更好地保证程序的正确语义不被破坏。
2. 编译器可以在编译期对constexpr的代码进行非常大的优化，比如将用到的constexpr表达式都直接替换成最终结果等。
3. 相比宏来说，没有额外的开销，但更安全可靠。



```c++
using namespace std;

//constexpr用来修饰普通函数
//c++11不支持constexpr递归
constexpr int f(int x) {
    return 3 * x;
}

class A {
public:
    //constexpr用来修饰构造函数
    constexpr A(int x, int y) : x(x), y(y) {}
    int x, y;
};

int main() {
    int n;
    cin >> n;

    //const 运行期常量
    //constexpr 严格的编译期常量
    //错误示范 constexpr int m = 2 * n;
    //正确表达 constexpr int m = 2 * 2;

    const int m = 2 * n;
    cout << m << endl;
    
    //使用constexpr
    constexpr int k = f(3);
    cout << k << endl;
    
    constexpr A a(2, 3);
    cout << "a.x = " << a.x << ", a.y = " << a.y << endl;

    return 0;
}
```



## final



**作用**

* final防止子类对父类方法的重写

* final防止类再被继承



```c++
class A : public map<int, int> {
public:
    virtual void say() {
        cout << "Class A : hello" << endl;
    }
};

//2.final防止类再被继承
class B final: public A{
    //1.final防止子类对父类方法的重写
    void say() final override {
        cout << "Class B : caaaaaaat" << endl;
    }
};

//错误示范: 无法继承final类
/* //错误示范：无法重写final方法 */
/* class C : public B { */
/* public: */
/*     void say() override { */
/*         cout << "Class C : I'm C!" << endl; */
/*     } */
/* }; */


int main() {
    A a;
    a[2333] = 332;
    a[3333] = 22222;
    for (auto iter : a) {
        cout << iter.first << " " << iter.second << endl;
    }
    return 0;
}
```





## nullptr与NULL



* nullptr <- 地址 
* NULL <- 0 当成地址，实际是(void*)0



```c++
int f(int x) {
    cout << "output int value : " << endl;
    cout << x << endl;
    return 0;
}

int f(int *x) {
    cout << "output address : ";
    cout << x << endl;
    return 0;
}

int main() {
    printf("%lld", (long long)nullptr);
    cout << NULL << endl;
    int n = 123, *p = &n;
    f(n);
    f(p);
    f(nullptr);    
    // nullptr <- 地址
    f((int)NULL);       
    // NULL <- 0 当成地址
    //实际是(void*)0
    return 0;
}

```



**输出**

```
00
output int value : 
123
output address : 0x7ffe166ec43c
output address : 0
output int value : 
0
```





## 左值与右值

<font color=blue>左值优先左值引用，右值优先右值引用</font>



```c++
//只要能放在等号左边都是左值
//左值：同样的变量，单一的方式，同样的结果
//右值：表临时,不能放在等号左边
int main() {
    int a;
    //a左值 123+456右值
    a = 123 + 456;

    int x, y = 1, z = 3;
    //xy左值
    x = y;
    //y+z右值
    x = y + z;

    x++;//表达式右值
    ++x;//表达式左值
    
    //(x = y); ->赋值表达式为左值
    (x = y) = z; //结果： b不变，a为z值

    return 0;
}
```





```c++

#define TEST(a, f) {\
    cout << #a << " : " << #f << " ";\
    f(a);\
}

void f2(int &x) {
    cout << "left value" << endl;
}

void f2(int &&x) {
    cout << "right value" << endl;
}

void f(int &x) {
    cout << "left value" << endl;
    TEST(x, f2);
}

void f(int &&x) {
    cout << "right value" << endl;
    //forward和move示例
    //TEST(forward<int &&>(x), f2);
    TEST(move(x), f2);
}

int main() {
	int a = 0, b = 1, c = 3;
    TEST(a += 3, f);
    TEST(1 + 4, f);
    TEST(b + c, f);
    TEST(a++, f);
    TEST(++a, f);
    return 0;
}
```





**使用forward，move之前**

```
a += 3 : f left value
x : f2 left value
1 + 4 : f right value
x : f2 left value
b + c : f right value
x : f2 left value
a++ : f right value
x : f2 left value
++a : f left value
x : f2 left value
```



**使用forward，move**

```
a += 3 : f left value
x : f2 left value
1 + 4 : f right value
forward<int &&>(x) : f2 right value
b + c : f right value
forward<int &&>(x) : f2 right value
a++ : f right value
forward<int &&>(x) : f2 right value
++a : f left value
x : f2 left value
```

