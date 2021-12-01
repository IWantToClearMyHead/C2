### Small Number
C language is based on binary, or digital electrical component, that is to say, everything is a number. 
We classify the number in different size as data type, just like street block number. The minum size is one *byte*, or eight bits, or harf word.

| Data Type | Memory (bytes) | Range | Format Specifier |
| --- | --- | --- | --- |
| short int | 2   | -32,768 to 32,767 | %hd |
| unsigned short int | 2   | 0 to 65,535 | %hu |
| unsigned int | 4   | 0 to 4,294,967,295 | %u  |
| int | 4   | -2,147,483,648 to 2,147,483,647 | %d  |
| long int | 4   | -2,147,483,648 to 2,147,483,647 | %ld |
| unsigned long int | 4   | 0 to 4,294,967,295 | %lu |
| long long int | 8   | -(2^63) to (2^63)-1 | %lld |
| unsigned long long int | 8   | 0 to 18,446,744,073,709,551,615 | %llu |
| signed char | 1   | -128 to 127 | %c  |
| unsigned char | 1   | 0 to 255 | %c  |
| float | 4   |     | %f  |
| double | 8   |     | %lf |
| long double | 16  |     | %Lf |

### Big Number
When we build a caculator, we really need to process big number, like a billion or more, which could exceed the limits, so we have to find a way to represent it.
Take below factorial as example,
```
# cat a.c
#include <assert.h>
#include <stdio.h>

int fact(int n){
        int i;
        int p = 1;
        for (i=1; i <= n ; ++i){
                p = p * i;
        }
        return p;
}
int main(int argc, char * argv[]){
        int n;
        n = atoi(argv[1]);
        assert( n >= 0);
        /* Print the factorial */
        printf ("%d ! = %d \n", n, fact(n));
        return 1;
}
# ./a.out 17
17 ! = -288522240 
```

On Linux, we can use GMP to calculate BN.
```
# cat a.c
#include<gmp.h>
#include<stdio.h>

int main()
{
    mpz_t a, c;
    mpz_init(a);
    mpz_init(c);
    //2 to the power of 1000
    mpz_init_set_ui(a, 2);
    mpz_pow_ui(c, a, 1000);
    gmp_printf("2 to the power of 1000 = %Zd\n", c);
    mpz_clear(a);
    
    //fact of 16
    mpz_fac_ui(c, 16);
    gmp_printf("fact of 16 = %Zd\n", c);
    mpz_clear(c);
    
    return 0;
}
# gcc a.c -lgmp
# ./a.out 
2 to the power of 1000 = 10715086071862673209484250490600018105614048117055336074437503883703510511249361224931983788156958581275946729175531468251871452856923140435984577574698574803934567774824230985421074605062371141877954182153046474983581941267398767559165543946077062914571196477686542167660429831652624386837205668069376
fact of 16 = 20922789888000
```

### Matrix
Numbers can be put into homogeneous function of degree n.
In C, array is developed to hold such data.

<a href="#top">Back to top</a>

