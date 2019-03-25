



## 二叉树中的节点个数
``` 
/**
* 1. 求二叉树中的节点个数
* 非递归
* @param root 树根节点
* @return 节点个数
*/
public static int getNodeNum(TreeNode root) {
    if (root == null) {
        return 0;
    }
    Queue<TreeNode> queue =  new LinkedList<>(); // 用队列保存树节点，先进先出
    queue.add(root);
    int count = 1; // 节点数量
    while (!queue.isEmpty()) {
        TreeNode temp = queue.poll(); // 每次从对列中删除节点，并返回该节点信息
        if (temp.left != null) { // 添加左子孩子到对列
            queue.add(temp.left);
            count++;
        }
        if (temp.right != null) { // 添加右子孩子到对列
            queue.add(temp.right);
            count++;
        }
    }
    return count;
}
```

## 求二叉树的深度（高度）
```
如果二叉树为空，二叉树的深度为0
如果二叉树不为空，二叉树的深度 = max(左子树深度， 右子树深度) + 1
/**
* 求二叉树的深度（高度）
* 递归
* @return 树的深度
*/
public static int getDepthRec(TreeNode root) {
   if (root == null) {
       return 0;
   }
   return Math.max(getDepthRec(root.left), getDepthRec(root.right)) + 1;
}
```


## 二叉树的层次遍历
```
public static void levelTraver(TreeNode root){
	if(node == null) return;
	Queue<TreeNode> queue = new ArrayDeque<TreeNode>();
	queue.offer(root);
	Node temp;
	while(!queue.isEmpty){
		temp = queue.poll();
		System.out.print(temp.val + " ");
		if(root.left != null) queue.offer(root.left);
		if(root.right != null) queue.offer(root.right);
	}
}
```


















