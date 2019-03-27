



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
    Queue<TreeNode> queue =  new LinkedList<TreeNode>(); // 用队列保存树节点，先进先出
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
   if (root == null) 
       return 0;
   return Math.max(getDepthRec(root.left), getDepthRec(root.right)) + 1;
}
```
还有一种写法：
```
    public static int getDepthRec(TreeNode root) {
        if(root == null)
            return 0;
        int l = getDepthRec(root.left);
        int r = getDepthRec(root.right);
        return l > r ? l + 1 : r + 1;
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


## 叉树的直径（两节点的最长路径）
 根节点为root的二叉树的直径 = max(root.left的直径，root.right的直径，
root.left的最大深度+root.right的最大深度+1)
```
    class Solution{
        int max = 0;
        public int depthTree(TreeNode root){
            if(root == null) return 0;
            else
                return Math.max(TreeNode(root.left),TreeNode(root.right)) + 1;        
        }
        
        public int maxDepthTree(TreeNode root){
            if(root == null) return 0;
            int depthlr = depthTree(root.left)+depthTree(root.right)+1
            max =  Math.max(depthlandr,max);
            
            maxDepthTree(root.left);
            maxDepthTree(root.right);
            
            return max;
        }
```

## 统计树中结点的个数
树中结点的个数等于根节点(1) + 左子树结点个数 + 右子树的个数，递归求解即可。

```
public static int count(Node T) {
	if(T != null) {
		return count(T.left) + count(T.right) + 1;
	}else 
		return 0;
	}
```


## 求二叉树第k层的节点个数
递归解法： O(n)O(n)
思路：求以root为根的k层节点数目，等价于求以root左孩子为根的k-1层（因为少了root）节点数目 加上以root右孩子为根的k-1层（因为 少了root）节点数目。即：

1.如果二叉树为空或者k<1，返回0
2.如果二叉树不为空并且k==1，返回1
3.如果二叉树不为空且k>1，返回root左子树中k-1层的节点个数与root右子树k-1层节点个数之和
```
public int kNum(TreeNode root,int k){
	if(root == null || k < 1) return 0;
	if(k == 1) return 1;
	return kNum(root.left,k-1) + kNum(root.right,k-1) +1;
```

## 求二叉树的镜像
操作给定的二叉树，将其变换为源二叉树的镜像。如下图：
![avatar](https://img-blog.csdn.net/20180401215350230?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p4enh6eDAxMTk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

递归求解的过程:
1.先把当前根节点的左右子树换掉；
2.然后递归换自己的左右子树；

```
public void minorTree(TreeNode root){
	if(root == null) return;
	TreeNode temp = root.left;
	root.left = root.right;
	root.right = temp;
	minorTree(root.left);
	minorTree(root.right);
}
```































