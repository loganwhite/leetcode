# LeetCode Algorithm Problem Set No.5 -- Longest Palindromic Substring #

## Problem Description ##

> &nbsp;&nbsp;Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

## Background knowledge -- What is PALINDROMIC STRING ##

&nbsp;&nbsp;A palindromic string is the kind of string that you can either read from left to right or from right to left and both kinds are the same. See [https://en.wikipedia.org/wiki/Palindrome](https://en.wikipedia.org/wiki/Palindrome "Wikipedia description")  for more information.

## Problem Analysis and Solution ##

### Dynamic Programming ###

&nbsp;&nbsp;After read the problem, I decided to use DP method to solve it. why? Because it can divide the problem into sub-problems and each sub-problems are relevant which is suitable for DP.<br/>
&nbsp;&nbsp;First of all, each element in the string itself is a palindromic substring of the whole string and the length of it is *1*. This is obvious. Second, if the string *s[i] == s[i+1]* then the length of *s[i,i+1]* is 2. Finally, we can test if string *s* contains a substring *s'* whole length is set from 3 to the length of string *s*. For each length, we shift *s'* from the beginning to the end. And for each *s'*, we test if *s[i] == s[j]* and substring *s[i+1,j-1]* is already a palindromic string.<br/>
&nbsp;&nbsp;The key to dynamic programming is the state transition formula. In this problem, we use the value of *matrix[i][j]* to represent if *s[i,j]* is a palindromic string. In this way don't have to calculate the if substring *s[i+1,j-1]* is a palindromic string every time. So the state transition formula is shown above.

$$ matrix[i][j]=\\left\\{
\\begin{aligned}
matrix[i+1][j-1] &, & s[i] = s[j] \\\
0 & , & s[i] \\ne s[j] \\\
1 & , & i = j
\\end{aligned}
\\right.
$$

&nbsp;&nbsp;The code is shown below.

	char* longestPalindrome(char* s) {
	    int matrix[1000][1000] = {0};
	    int maxLen = 1;
	    int maxBegin = 0;				//start of the substring
	    int n = strlen(s);
	
	    int i, len;
	    for (i = 0; i < n; i++)
	        matrix[i][i] = 1;
	
	    for (i = 0; i < n-1; i++) {
	        if (s[i] == s[i+1]) {
	            matrix[i][i+1] = 1;
	            maxBegin = i;
	            maxLen = 2;
	        }
	    }
	
	    for (len = 3; len <= n; len++)		//start testing substring 
	        for (i = 0; i < n-len+1; i++) {	//with len from 3 to length of whole string
	            int j = i + len - 1;
	            if (s[i] == s[j] && matrix[i+1][j-1]) {
	                matrix[i][j] = 1;
	                maxBegin = j;
	                maxLen = len;
	            }
	        }
	    *(s + maxBegin + maxLen) = '\0';	//add the end character of the substring
	    return (s + maxBegin);
	}