# Palindrome Number #
## Description ##
Determine whether an integer is a palindrome. Do this without extra space.
## My Solution ##
The first thought on seeing this problem is to use the previous result. We have done a problem called Reverse interger. So all we have to do is to call the reverse function we write before and compare the result with the parameter. Note that a negtive number is not a **Palindrome Number** because we don't have a number with a '-' sign in the tail.

However, this problem requires us don't use extra space. So the previous algorithm is not allowed even the LeetCode OJ ACCETED that kind of code. So we have to use the original method, that is split the bits by dividing. Since we want to have the reversed version of an integer. So each time, we can just mod the number and get the remainder and multiple it by 10. The code are shown below.

## Code in C ##
```c
bool isPalindrome(int x) {
    int p = x; 
    int q = 0; 
    
    if (x < 0) return false;
    
    while (p >= 10){
        q *=10; 
        q += p%10; 
        p /=10; 
    }
    
    return q == x / 10 && p == x % 10;
}
```
