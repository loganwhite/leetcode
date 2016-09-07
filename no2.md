# LeetCode Algorithm Problem Set No.2 -- Add Two Numbers #

## Problem Description ##

> You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
> 
> **Input:** (2 -4 -3) + (5 -6 -4)<br/>
> **Output:** 7 -0 -8

## Problem Analysis and Solution ##

&nbsp;&nbsp;This problem demonstrate how we add up two numbers by hands. First of all, we add the last digit of each number, if the result is greater than 9, it will contains a carry. And actually, the value of carry is 0 if the result is less than 10. And at the beginning, the carry is definitely 0. So for each digit from beginning to the end, we shall calculate the sum of two numbers and the carry. And then get the digit ought to be shown and the new carry to the next digit. each time we produce a new digit we shall allocate a new node to store it. The time to stop is when all the digits of the two numbers are calculated and carry is 0. The code below implements the procedure.

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	
	struct ListNode* newNode(int val) {
	    struct ListNode* new_node = (struct ListNode*)malloc(sizeof(struct ListNode*));
	    new_node->val = val;
	    new_node->next = NULL;
	    return new_node;
	}
	
	struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
	    struct ListNode* result = NULL, *cur;
	    int a, b;
	    int temp, carry = 0;
	    while(l1 || l2 || carry) {
	        if (l1) {
	            a = l1->val;
	            l1 = l1->next;
	        } else a = 0;
	        if (l2) {
	            b = l2->val;
	            l2 = l2->next;
	        } else b = 0;
	        temp = a + b + carry;
	        carry = temp / 10;
	        temp %= 10;
	        if (!result) {
	            result = newNode(temp);
	            cur = result;
	        } else {
	            cur->next = newNode(temp);
	            cur = cur->next;
	        }
	    }
	    return result;
	}