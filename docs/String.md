### Emoji
Nowadays we have so many fun chars other than words, as below,
```
# cat f.c
#include <stdio.h>
#include <wchar.h>
#include <locale.h>

#define N 6

int main() {
  setlocale(LC_ALL, "en_US.utf-8");

  // Emoji array. Look up on emojipedia!
  wchar_t emojis[N] = {0x1f332, 0x1f341, 0x1f4cd, 0x1f342, 0x1f698, 0x1f387};

  // Print emoji array
  printf("This could be the description of any inspirational insta picture\n");
  printf("#reasontoroam #nrthwst\n");
  for(int i = 0; i < N; ++i) printf("%lc", emojis[i]);
  printf("\n");
}
root@hwsrv-894377:~# ./a.out 
This could be the description of any inspirational insta picture
#reasontoroam #nrthwst
🌲🍁📍🍂🚘🎇
```

The character developed in half century, 

| phase | coding  | note   |
|-------|---------|--------|
| 1     | ASCII   |        |
| 2     | ANSI    |        |
| 3     | GB2312  |        |
| 4     | GBK     |        |
| 5     | Unicode |        |
| 6     | UTF-16  |        |
| 7     | UTF-8   |        |



<a href="#top">Back to top</a>
