# Reverse Integer #
## Problem Description ##
> Reverse digits of an integer.
> 
> Example1: x = 123, return 321<br/>
> Example2: x = -123, return -321
## My Solution ##
The key part of this algorithm is to convert the number to string and reverse the elements in the string and then convert it back to int. However, there are some boundary cases like it may overflow after reverse. So when converting string back to a number, I first store the value in a long variable, and test if it overflows in 32-int, if it overflows, return 0 directly, if not, return the converted version.

## Code in C ##
```c
void swap(char* a, char* b) {
    char temp = *a;
    *a = *b;
    *b = temp;
}

#define abs(x) (((x) > 0) ? (x) : (-x))

int reverse(int x) {
    int sign = x < 0 ? 1 : 0;
    int len, i;
    char buf[11];
    long result;
    sprintf(buf, "%d", abs(x));
    len = strlen(buf);
    for(i = 0; i < len>>1; i++)
        swap(buf+i, buf+(len-1-i));
    sscanf(buf, "%ld", &result);
    if (result > 2147483647 && !sign || result > 2147483648 && sign) return 0;
    x = (int) result;
    return sign? -x: x;
}
```
