## 问题

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。



## 示例

```json
输入：head = [1,3,2]
输出：[2,3,1]
```





## 代码

### 模拟

```java
 class Solution {
    public int[] reversePrint(ListNode head) {
        int len = 0;
        ListNode node = head;

        while(node != null){
            len++;
            node = node.next;
        }
        node = head;
        int[] arr = new int[len];
        for(int i = 0; i < len; i++){
            arr[len - i - 1] = node.val;
            node = node.next;
        }

        return arr;
    }
}
```



### 递归

```java
class Solution {
    ArrayList<Integer> tmp = new ArrayList<>();
    
    public int[] reversePrint(ListNode head) {
        recur(head);
        int[] res = new int[tmp.size()];
        
        for(int i = 0; i < res.length; i++)
            res[i] = tmp.get(i);
        
        return res;
    }
    
    void recur(ListNode head) {
        if(head == null) return;
        
        recur(head.next);
        tmp.add(head.val);
    }
}
```



###  辅助栈

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        LinkedList<Integer> stack = new LinkedList<>();
        
        while(head != null) {
            stack.addLast(head.val);
            head = head.next;
        }
        int[] res = new int[stack.size()];
        for(int i = 0; i < res.length; i++)
            res[i] = stack.removeLast();
    	
        return res;
    }
}
```

