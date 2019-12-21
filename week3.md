# 1. Algorithm
2. 两数相加<br>
给出两个非空的链表用来表示两个非负的整数。其中，它们各自的位数是按照逆序的方式存储的，并且它们的每个节点只能存储一位数字。如果,我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。<br>
**解法1:**
``` java
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
        ListNode order = new ListNode(0);
        ListNode movePoint = order;
        ListNode l1Item = l1;
        ListNode l2Item = l2;
        // 是否需要进一的标志
        boolean needAdd1 = false;
        do {
            int nodeVal = 0;
            // 判断其中一个节点为空的情况
            if (l1Item == null){
                nodeVal = l2Item.val;
            } else if (l2Item == null){
                nodeVal = l1Item.val;
            } else {
                nodeVal = l1Item.val + l2Item.val;
            }
            if (needAdd1) {
                nodeVal ++;
            }
            if (nodeVal > 9){
                needAdd1 = true;
                nodeVal = nodeVal - 10;
            } else {
                needAdd1 = false;
            }
            movePoint.next = new ListNode(nodeVal);
            if (l1Item != null){
                l1Item = l1Item.next;
            }            
            if (l2Item != null){
                l2Item = l2Item.next;
            }            
            movePoint = movePoint.next;
        } while (l1Item != null || l2Item != null);
        if (needAdd1) {
            movePoint.next = new ListNode(1);
        }    
        return  order.next;
    }
}
```




