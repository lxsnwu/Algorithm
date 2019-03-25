[toc]

## 单链表反转

### 递归法
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
[toc]

### 遍历法
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

## 求单链表节点的个数
```
public static int getLength(Node head){
    if(node == null) return 0;
    int length = 0;
    Node temp = head;
    while(node != null){
        length++;
        temp = temp.next
    }
    return length;
}
```

## 查找单链表中的倒数第k个结点
```
public static Node findLastNode(Node head,int index){
    if(node == null) return null;
    
    Node r1 = head;
    Node r2 = head;
    for(int i = 0 ; i<k ; i++){
        r1 = r1.next;
        if(r1 == null) return null;
    }
    while(r1.next != null){
        r2 = r2.next
    }
    return r2;
}

```














