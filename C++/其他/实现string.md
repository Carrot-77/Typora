

# 方法一



```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <vector>
#include <queue>
#include <stack>
#include <set>
#include <map>

using namespace std;
#define maxn 100000

class Mystring {
public:
    //string s1();
    Mystring() {
        length = 1;
        str = new char[1];
        *str = '\0';
    }
    
    //string s2("hello");
    Mystring(const char *s) {
        length = strlen(s);
        str = new char[length + 1];
        strcpy(str, s);
    }

    //string s3(3, 'k');
    Mystring(int n, char c) {
        length = n;
        str = new char[length + 1];
        for (int i = 0; i < n; i++) {
            str[i] = c;
        }
    }

    //string s4("hello", 1, 3);
    Mystring(const char *s, int a, int b) {
        length = b - a + 1;
        str = new char[length + 1];
        for (int i = 0; i < length; i++) {
            str[i] = s[i + a];
        }
    }

    char* str_out() const {return str;}

    Mystring(const Mystring &my) {
        length = strlen(my.str);
        str = new char[length + 1];
        strcpy(str, my.str);
    }
    
    //+
    Mystring operator+(const Mystring &my) {
        length = strlen(this->str) + strlen(my.str);
        Mystring newstr;
        delete []newstr.str;
        newstr.str = new char[length + 1];
        strcat(newstr.str, this->str);
        strcat(newstr.str, my.str);
        return newstr;
    }
 
    //=
    Mystring &operator=(const Mystring &my) {
        if (this == &my) return *this;
        delete []str;
        length = strlen(my.str);
        this->str = new char[length + 1];
        strcpy(this->str, my.str);
        return *this;
    }

    //==
    bool operator==(const Mystring &my) {
        if(strcmp(this->str, my.str) == 0) return true;
        else return false;
    }

    //!=
    bool operator!=(const Mystring &my) {
        if(strcmp(this->str, my.str) == 0) return false;
        else return true;
    }

    //>
    bool operator>(const Mystring &my) {
        if(strcmp(this->str, my.str) > 0) return true;
        else return false;
    }

    //>=
    bool operator>=(const Mystring &my) {
        if(strcmp(this->str, my.str) >= 0) return true;
        else return false;
    }

    //<
    bool operator<(const Mystring &my) {
        if(strcmp(this->str, my.str) < 0) return true;
        else return false;
    }

    //<=
    bool operator<=(const Mystring &my) {
        if(strcmp(this->str, my.str) <= 0) return true;
        else return false;
    }

    //[]
    char &operator[](int ind) {
        return str[ind];
    }




    ~Mystring() {
        delete []str;
    }


private:
    int length;
    char *str;
};



ostream &operator<<(ostream &out, const Mystring &my) {
    cout << my.str_out();
    return out;
}


int main() {
    char s[maxn];
    char c;
    int a, b;
    memset(s, 0, sizeof(char) * maxn);
    
    cout << "2: create string(char*)" << endl;
    cin >> s;
    Mystring str2(s);
    cout << "string(char*): " << str2 << endl;
    
    cout << "3: create string(int, char)" << endl;
    cin >> a >> c;
    Mystring str3(a, c);
    cout << str3 << endl;

    memset(s, 0, sizeof(char) * maxn);
    cout << "4: create string(char*, int, int)" << endl;
    cin >> s >> a >> b;
    Mystring str4(s, a, b);
    cout << str4 << endl;

    cout << "str2 + str3: " << str2 + str3 << endl;
    Mystring str5 = str2;
    cout << "str5 = str2" << endl;
    cout << "str5: " << str5 << endl;
    
    if (str2 >= str3) {
        cout << str2 << endl;
    } else cout << str3 << endl;
    return 0;
}
```





# 方法二

```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <string>
#include <vector>
#include <queue>
#include <stack>
#include <set>
#include <map>

using namespace std;

namespace hz {
class string {
public:
    string() {
        this->__buff_size = 10;
        this->buff = new char[this->__buff_size];
        this->__length = 0;
    }
    string(const char *str) {
        this->__buff_size = strlen(str) + 1;
        this->buff = new char[this->__buff_size];
        strcpy(this->buff, str);
        this->__length = this->__buff_size - 1;
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
        int size = this->__length + s.__length + 1;
        char *temp = new char[size];
        strcpy(temp, this->buff);
        strcat(temp, s.buff);
        return temp;
    }
    int size() {return this->__length;}


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
    cout << s1 << endl;
    cout << s1 + s2 + s3 << endl;
    for (int i = 0; i < s1.size(); i++) {
        cout << s1[i] << endl;
    }
    return 0;
}

```

