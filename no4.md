# LeetCode Algorithm Problem Set No.4 -- Median of Two Sorted Arrays #

## Problem Description ##

> There are two sorted arrays nums1 and nums2 of size m and n respectively.
> 
> Find the median of the two sorted arrays. The overall run time complexity should be *O(log (m+n))*.
> 
> **Example 1:**
> 
>     nums1 = [1, 3]
>     nums2 = [2]
> 
> The median is 2.0
> 
> **Example 2:**
> 
>     nums1 = [1, 2]
>     nums2 = [3, 4]
> 
> The median is (2 + 3)/2 = 2.5

## Problem Analysis and Solution ##

### A Simple Approach ###

&nbsp;&nbsp;This problem is very simple if we dismiss the time complexity of the algorithm. We can simply merge the two array and find the median of the complete array. The code below implements in this way. The time complexity is *O(n + m)* obviously.
	
	//watch out! this function allocates memory from heap, 
	//free them after use.
	int* merge(int* nums1, int nums1Size, int* nums2, int nums2Size) {
		int s = 0, k = 0, i;
		int len = nums1Size + nums2Size;
		int *complete = (int*)malloc(sizeof(int)*len);
		//merge the array
		for (i = 0; i < len; i++) {
			if (s == nums1Size) {
				if (k < nums2Size)
					complete[i] = nums2[k++];
				continue;
			}
			if (k == nums2Size) {
				if (s < nums1Size)
					complete[i] = nums1[s++];
				continue;
			}

			if (nums1[s] < nums2[k]) {
				complete[i] = nums1[s];
				s++;
			} else {
				complete[i] = nums2[k];
				k++;
			}
		}
		return complete;
	}
	
	double findMedianSortedArrays(int* nums1, int nums1Size, int* nums2, int nums2Size) {
	    int * complete;
	    int len = nums1Size + nums2Size;
	    double median;
	    complete = merge(nums1,nums1Size,nums2,nums2Size);
		//find the median directly.
	    median = (len % 2) (double)complete[len >> 1] :
			(((double)complete[len >> 1] + (double)complete[(len >> 1) - 1]) / 2.0);
	    free(complete);
	    return median;
	}

### An Optimized Approach ###
&nbsp;&nbsp;Actually the problem itself gives us hints. The time complexity ought to be *O(log(n + m))*. *log n* actually means *log<sub>2</sub>n*. On what occasion will the algorithm have the complexity? Divide and conquer or dynamic programming. For this problem, we imagine if we can divide the big problem into 2 smaller one. And for the 2 smaller problems, each of them is similar to the big one and the only difference is the scale of the problem is smaller. We divide the problem until the scale of the small problem to be small enough to solve. For this problem, we can directly get the median of the two arrays, we mark median of the array if *m<sub>1</sub>* and median of the second array is *m<sub>2</sub>* shown in  the figure above.
![array division](http://i.imgur.com/s0ClxSm.jpg)

&nbsp;&nbsp;If *m<sub>1</sub>* = *m<sub>2</sub>*:<br/>
&emsp;&emsp;The median of the merged array is *m* = *m<sub>1</sub>* = *m<sub>2</sub>*. That is obvious.

&nbsp;&nbsp;If *m<sub>1</sub>* < *m<sub>2</sub>*:<br/>
&emsp;&emsp;What happened if *m<sub>1</sub>* < *m<sub>2</sub>*? This condition can be represented into this. ...*m<sub>1</sub>*...*m<sub>2</sub>*... So the median must be between *m<sub>1</sub>* and *m<sub>2</sub>*. As we shown in the figure above, it belongs to the area **B** and **C**. So this time, the problem has become find the the median of the two sorted array **B** and **C** and the scale of **B** and **C** is definitely smaller than the original problem. As for finding the median of sorted array **B** and **C**. It just the same procedure.

&nbsp;&nbsp;If *m<sub>1</sub>* > *m<sub>2</sub>*:<br/>
&emsp;&emsp;Similarly, What happened if *m<sub>1</sub>* > *m<sub>2</sub>*? This condition can be represented into this. ...*m<sub>2</sub>*...*m<sub>1</sub>*... So the median must be between *m<sub>2</sub>* and *m<sub>1</sub>*. In the area of **D** and **A**. Again, the scale of the whole problem is has decreased. Now all we have to do is to find the median of the two sorted array **D** and **A**. The code below is the implementation in C.

	double median(int* nums, int size) {
		return (size % 2) ? (double) nums[size >> 1] : (((double)nums[size >> 1] + (double)nums[(size >> 1) - 1])/2.0);
	}
	
	double findMedianSortedArrays(int* nums1, int nums1Size, int* nums2, int nums2Size) {
	    double m1, m2;
	    m1 = median(nums1,nums1Size);
	    m2 = median(nums2,nums2Size);
	    if (m1 == m2) return m1;
	    else if (m1 < m2) {
	    	int * b, *c, lenb, lenc;
	    	if (nums1Size % 2) {
	    		b = nums1 + (nums1Size >> 1) + 1;
	    		lenb = nums1Size - 1 - (nums1Size >> 1);
	    	} else {
	    		b = nums1 + (nums1Size >> 1);
	    		lenb = nums1Size - (nums1Size >> 1);
	    	}
	
	    	c = nums2;
	    	lenc = (nums2Size % 2) ? lenc = nums2Size - 1 - (nums2Size >> 1) : 
	    		nums2Size - (nums2Size >> 1);
	
	    	return findMedianSortedArrays(b,lenb,c,lenc);
	
	    }
	    else {
	    	int *a, *d, lena, lend;
	
	    	a = nums1;
	    	lena = (nums1Size % 2) ? nums1Size - 1 - (nums1Size >> 1) :
	    		nums1Size - (nums1Size >> 1);
	    	if (nums2Size % 2) {
	    		d = nums2 + (nums1Size >> 1) + 1;
	    		lend = nums2Size - 1 - (nums2Size >> 1);
	    	} else {
	    		d = nums2 + (nums1Size >> 1);
	    		lend = nums2Size - (nums2Size >> 1);
	    	}
	
	    	return findMedianSortedArrays(d,lend,a,lena);
	
	    }
	}