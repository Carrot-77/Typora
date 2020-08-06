# final



1. final防止子类对父类方法的重写

2. final防止类再被继承



```c++
using namespace std;

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

