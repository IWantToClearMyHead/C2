
### 8 in data type

|  1   | 2  |  3   | 4  |
|  ----  | ----  |  ----  | ----  |
| auto  | <span style="color:green">double</span> | <span style="color:green">long</span> | switch |
| break  | else | register | typedef |
| case  | enum | return  | <span style="color:green">unsigned</span> |
| <span style="color:green">char</span> | extern | <span style="color:green">short</span> | union |
| const  | <span style="color:green">float</span> | <span style="color:green">signed</span> | void |
| continue  | for | sizeof | volatile |
| default  | goto | while | static | 
| do  | if | <span style="color:green">int</span> | struct |

The basic data type used up 8 keywords, thus left 24. See previous [Number](Number.md) for detail.

### 4 in storage
|  type  | storage  |  default<br>value  | scope | life<br>cycle  |
|  ----  | ----  |  ----  | ----  | ----  |
| auto |  stack  |  garbage  | within block  | end of block  |
| extern |  data segment  |  zero  | global multiple files  | till end of the program  |
| static |  data segment  |  zero  | within block  | till end of the program  |
| register |  cpu  |  garbage  | within block  | end of block  |

The storage type used up 4 keywords, thus left 20.

*auto* is a kind of long long ago story, now we hardly ever use it, since all variables in functions are local by default now.

| type | default value |
|  ----  | ----  |
| int |	0 |
| char	| '\0' |
| float	| 0 |
| double	| 0 |
| pointer	|NULL|

*extern* variables can be declared number of times but defined only once. 
Definition of a variable is when the variable is created and the memory for it is allocated.
Declaration of a variable just tells the compiler that this variable exists. It does not allocate any memory.
In practice it should be used in our header files and then we will include the necessary headers. We should avoid the usage of exern keyword in our source files.
*static* variables remain in memory while the program is running. A normal or auto variable is destroyed when a function call where the variable was declared is over. 
```
# cat a.c
#include<stdio.h>
int fun()
{
  static int count = 0;
  count++;
  return count;
}
  
int main()
{
  printf("%d ", fun());
  printf("%d ", fun());
  return 0;
}
# ./a.out
1 2
```
*register* variables tell the compiler to store the variable in CPU register instead of memory. Frequently used variables are kept in registers and they have faster accessibility. We can never get the addresses of these variables.

### 1 sizeof
return a typedef value *size_t* depends on the compiler, 32 bit for unsigned int and 64 bit for unsigned long long. 
```
#include <stdio.h>
   
int main()
{
    printf("Size of char   =  %ld \n", sizeof(char));
    printf("Size of int    =  %ld \n", sizeof(int));
    printf("Size of float  =  %ld \n", sizeof(float));
    printf("Size of double =  %ld \n\n", sizeof(double));
   
    printf("Size of short int      =  %ld \n", sizeof(short int));
    printf("Size of long int       =  %ld \n", sizeof(long int));
    printf("Size of long long int  =  %ld \n", sizeof(long long int));
    printf("Size of long double    =  %ld \n", sizeof(long double));
   
    return 0;
}
```

### 1 union
*union* is a derived type, like 🦎. That is to say, its size equal to the max size of its member.

```
# cat a.c
#include <stdio.h>
union Job {
   float salary;
   int workerNo;
} j;

int main() {
   j.salary = 12.3;
   printf("sizeof = %ld\n", sizeof(j));
   printf("Salary = %.1f\n", j.salary);
   // when j.workerNo is assigned a value,
   // j.salary will no longer hold 12.3
   j.workerNo = 100;
   printf("sizeof = %ld\n", sizeof(j));
   printf("Salary = %.1f\n", j.salary);
   printf("Number of workers = %d", j.workerNo);
   return 0;
}
# ./a.out
sizeof = 4
Salary = 12.3
sizeof = 4
Salary = 0.0
Number of workers = 100
```

### 1 struct
Sometimes we need compound data type, and in hardware we care more about alignment.

```
# cat a.c
#include <stdio.h>
#include <string.h>
 
/*  Below structure1 and structure2 are same. 
    They differ only in member's allignment */
 
struct structure1 
{
       int id1;
       int id2;
       char name;
       char c;
       float percentage;
};
 
struct structure2 
{
       int id1;
       char name;
       int id2;
       char c;
       float percentage;                      
};
 
int main() 
{
    struct structure1 a;
    struct structure2 b;
 
    printf("size of structure1 in bytes : %d\n", 
            sizeof(a));
    printf ( "\n   Address of id1        = %u", &a.id1 );
    printf ( "\n   Address of id2        = %u", &a.id2 );
    printf ( "\n   Address of name       = %u", &a.name );
    printf ( "\n   Address of c          = %u", &a.c );
    printf ( "\n   Address of percentage = %u", &a.percentage );
 
    printf("   \n\nsize of structure2 in bytes : %d\n",
                   sizeof(b));
    printf ( "\n   Address of id1        = %u", &b.id1 );
    printf ( "\n   Address of name       = %u", &b.name );
    printf ( "\n   Address of id2        = %u", &b.id2 );
    printf ( "\n   Address of c          = %u", &b.c );
    printf ( "\n   Address of percentage = %u", &b.percentage );
    getchar();
    return 0;
}
# ./a.out
size of structure1 in bytes : 16

   Address of id1        = 1761339056
   Address of id2        = 1761339060
   Address of name       = 1761339064
   Address of c          = 1761339065
   Address of percentage = 1761339068   

size of structure2 in bytes : 20

   Address of id1        = 1761339072
   Address of name       = 1761339076
   Address of id2        = 1761339080
   Address of c          = 1761339084
   Address of percentage = 1761339088
```
The result is different from math, `int id1 + char name + int id2 + char c + float percentage = 4 + 1 + 4 + 1 + 4 = 14 bytes`, due to structure padding, that is, in order to align the data in memory,  one or more empty bytes (addresses) are inserted (or left empty) between memory addresses which are allocated for other structure members while memory allocation. 
The above example has a step of *8 bytes*, thus 64-bit platform. For structure1, `int, int, char, char, empty(2), float`, and structre2, `int, char, empty(3), int, char, empty(3), float`.

use `pack` to get 14 bytes,
```
#include <stdio.h>
#include <string.h>
 
/*  Below structure1 and structure2 are same. 
    They differ only in member's allignment */
 
#pragma pack(1)
struct structure1 
{
       int id1;
       int id2;
       char name;
       char c;
       float percentage;
};
 
struct structure2 
{
       int id1;
       char name;
       int id2;
       char c;
       float percentage;                      
};
 
int main() 
{
    struct structure1 a;
    struct structure2 b;
 
    printf("size of structure1 in bytes : %d\n",
                   sizeof(a));
    printf ( "\n   Address of id1        = %u", &a.id1 );
    printf ( "\n   Address of id2        = %u", &a.id2 );
    printf ( "\n   Address of name       = %u", &a.name );
    printf ( "\n   Address of c          = %u", &a.c );
    printf ( "\n   Address of percentage = %u", 
                   &a.percentage );
 
    printf("   \n\nsize of structure2 in bytes : %d\n", 
                   sizeof(b));
    printf ( "\n   Address of id1        = %u", &b.id1 );
    printf ( "\n   Address of name       = %u", &b.name );
    printf ( "\n   Address of id2        = %u", &b.id2 );
    printf ( "\n   Address of c          = %u", &b.c );
    printf ( "\n   Address of percentage = %u", 
                   &b.percentage );
    getchar();
    return 0;
}
```

### 1 enum
An easier way to number sequnce in a group(😶at this point, left 16).



<a href="#top">Back to top</a>
