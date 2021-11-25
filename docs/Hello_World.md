### Hello World
The first application that we learn, almost for every programming language is "Hello World".

In C, this is quite neat,

```
# cat a.c
#include <stdio.h>    
int main()
{ 
     // Displays the string inside quotations
     printf("Hello World\n");
     return 0;
}
# gcc a.c
# ./a.out
Hello World
```

The above can be understood via a table,
| command  | function                  | note           |
|----------|---------------------------|----------------|
| cat      | linux show command        |                |
| include  | header for c source file  |                |
| int main | main function             |                |
| {}       | code block                |                |
| //       | comment for code          |                |
| printf   | standard output to screen |                |
| \n       | new line                  |                |
| return 0 | function return value     |                |
| gcc      | compile c source file     | must install   |
| ./       | linux execute command     | 755 permission |
| a.out    | object of c source file   |                |

### CJK and etc
On the earth planet, we have nearly 200 countries, though English is wide spreaded, people do have dialect and corresponding characters.
Let's translate "Hello World" into other human languages, in a table,
| lang | char        |
|------|-------------|
| ENG  | Hello World |
| CHN  | 你好        |
| JPN  | こんにちわ   |
| KRN  | 안녕하세요   |
| ARB  | السلام عليكم|

```
# cat a.c
#include <stdio.h>
int main()
{
     // Displays the string inside quotations
     printf("你好\n");
     return 0;
}
# ./a.out 
你好

# cat a.c
#include <stdio.h>
int main()
{
     // Displays the string inside quotations
     printf("السلام عليكم\n");
     return 0;
}
# ./a.out 
السلام عليكم
```

### scanf
