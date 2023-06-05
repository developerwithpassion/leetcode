## 问题

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。





## 示例

```json
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```





## 代码

### 回溯 + 哈希表

```java
class Solution {
    // 哈希表记录每一节点对应的新节点
    // 检查”后继节点“和”随机指向节点“
    Map<Node, Node> cachedNode = new HashMap<>();

    // 
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }
        // 防止重复拷贝
        if (!cachedNode.containsKey(head)) {
            Node headNew = new Node(head.val);
            cachedNode.put(head, headNew);
            headNew.next = copyRandomList(head.next);
            headNew.random = copyRandomList(head.random);
        }

        return cachedNode.get(head);
    }
}
```



### 迭代 + 节点拆分 

```java
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        for (Node node = head; node != null; node = node.next.next) {
            Node nodeNew = new Node(node.val);
            nodeNew.next = node.next;
            node.next = nodeNew;
        }
        for (Node node = head; node != null; node = node.next.next) {
            Node nodeNew = node.next;
            nodeNew.random = (node.random != null) ? node.random.next : null;
        }
        Node headNew = head.next;
        for (Node node = head; node != null; node = node.next) {
            Node nodeNew = node.next;
            node.next = node.next.next;
            nodeNew.next = (nodeNew.next != null) ? nodeNew.next.next : null;
        }
        
        return headNew;
    }
}
```

