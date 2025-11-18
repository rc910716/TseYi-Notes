###### if(0)的作用
1. 可以用于goto语句中：因为标签地点之后的代码是无论是否跳转都会按顺序执行的，所以使用if(0),可以用来指定那些不想顺序执行，但是又希望能够通过跳转执行的代码。下面是示例：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
int main (int argc, char** argv)
{
    int num;
 
    if (argc != 3)
    {
        fprintf (stderr, "Usage: %s {BIN|OCT|DEC|HEX|STR} {ARG}\n", argv[0]);
        return 1;
    }
 
    if (!strcmp (argv[1], "BIN") )
    {
        num = strtol (argv[2], NULL, 2);
        goto number_mode;
    }
    else if (!strcmp (argv[1], "OCT") )
    {
        num = strtol (argv[2], NULL, 8);
        goto number_mode;
    }
    else if (!strcmp (argv[1], "DEC") )
    {
        num = strtol (argv[2], NULL, 10);
        goto number_mode;
    }
    else if (!strcmp (argv[1], "HEX") )
    {
        num = strtol (argv[2], NULL, 16);
        goto number_mode;
    }
    else if (!strcmp (argv[1], "STR") )
    {
        printf ("Called with string argument: '%s'\n", argv[2]);
    }
    else
    {
        printf ("Called unsupported mode: '%s'\n", argv[1]);
    }
 
    /* Clifford's Device */
    if (0)
    {
number_mode:
        printf ("Called with numeric argument: %d\n", num);
    }
 
    return 0;
}

```
2. 第二个作用,下面这个示例并不算太好，但是他仍然告诉了我们一些if(0)语句的作用：当我们需要某个代码段不起作用时就可以这样做，用if(0)将他们包围起来。
```c
#include <stdio.h>
#define IF_DEF  1

#define MCASE((X),(SS)) if(0) {case X: SS }

int main (void)
{
    char* num;

    int argc_test;

    for (int i = 0; i < 7; i++)
    {
        argc_test = i;
#if IF_DEF == 1
        printf ("if (0) %d\n" , argc_test);
        switch (argc_test - 1)
        {
            if (0) { case  0:
                num = "zero";
                printf ("==0\n");
            }
            if (0)
            {
            case  2:
                num = "two";
                printf ("==2\n");
            }
            if (0)
            {
            case  3:
                num = "three";
                printf ("==3\n");
            }
            if (0)
            {
            case  4:
                num = "four";
                printf ("==4\n");
            }
            if (0)
            {
            case  5:
                num = "five";
                printf ("==5\n");
            }
            if (0)
            {
            default:
                num = "many";
                printf ("==...\n");
            }
            printf ("Called with %s arguments.\n", num);
            break;
        case 1:
            printf ("Called with one argument.\n");
        }
#else
        printf ("no if (0)\n");
        switch (argc_test - 1)
        {
            //if (0)
            {
            case  0:
                num = "zero";
                printf ("==0\n");
            }
            //if (0)
            {
            case  2:
                num = "two";
                printf ("==2\n");
            }
            //if (0)
            {
            case  3:
                num = "three";
                printf ("==3\n");
            }
            //if (0)
            {
            case  4:
                num = "four";
                printf ("==4\n");
            }
            //if (0)
            {
            case  5:
                num = "five";
                printf ("==5\n");
            }
            //if (0)
            {
            default:
                num = "many";
                printf ("==...\n");
            }
            printf ("Called with %s arguments.\n", num);
            break;
        case 1:
            printf ("Called with one argument.\n");
        }
#endif
    }

    return 0;
}
```
3. 上面这个示例还同时表现出另外的一个问题，switch-case语句实际上是要比if-elseif-else语句更快的，因为switch语句可以通过生成线性表，直接使用类似于goto语句的跳转功能，而后者需要一直进行判断。