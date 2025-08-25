# Day 4 Notes

## 24. Swap Nodes in Pairs

**题目链接**: [LeetCode 24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

**English**
 Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**中文**
 给你一个链表，两两交换其中相邻的节点，并返回交换后的链表。你必须在不修改节点内部的值的情况下完成本题（也就是说，仅仅交换节点本身）。

![image-20250824153544339](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250824153544339-6074944.png)

> This problem can be solved using two approaches: an iterative method and a recursive method.
>
> For the **iterative solution**, I first initialized a new node called `dummy`, and set `dummy.next = head`. Then I declared a `cur` pointer and assigned it to the `dummy` node.
>
> I used a `while` loop to traverse the entire list. The base case for the loop is that both `cur.next` and `cur.next.next` are not `null`, meaning we have at least two nodes to swap.
>
> Inside the loop:
>
> - I stored the two nodes to be swapped in temporary variables: `first = cur.next` and `second = cur.next.next`.
> - Then, I performed the swap:
>   - `first.next = second.next`
>   - `second.next = first`
>   - `cur.next = second`
>
> After the swap, I moved `cur` forward two steps using `cur = first`.
>
> Finally, I returned `dummy.next`, which is the new head of the swapped list.

> **Time Complexity**: O(n)  Length of LinkedList

> **Space Complexity**: O(1)  dummyHead, a few variables

![image-20250824154930919](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250824154930919-6075770.png)

> The recursive solution is very clean and elegant.
>
> First, I check the base case: if `head == null` or `head.next == null`, I return `head` directly — no need to swap.
>
> Otherwise, I store `head.next` in a variable `second`, and then recursively call the function on `second.next`, assigning the result to `head.next`. This links the current node’s next to the result of recursively swapping the rest of the list.
>
> Then I set `second.next = head` to complete the current pair’s swap, and finally return `second`, which becomes the new head for this segment of the list.
>
> **Time Complexity**: O(n)  Length of LinkedList

> **Space Complexity**: O(n)  Each recursion creates a Stack Frame

------

## 19. Remove Nth Node From End of List

**题目链接**: [LeetCode 19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

**English**
 Given the `head` of a linked list, remove the `n`th node from the end of the list and return its head.

**中文**
 给你一个链表，删除链表的倒数第 `n` 个节点，并返回链表的头节点。

![image-20250824165622200](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250824165622200-6079782.png)

> This problem is a classic example of the two-pointer technique.
>
> First, I initialized a dummy node and set `dummy.next = head`. This helps handle edge cases where the head might be removed.
>
> I then initialized two pointers:
>
> - `fast` starts from the `head`
> - `slow` starts from the `dummy`
>
> The idea is to move the `fast` pointer `n` steps forward first. Once that’s done, I move both `fast` and `slow` one step at a time until `fast` reaches the end of the list (`null`).
>
> At that point, `slow.next` is the node to be deleted. So to remove it, I simply do: slow.next = slow.next.next;
>
> Finally, I return `dummy.next` as the new head of the list.
>
> **Time Complexity**: O(n)  Length of LinkedList

> **Space Complexity**: O(1)  Few vairables

------

## 160. Intersection of Two Linked Lists

**题目链接**: [LeetCode 160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

**English**
 Given the heads of two singly linked lists `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return `null`.

**中文**
 给你两个单链表的头节点 `headA` 和 `headB`，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null`。

![image-20250824181043110](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250824181043110-6084243.png)

> ### Method 1: Length Alignment (Brute-force but reliable)
>
> First, I check if either `headA` or `headB` is null. If either is null, there can't be an intersection, so return `null`.
>
> Then I create two pointers:
>
> - `node1` starting at `headA`
> - `node2` starting at `headB`
>
> I also initialize two variables `size1` and `size2` to calculate the lengths of both lists.
>
> After traversing each list to get its length, I reset `node1` and `node2` back to the heads. Then I calculate the absolute difference between the lengths.
>
> To align both pointers:
>
> - If `size1 > size2`, I move `node1` forward by `size1 - size2` steps
> - If `size2 > size1`, I move `node2` forward by `size2 - size1` steps
>
> Now both pointers are the same distance away from the potential intersection. I iterate through both lists in a `while` loop:
>
> - If `node1 == node2`, return the intersection node
> - Otherwise, move both pointers forward until they meet or reach the end
>
> If there is no intersection, both pointers will eventually become `null`, and we return `null`. 
>
> **Tips**: Remember to keep moving `node1` and `node2` forward until they meet at the intersection node.
>
> **Time Complexity**: O(m + n) Length of two LinkedLists

> **Space Complexity**: O(1)  Few vairables

![image-20250824185335931](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250824185335931-6086815.png)

> ### Method 2: Two-Pointer Redirection (Elegant & Space Efficient)
>
> This is a very elegant and efficient approach.
>
> First, check the base case — if either `headA` or `headB` is null, return `null`.
>
> Then I initialize two pointers:
>
> - `pa` pointing to `headA`
> - `pb` pointing to `headB`
>
> Then I use a `while (pa != pb)` loop. In each iteration:
>
> - If `pa` becomes null, reassign it to `headB`, otherwise move to `pa.next`
> - If `pb` becomes null, reassign it to `headA`, otherwise move to `pb.next`
>
> Eventually, either the two pointers will meet at the intersection node, or they will both reach `null` (no intersection). In either case, we return `pa` (or `pb`, since they are equal at the end).
>
> This method works because by switching heads, both pointers travel equal total distances.
>
> Tips: ![image-20250824190614180](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250824190614180-6087574.png)
>
> **Time Complexity**: O(n)  Length of LinkedList

> **Space Complexity**: O(1)  Few vairables

------

## 142. Linked List Cycle II

**题目链接**: [LeetCode 142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

**English**
 Given the `head` of a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

**中文**
 给定一个链表的头节点 `head`，返回链表开始入环的第一个节点。如果链表无环，则返回 `null`。

![image-20250825010435828](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250825010435828-6109075.png)

> First, I use two pointers, `slow` and `fast`. `slow` moves one step at a time, `fast` moves two steps. If there is a cycle, the two pointers will eventually meet inside the cycle.
>
> Once they meet, I set one pointer (`index1`) at the meeting point, and another pointer (`index2`) at the head. I move both pointers one step at a time. The node where they meet again is the entry point of the cycle.
>
> To understand why this works, I looked into the math. Let:
>
> - `x` be the distance from head to the cycle entry
> - `y` be the distance from the entry to the meeting point
> - `z` be the remaining distance in the cycle from the meeting point back to the entry
>
> So, the total length of the cycle is `y + z`.
>
> When the two pointers meet:
>
> - `slow` has traveled `x + y` steps
> - `fast` has traveled `x + y + n(y + z)` steps (where `n` is the number of full loops fast made in the cycle)
>
> Because `fast` moves twice as fast, we can say: 2(x + y) = x + y + n(y + z)
>
> Subtract `x + y` from both sides: x + y = n(y + z)
>
> Solve for `x`: x  = n(y + z) - y  
>   			  = (n - 1)(y + z) + z
>
> This equation shows that the distance from the head to the cycle entry (`x`) is exactly equal to the distance from the meeting point to the entry (`z`), after `(n - 1)` full cycles.
>
> That’s why, if I start one pointer at the head and one at the meeting point, and move them both one step at a time, they will meet at the cycle entry.
>
> This method is guaranteed to find the entry point and doesn’t modify the original list.
>
> **Tips**: Images from Carl
>
> ![image-20250825010730476](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250825010730476-6109250.png)
>
> ![image-20250825010743508](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250825010743508-6109263.png)
>
> ![image-20250825010823086](/Users/fengweiren/Downloads/LeetCode/leetcode-solutions/images/image-20250825010823086-6109303.png)
>
> **Time Complexity**: O(n) - where n is the number of nodes
>
> - Phase 1: Detect cycle - O(n)
> - Phase 2: Find entrance - O(n)

> **Space Complexity**: O(1) - only using pointer variables

------