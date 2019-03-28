



## 二叉树中的节点个数
递归法
```
public int getNodeNum(TreeNode root){
	if(root == null) return 0;
	return getNodeNum(root.left) + getNodeNum(root.right) + 1;
}
```

非递归法
```
public int getNodeNum(TreeNode root) {
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

## 判断二叉树是不是平衡二叉树
递归实现：借助前面实现好的求二叉树高度的函数

1.如果二叉树为空， 返回真
2.如果二叉树不为空，如果左子树和右子树都是AVL树并且左子树和右子树高度相差不大于1，返回真，其他返回假
```
public static boolean isAVLTree(TreeNode root) {
    if (root == null) {
        return true;
    }
    if (Math.abs(getDepthRec(root.left) - getDepthRec(root.right)) > 1) { // 左右子树高度差大于1
        return false;
    }
    return isAVLTree(root.left) && isAVLTree(root.right); // 递归判断左右子树
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


## 求二叉树中叶子节点的个数
递归解法：

1.如果二叉树为空，返回0
2.如果二叉树是叶子节点，返回1
3.如果二叉树不是叶子节点，二叉树的叶子节点数 = 左子树叶子节点数 + 右子树叶子节点数
```
public int TreeLeaf(TreeNode root){
	if(root == null) return 0;
	if(root.left == null && root.right == null){
		return 1;
	}
 	return TreeLeaf(root.left) + TreeLeaf(root.right);
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

例如：
  翻转前：     翻转后：
    1     |     1
   / \    |    / \
  2   3   |   3   2
 / \      |      / \
4   5     |     5   4

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


## 求二叉树中两个节点的最低公共祖先节点
递归解法：
1.如果两个节点分别在根节点的左子树和右子树，则返回根节点
2.如果两个节点都在左子树，则递归处理左子树；如果两个节点都在右子树，则递归处理右子树

```
//判断树中是否包含某节点
public boolean hasNode(TreeNode root,TreeNode node){
	if(root == null) return null;
	if(root.left == node || root.right == node)
		return true;
	else return hasNode(root.left,node) || hasNode(root.right,node);
}

//求公共节点
public TreeNode comNode(TreeNode root,TreeNode n1,TreeNode n2){
	if(root == n1) return n1;
	if(root == n1) return n2;
	else{
	     if(hasNode(root.left,n1)){
		if(hasNode(root.right,n2))
			return root;
			else comNode(root.left,n1,n2)
		}
	} else {
		if(hasNode(root.right,n1)){
			if(hasNode(root.left,n2))
				return root;
			else comNode(root.right,n1,n2)
			}
		}
}
```






















