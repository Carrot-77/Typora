# getopt()



## 头文件

```c
#include <unistd.h>
```



## 函数原型

```c
int getopt(int argc,char * const argv[ ],const char * optstring);
```

```c
extern char *optarg;  
//选项的参数指针

extern int optind;
//下一次调用getopt的时，从optind存储的位置处重新开始检查选项。 

extern int opterr;  
//当opterr=0时，getopt不向stderr输出错误信息。

extern int optopt;  
//当命令行选项字符不包括在optstring中或者选项缺少必要的参数时，该选项存储在optopt中，getopt返回'？’
```



## 示例

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
 
int main(int argc, char **argv)
{
    int result;
 
    opterr = 0;  //使getopt不行stderr输出错误信息
 
    while( (result = getopt(argc, argv, "ab:c::")) != -1 )
    {
           switch(result)
          {
               case 'a':
                   printf("option=a, optopt=%c, optarg=%s\n", optopt, optarg);
                   break;
              case 'b':
                   printf("option=b, optopt=%c, optarg=%s\n", optopt, optarg);
                   break;
              case 'c':
                   printf("option=c, optopt=%c, optarg=%s\n", optopt, optarg);
                   break;
              case '?':
                    printf("result=?, optopt=%c, optarg=%s\n", optopt, optarg);
                    break;
              default:
                   printf("default, result=%c\n",result);
                   break;
           }
        printf("argv[%d]=%s\n", optind, argv[optind]);
    }
    printf("result=-1, optind=%d\n", optind);   //看看最后optind的位置
 
    for(result = optind; result < argc; result++)
         printf("-----argv[%d]=%s\n", result, argv[result]);
 
 //看看最后的命令行参数，看顺序是否改变了哈。
    for(result = 1; result < argc; result++)
          printf("\nat the end-----argv[%d]=%s\n", result, argv[result]);
    return 0;
}
```

