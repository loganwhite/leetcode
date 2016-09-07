# LeetCode Algorithm Problem Set No.1 -- Two Sum #

## Problem Description ##

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
> 
> You may assume that each input would have exactly one solution.
> 
> Example:
> 
> 	 Given nums = [2, 7, 11, 15], target = 9,
> 	 
> 	 Because nums[0] + nums[1] = 2 + 7 = 9,
> 	 return [0, 1].

## Problem Analysis and Solution ##

&nbsp;&nbsp;This problem is simple, we can just add every 2 elements in this array and return the 2 with the sum of the target. The code below show the whole process.

	/**
	 * Note: The returned array must be malloced, assume caller calls free().
	 */
	int* twoSum(int* nums, int numsSize, int target) {
	    int i, j;
	    int *result = (int*)malloc(sizeof(int)*2);
	    for (i = 0; i < numsSize; i++)
	    	for (j = i + 1; j < numsSize; j++) {
	    		if ((nums[i] + nums[j]) == target) {
	    			*result = i;
	    			*(result + 1) = j;
	    			return result;
	    		}
	    	}
	    	
	    return NULL;
	}