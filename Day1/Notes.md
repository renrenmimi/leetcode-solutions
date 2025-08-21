# Day 1 Notes

Basic theory of Arrays:

First, we need to know understand how Arrays are stored in the memory.

An Array is a collection with/of the same data type stored in the continuous memory.

Data can be  conveniently accessed by the index of the Array.

![image-20250820102408759](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820102408759.png)



Indexes start from 0.

Because the memory locations of the Array are continuous, if we want to add or delete elements, we need to shift the position of other elements. For example, if we want to delete the element at index 3:

![image-20250820102800000](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820102800000.png)

Oh, I should say, elements of the Array cannot be deleted; they can only be overwritten.

A 2D Array looks like:

![image-20250820103227030](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820103227030.png)

So, are the locations for a 2D Array is continuous?

In Java, it might be like this:

![image-20250820103542178](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820103542178.png)



## 704. Binary Search

**题目链接**: [LeetCode 704. Binary Search](https://leetcode.com/problems/binary-search/)

**English**  
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

**中文**  
给定一个按升序排序的整数数组 `nums` 和一个整数 `target`，编写一个函数在 `nums` 中搜索 `target`。如果目标值存在，则返回其索引；否则返回 `-1`。

![image-20250820154354936](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820154354936.png)

> I used the left-closed, right-closed interval for this question because the left-closed, right-open format is a bit more abstract.
> The condition of the while loop is left <= right because when left == right, the target might still be at that position.
> To avoid integer overflow, I used left + (right - left) / 2 instead of (left + right) / 2.
> When mid is not the target, we move to mid + 1 or mid - 1 because mid has already been checked and can be excluded from the search range.

> **Time Complexity**: O(logn)  n -> nums.length

> **Space Complexity**: O(1)  Fixed left, right, mid

---

## 27. Remove Element
**题目链接**: [LeetCode 27. Remove Element](https://leetcode.com/problems/remove-element/)

**English**  
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

**中文**  
给定一个整数数组 `nums` 和一个整数 `val`，请你原地移除所有数值等于 `val` 的元素。元素的顺序可以改变。然后返回数组中不等于 `val` 的元素的个数。

![image-20250820175136732](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820175136732.png)

> I used two pointers for this question.

> The slow pointer starts at index 0.

> I used a fast pointer to iterate through the entire `nums` array. If the fast pointer points to a value equal to `val`, I skip it. If it’s not equal, I assign the current value to the slow pointer’s position and increment the slow pointer.

> Tips: I spent too much time deciding whether to use a `while` loop or a `for` loop. For this problem, a `for` loop is definitely the better choice.

> **Time Complexity**: O(n) -> for loop  for nums.length

> **Space Complexity**: O(1)  int n, int slow

---

## 977. Squares of a Sorted Array
**题目链接**: [LeetCode 977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

**English**  
Given an integer array `nums` sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

**中文**  
给你一个按非递减顺序排序的整数数组 `nums`，返回一个由每个数的平方组成的新数组，要求也按非递减顺序排序。

![image-20250820191014189](/Users/fengweiren/Library/Application Support/typora-user-images/image-20250820191014189.png)

> I declared a new array with the same length as nums to store the results. I used two pointers with a while loop: the left pointer starts at index 0, and the right pointer starts at nums.length - 1.

> Regardless of whether the array includes negative numbers or not, I compared the square (or absolute value) of the elements at the left and right pointers, and added the larger one to the end of the result array. Then I moved the corresponding pointer: either left++ or right--.

> Be careful: the termination condition is left <= right, and it’s important to handle the case when left == right.

> **Time Complexity**: O(n), because we iterate through the array once

> **Space Complexity**: O(n), due to the additional array used to store the result. Variables like left and right only use constant space (O(1))