## 问题

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。



## 示例

```json
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```



## 代码

### 模拟

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        ListNode temp = new ListNode(-1);

        while(cur != null){
            temp = cur.next;

            cur.next = pre;
            pre = cur;

            cur = temp;
        }

        return pre;
    }
}
```



### 迭代

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        
        return prev;
    }
}
```



### 递归

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode newHead = reverseList(head.next);
        
        head.next.next = head;
        head.next = null;
        
        return newHead;
    }
}
```

