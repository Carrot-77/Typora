

* nullptr 实际为地址 
* NULL 实际为0，当成地址,实际是(void*)0



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

