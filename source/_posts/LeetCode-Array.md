---
title: 'LeetCode::Array'
tags: [LeetCode]
date: 2018-02-11 16:48:16
---

记录LeetCode::Array部分的思路与遇到的问题。从easy到hard排序。

<!-- more -->

## Remove Duplicates From Sorted Array (id: 26)
题目不难，主要在于如何充分利用空间。利用现有的数组滚动，最后取数据时只需要取出需要的长度即可。
{% codeblock line_number:false%}
A[i++] = n
{% endcodeblock %}

## Maximum Subarray (id: 53)
用DP（Dynamic Programming）解题。DP对我来说一直是个比较难理解（应用）的方法。
也许可以专门放一个篇幅来系统学习一下。对于这个问题，我一直卡在没有想清楚怎么样才能快速的排除掉错误的部分，从而加快运算速度。
（提交不过就是因为超时）。因为总是想要把每个组合都要计算一遍，才能保证结果。比如，从`1`开始，要一直遍历到`n`才能知道A[1]到A[n]的组合中谁最大。
后来在看了讨论的帖子后理解了，如果`A[i] + A[i+1] < 0`那么之后的关于A[i]都不用考虑了。

## Merge Sorted Array （id: 88)
最容易实现的方式是创建一个新的vector，然后比较`nums1`和`nums2`里面的值，从小到大往新的vector里`push_back`，最后还要判断下，哪个没有放完的，把剩下的全部放到最后，结束。
>因为根据提示: You may assume that nums1 has enough space, 所以leetcode会吧nums1扩容.
>所以还有种方法是从后往前放，因为最后的数组我们是知道大小的，`k = m + n - 1`，所以这样可以不用新创建一个vector。
> `nums1[k--] = nums1[i] < nums2[j] ? nums2[j--] : nums1[i--]` （伪代码)

## Convert Sorted Array to Binary Search Tree (id:108)
这个问题比较容易用递归的方式实现，但是我实现的并不是很简洁(16ms)，BST可以看做是不断二分的数组，中间的元素作为root，两边分别作为left和right，以此类推。关于如果提高速度，主要是是否使用vector的内置函数，vector::begin(), vector::end(), 如果用index得方式会跟快，但是不是很一目了然。

