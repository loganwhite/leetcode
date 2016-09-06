# LeetCode Algorithm Problem Set No.3 -- Longest Substring Without Repeating Characters#

## Problem Description ##

> Given a string, find the length of the longest substring without repeating characters.

> Examples:

> Given "abcabcbb", the answer is "abc", which the length is 3.

> Given "bbbbb", the answer is "b", with the length of 1.

> Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Problem Analysis and Solution ##

### A Simple Approach ###

&nbsp;&nbsp;For the given string, to find the longest substring without repeating characters. We can first let the length of the substring from the original string length and then find out if there exists duplicate characters. If so, the length will be decreased by 1 and do the same procedure all over again until the characters in the substring are distinguish from each other. This method is straightforward and it's very easy to count on. The following code implements in this way.
	
	//method to find if there are duplicate characters in the substring
	int isDup(char* src, int len) {
		//map here stores the number of a certain character
		int map[256] = {0};
		while(len--) {
			map[src[len]] ++;
			if (map[src[len]] > 1) return 1;
		}
		return 0;
	}

	int lengthOfLongestSubstring(char* s) {
	    int len = strlen(s),j;
	    int i;
	    char * substr;
	    j = len;
	    if (!len) return 0;
		//get the substring with the length of j
	    while(j >= 1) {
			//get all the substring with the length of j
	    	for (i = 0; i + j <= len; i++ ) {
	    		substr = s+i;
				//test if it is duplicate
	    		if (!isDup(substr,j)) return j;
	    	}
	    	j--;
	    }
	    return 1;
	}

### An Optimized Approach ###
&nbsp;&nbsp;The previous method tried every attempt to find the longest substring without repeating characters. It's obvious that some attempts are not necessary. We wonder if there are some possibility to avoid so much iteration and finish all the tasks in a single loop. The answer is, yes. For substring *S[i, j-1]*, if *S[j]* exists in *S[i, j-1]*,