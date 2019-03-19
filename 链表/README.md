

# 单链表反转

##　递归法
```
static Node reverseLinkedList(Node node) {
    if (node == null || node.next == null) {
        return node;
    } else {
        Node headNode = reverseLinkedList(node.next);
        node.next.next = node;
        node.next = null;
        return headNode;
    }
}
```

##　遍历法
```
public static Node reverse(Node node) {
    Node first = node;
    Node reverse = null;        //reverse用于储存前一节点，second用于储存后一节点*
    while (first != null) {
        Node second = first.next;    
        first.next = reverse;       
        reverse = first;              
        first = second;
    }

    return reverse;
}
```




