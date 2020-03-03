Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists begin to intersect at node c1.

![image](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)



### Solution 

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode A = headA, B = headB;
        int a = 0, b = 0; 
        while(A != null) {
            A = A.next; a++;
        }
        while(B != null) {
            B = B.next; b++;
        }
        A = headA; B = headB;
        if(a > b) {
            while(a > b) {
                A = A.next; a--;
            }
            while(A != B) {
                A = A.next; B = B.next;
            }
        }
        else if(a < b) {
            while(a < b) {
                B = B.next; b--;
            }
            while(A != B) {
                A = A.next; B = B.next;
            }
        }
        else {
            while(A != B) {
                A = A.next; B = B.next;
            }
        }
        return A;
    }
}
```
