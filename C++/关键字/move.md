`std::move` 会无条件将自己的参数转换为右值。在对象拷贝的时候，在运行时，它们不会产生一行代码， 可以减少资源创建和释放。





```c++
namespace hz {
class string {
public:
    string() {
        cout << "string: constructor" << this << endl;
        this->__buff_size = 10;
        this->buff = new char[this->__buff_size];
        this->__length = 0;
    }
    string(const char *str) {
        cout << "string: const char constructor: " << this << endl;
        this->__buff_size = strlen(str) + 1;
        this->buff = new char[this->__buff_size];
        strcpy(this->buff, str);
        this->__length = this->__buff_size - 1;
    }
    string(const string &s) {
        cout << "copy constructor" << this << endl;
        this->__buff_size = s.__buff_size;
        this->__length = s.__length;
        this->buff = new char[s.__buff_size];
        this->__length = s.__length;
        strcpy(this->buff, s.buff);
    }
    string (string &&s) {
        cout << "move constructor " << this << endl;
        this->__buff_size = s.__buff_size;
        this->__length = s.__length;
        this->buff = s.buff;
        s.buff = nullptr;
    }
    char &at(int ind) {
        if (ind < 0 || ind >= __length) {
            cout << "String Error: out of range" << endl;
            return __end;
        }
        return this->operator[](ind);
    }
    char &operator[](int ind) {
        return buff[ind];
    }
    char *c_str() const {
        return buff;
    }
    string operator+(const string &s) {
        cout << "string: operator + " << this << endl;
        int size = this->__length + s.__length + 1;
        char *temp = new char[size];
        strcpy(temp, this->buff);
        strcat(temp, s.buff);
        return temp;
    }
    int size() {return this->__length;}
    ~string() {
        cout << "destructor" << this << endl;
        if (this->buff) delete []buff;
    }

private:
    int __length, __buff_size;
    char *buff;
    char __end;
};
}

ostream &operator<<(ostream &out, const hz::string &s) {
    out << s.c_str();
    return out;
}

int main() {
    hz::string s1 = "carrot", s2 = "ccccct", s3 = ",.!";
    cout << "===s4===" << endl;
    hz::string s4 = s1 + s2 + s3;
    cout << "===s4===" << endl;
    cout << s4 << endl;
    /* cout << s1 << endl; */
    /* hz::string s5(s4); */
    /* cout << s4 << endl; */
    /* cout << s5 << endl; */
    /* s4[3] = '='; */
    /* cout << "=" << endl; */
    /* cout << s4 << endl; */
    /* cout << s5 << endl; */
    /* s5[3] = '6'; */
    /* cout << "6" << endl; */
    /* cout << s4 << endl; */
    /* cout << s5 << endl; */
    /* cout << s1 + s2 + s3 << endl; */
    /* for (int i = 0; i < s1.size(); i++) { */
    /*     cout << s1[i] << endl; */
    /* } */
    return 0;
}

```



## 无移动构造输出

> g++ | ./a.out



```
string: const char constructor: 0x7fffd7f587e0
copy constructor0x7fffd7f58740
destructor0x7fffd7f587e0
string: const char constructor: 0x7fffd7f587e0
copy constructor0x7fffd7f58760
destructor0x7fffd7f587e0
string: const char constructor: 0x7fffd7f587e0
copy constructor0x7fffd7f58780
destructor0x7fffd7f587e0
===s4===
string: operator + 0x7fffd7f58740
string: const char constructor: 0x7fffd7f58700
copy constructor0x7fffd7f587c0
destructor0x7fffd7f58700
string: operator + 0x7fffd7f587c0
string: const char constructor: 0x7fffd7f58700
copy constructor0x7fffd7f587e0
destructor0x7fffd7f58700
copy constructor0x7fffd7f587a0
destructor0x7fffd7f587e0
destructor0x7fffd7f587c0
===s4===
carrotccccct,.!
destructor0x7fffd7f587a0
destructor0x7fffd7f58780
destructor0x7fffd7f58760
destructor0x7fffd7f58740
```





## 移动构造输出

> g++ -fno-elide-constructors 28.move_constructor.cpp | ./a.out



```
string: const char constructor: 0x7ffdc5b04d40
move constructor 0x7ffdc5b04ca0
destructor0x7ffdc5b04d40
string: const char constructor: 0x7ffdc5b04d40
move constructor 0x7ffdc5b04cc0
destructor0x7ffdc5b04d40
string: const char constructor: 0x7ffdc5b04d40
move constructor 0x7ffdc5b04ce0
destructor0x7ffdc5b04d40
===s4===
string: operator + 0x7ffdc5b04ca0
string: const char constructor: 0x7ffdc5b04c60
move constructor 0x7ffdc5b04d20
destructor0x7ffdc5b04c60
string: operator + 0x7ffdc5b04d20
string: const char constructor: 0x7ffdc5b04c60
move constructor 0x7ffdc5b04d40
destructor0x7ffdc5b04c60
move constructor 0x7ffdc5b04d00
destructor0x7ffdc5b04d40
destructor0x7ffdc5b04d20
===s4===
carrotccccct,.!
destructor0x7ffdc5b04d00
destructor0x7ffdc5b04ce0
destructor0x7ffdc5b04cc0
destructor0x7ffdc5b04ca0
```

