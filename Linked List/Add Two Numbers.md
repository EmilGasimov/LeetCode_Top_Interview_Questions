You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: `(2 -> 4 -> 3) + (5 -> 6 -> 4)`

Output: `7 -> 0 -> 8`
Explanation: 342 + 465 = 807.

### Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode walk1 = l1, walk2 = l2, head0 = new ListNode(0); 
        ListNode sum = head0;
        while(walk1 != null || walk2 != null) {
            sum.next = new ListNode(0);
            if(walk1 == null && walk2 != null) {
                int n = (sum.val + walk2.val)/10, rem = (sum.val + walk2.val)%10;
                sum.val = rem; sum.next.val = n;
            }
            else if(walk1 != null && walk2 == null) {
                int n = (sum.val + walk1.val)/10, rem = (sum.val + walk1.val)%10;
                sum.val = rem; sum.next.val = n;
            }
            else {
                int n = (sum.val + walk1.val + walk2.val)/10, rem = (sum.val + walk1.val + walk2.val)%10;
                sum.val = rem; sum.next.val = n;
            } 
            sum = sum.next; if(walk1 != null) walk1 = walk1.next; if(walk2 != null) walk2 = walk2.next;                        
        }
        ListNode head = head0;
        while(head.next.next != null) head = head.next;
        if(head.next.val==0) head.next = null;
        return head0; 
    }
}
```
