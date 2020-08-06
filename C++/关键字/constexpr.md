

# constexpr



## const与constexpr



const 运行期常量
constexpr 严格的编译期常量



```c++
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

