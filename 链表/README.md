
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

## 查找单链表中的中间结点
```
public static Node findMidNode(Node head){
    if(node == null) return null;
    
    Node ri = head;
    Node r2 = head;
    while(r2 != null && r2.next != null){
        r1 = r1.next;
        r2 = r2.next.next;
    }
    return r1;
}
```

## 合并两个有序的单链表，合并之后的链表依然有序
```
public static Node mergeLinkList(Node head1,Node head2){
    if(head1 == null || head2 == null){
        if(head1 == null && head2 == null) return null;
        else return head1 == null ? head2 : head1;
    }
    //一个保持新链表的头节点，一个保存现在的指向
    Node temp;
    Node curhead;
    if(head1.val > head2.val) 
        curhead = head2;
        temp = head2;
        head2 = head2.next;
    else {
        curhead = head1;
        temp = head1;
        head1 = head1.next;
    }
    
    while(head1 != null || head2 != null){
        if(head1 != null && head2 !=null){
            if(head1.val > head2.val){
                temp.next = head2;
                head2 = head2.next;
            }
            else {
                temp.next = head1;
                head1 = head1.next;
            }
        }
        if(head1 == null){
            temp.next = head2;
            head2 = head2.next;
        }
        else {
            temp.next = head1;
            head1 = head1.next;
        }
    }
    return curhead;
}
```

## 从尾到头打印单链表
```
public staic viod reversePrint(Node head){
    if(head != null) return;
    reversePrint(head.next);
    System.out.print(head.val + "-->")
}

```

## 判断单链表是否有环

```
public static boolean hasCycle(Node head){
    if(head == null) return false;
    Node r1 = head;
    Node r2 = head;
    while(r2 != null){
    r1 = ri.next;
    r2 = r2.next.next;
    if(r1 == r2) return ture;
    }
    retrun false;
}
```

##  取出有环链表中，环的长度
```
//返回环中的一个节点r1
public static Node getCycleNode(Node head){
    if(head == null) return null;
    Node r1 = head;
    Node r2 = head;
    while(r2 != null){
        r1 = ri.next;
        r2 = r2.next.next;
        if(r1 == r2) return r1;
    }
}
//从r1开始，遍历环，若遍历到与r1相同处，则返回环的长度。
public static int getCycleLength(Node node){
    if(head == null) return 0;
    Node r = getCycleNode(node);
    Node r2 = r;
    int count = 0;
    while(r != null){
        r = r.next;
        count++;
        if(r == r2)
            break;
    }
    return count；
}
```












































