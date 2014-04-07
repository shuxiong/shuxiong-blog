---
published: true
layout: post
title: "shuxiong's leetcode solution I"
date: 2014-04-07 22:47
comments: false
categories: ['interview', 'leetcode']
---

#shuxiong's leetcode solution I#

[TOC]

##[Add Two Numbers](http://oj.leetcode.com/problems/add-two-numbers/)##

Well, it is nothing difficult.
Note: if the two list is given high-bit-first-order, we can firstly reverse the lists, and do the addition, and reverse the result again.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        int g=0;
        ListNode *ret=new ListNode(-1), *tail=ret;
        while (l1!=NULL || l2!=NULL || g>0){
            if (l1!=NULL){
                g+=l1->val;
                l1=l1->next;
            }
            if (l2!=NULL){
                g+=l2->val;
                l2=l2->next;
            }
            tail->next=new ListNode(g%10);
            tail=tail->next;
            g/=10;
        }
        ListNode *tmp=ret;
        ret=ret->next;
        delete tmp;
        return ret;
    }
};
```
##[Longest Substring Without Repeating Characters ](http://oj.leetcode.com/problems/two-sum/)##

We use two pointer, *head* and *tail*.head and tail form a substring, which is guaranteed to be a legal string.
In detail, we use *tail* to scan the string from front to back, and use an array to count how many specific character is passed. When some specific character is counted more than once, we have to move *head* backward, decrease the previous character *head* points, until the substring between *head* and *tail* is legal.

For each character in the given string, *head* and *tail* will pass exactly once, so
Time complexity will be O(N).


```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        // Start typing your C/C++ solution below
        // DO NOT write int main() function
        int counter[256]={0};
        int n=s.size(), biggerThanOne=0, j=0, ans=0;
        for (int i=0;i<n;i++){
            counter[s[i]]++;
            if (counter[s[i]]>1) biggerThanOne++;
            while (biggerThanOne>0){
                if (counter[s[j]]>1) biggerThanOne--;
                counter[s[j]]--;
                ++j;
            }
            if (ans<i-j+1) ans=i-j+1;
        }
        return ans;
    }
};
```

##[Median of Two Sorted Arrays ](http://oj.leetcode.com/problems/median-of-two-sorted-arrays/)##

The problem is the same with finding Kth element in two sorted arrays.
 1. find some specific element Ea in A
 2. count how many elements are smaller in B comparing with Ea
 3. do recurion according to result of comparing total elements smaller than Ea in two arrays and K, which will be 3 cases.

Each recurion will decrease the scale of A in half, so we will perform step 1 logN times at most, and each step 2 costs O(logM).

Time Complexity: O(logN*logM)

```cpp
#include <algorithm>
using std::max;

class Solution {
private:
    // find Kth element in two sorted arrays
    int findK(int A[], int m, int B[], int n, int k){
        // handle special cases
        if (m==0) return B[k-1];
        if (n==0) return A[k-1];
        if (A[m-1]<=B[0])
            if (m>=k) return A[k-1]; else return B[k-m-1];
        if (B[n-1]<=A[0])
            if (n>=k) return B[k-1]; else return A[k-n-1];
        // we use A[wa] as a referred value, and want to find how many elements are smaller than A[wa]
        int wa=(0+m-1)/2;
        // Binary search for A[wa] in array B, which result will be B[ans]<A[wa] and B[ans+1]>=A[wa]
        int h=0, t=n-1, ans=-1;
        while (h<=t){
            int w=(h+t)/2;
            if (B[w]<=A[wa]){
                ans=w;
                h=w+1;
                if (B[w]==A[wa]) break;
            } else
            if (B[w]>A[wa]) t=w-1;
        }
        // Elements smaller than A[wa] in both A and B we find will be A[0..wa] and B[0..ans]
        // So the number of these elements will be ans+1+wa+1, which comparing with K, there are 3 cases and it forms another findK problem which both arrays are smaller. Note: that the scale of A must be half of the previous, and when the scale of A goes to Zero, it falls to special cases and can be compute in O(1).
        // Time complexity: O(logM*logN)
        if (ans+1+wa+1<k) return findK(A+wa+1, m-wa-1, B+ans+1, n-ans-1, k-wa-1-ans-1); else
        if (ans+1+wa+1>k) return findK(A, wa+1, B, ans+1, k); 
            else return (ans==-1)?A[wa]:max(A[wa], B[ans]);
    }
public:
    double findMedianSortedArrays(int A[], int m, int B[], int n) {
        // Start typing your C/C++ solution below
        // DO NOT write int main() function
        if ((m+n)%2==0) return ((double)findK(A, m, B, n, (m+n)/2)+(double)findK(A, m, B, n, (m+n)/2+1))/2;
            else return (double)findK(A, m, B, n, (m+n+1)/2);
    }
};
```

##[Two Sum](http://oj.leetcode.com/problems/two-sum/)##

In a sorted array, we manage two pointer, first of which points to the head and the second one points to the tail.
The sum of two elements referred by this two pointers can be 3 cases, comparing with *target*,

 1. Equals. In this case, elements referred by this two pointers are exactly what we want.
 2. The sum is bigger than *target*. We move the tail pointer forward.
 3. The sum is smaller than *target*. We move the head pointer backward.

Note that there is guaranteed to exist one solution, so the two pointers will never encouter each other.

Time Complexity: O(nlogn), sort the array(nlogn) & scan the array(n)

```cpp
#include <vector>
#include <algorithm>
#include <utility>
using std::vector;
using std::pair;
using std::sort;
using std::make_pair;
using std::swap;

class Solution {
public:
    vector<int> twoSum(vector<int> &numbers, int target) {
        // Note: The Solution object is instantiated only once and is reused by each test case.
        int n=numbers.size();
        vector< pair<int, int> > tmpVector;
        for (int i=0;i<n;i++) tmpVector.push_back(make_pair(numbers[i], i+1));
        sort(tmpVector.begin(), tmpVector.end());
        int h=0, t=tmpVector.size()-1;
        vector<int> ans;
        while (h<t){
            if (tmpVector[h].first+tmpVector[t].first==target){
                ans.push_back(tmpVector[h].second);
                ans.push_back(tmpVector[t].second);
                if (ans[0]>ans[1]) swap(ans[0], ans[1]);
                return ans;
            } else
            if (h<t && tmpVector[h].first+tmpVector[t].first>target) --t; else
            if (h<t && tmpVector[h].first+tmpVector[t].first<target) ++h;
        }
        return ans;
    }
};
```
