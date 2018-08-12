---
layout: post
title:  "82. 删除排序链表中的重复元素 II"
categories: 算法
tags: leetcode 链表
---

* content
{:toc}

<!--more-->

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:

```
输入: 1->2->3->3->4->4->5
输出: 1->2->5
```

示例 2:

```
输入: 1->1->1->2->3
输出: 2->3
```

解：

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode newhead = new ListNode(-1);
        ListNode tmp = newhead;

        while (head != null && head.next != null) {
            if (head.val == head.next.val) {
                while (head.next != null && head.val == head.next.val) {
                    head = head.next;
                }
                head = head.next;
            } else {
                tmp.next = head;
                tmp = tmp.next;
                head = head.next;
            }
        }
        
        tmp.next = head;

        return newhead.next;
    }
}
```