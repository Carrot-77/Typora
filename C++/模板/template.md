程序=算法+数据结构

数据结构：能够存储任意类型

算法：能够操作存储任意类型数据的数据结构



|              | 泛型编程             |
| ------------ | -------------------- |
| 面向过程编程 | 使用模板实现函数过程 |
| 面向对象编程 | 使用模板实现类       |



# template

模板函数

```c++
template<typename T>
T add(T a, T b) {
    return a + b;
}
```



```c++
//typename与class没有如何区别
//decltype 推导表达式返回值类型
template<typename T, typename U>
decltype(T() + U()) add(T a, U b) {
    return a + b;
}

int main() {
    //add( , )编译器隐式推导
    //<>显示模板实例化
    cout << add(2, 3) << endl;
    cout << add(2.3, 3.2) << endl;
    cout << add(2.333, 3) << endl;

    return 0;
}
```

