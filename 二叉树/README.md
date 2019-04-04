



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
	TreeNode temp;
	while(!queue.isEmpty()){
		temp = queue.poll();
		System.out.print(temp.val + " ");
		if(temp.left != null) queue.offer(temp.left);
		if(temp.right != null) queue.offer(temp.right);
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

![avatar](https://s3.51cto.com/wyfs02/M00/7F/6D/wKiom1cd-Sui13McAAAbohCxaF4564.png)

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

## 二叉树的右视图
-leetcode199
```
解释:

   1         <---
 /   \
2     3      <---
 \     \
  5     4    <---
```
思路解析：层序遍历，找到最右边的节点即可

```
public ArrayList<Integer> rightSideView(TreeNode root){
	if(root == null) return null;
	ArrayList<Integer> arr = new ArrayList<Integer>();
	Queue<TreeNode> queue = new LinkList<TreeNode>();
	TreeNode temp = root;
	queue.offer(temp);
	while(!queue.isEmpty()){
		int size = queue.size();
		for(int i=0;i<size;i++){
			temp = queue.pop();
			if(i = size-1) arr.add(temp.val);
			if(temp.left!=null) queue.offer(temp.left);
			if(temp.right!=null) queue.offer(temp.right);
		}	
	}
	return arr;
}
```

## 给定一个二叉树，原地将它展开为链表。

例如，给定二叉树
```
    1
   / \
  2   5
 / \   \
3   4   6
将其展开为：

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

```
    public void flatten(TreeNode root) {
        if(root == null) return;
        if(root.left == null && root.right == null) return;
        LinkedList<TreeNode> queue = new LinkedList<>();
        Stack<TreeNode> stack      = new Stack<>();
        TreeNode currentNode       = null;
        stack.push(root);
        while(!stack.isEmpty()){
            currentNode = stack.pop();
            queue.add(currentNode);
            if(currentNode.right != null) {
                stack.push(currentNode.right);
            }
            if(currentNode.left != null) {
                stack.push(currentNode.left);
            }
        }
        currentNode = root;
        while(queue.size() > 0){
            currentNode.left  = null;
            currentNode.right = queue.poll();
            currentNode       = currentNode.right;
        }
    }
```

递归法：
```
    public void flatten(TreeNode root) {
        if(root == null) return;
        flatten(root.left);
        flatten(root.right);
        if(root.left != null){
            TreeNode node = root.left;
            while(node.right != null){
                node = node.right;
            }
            node.right = root.right;
            root.right = root.left;
	    //左树置空
            root.left = null;
        }
        
    }
```


## 二叉树中的最大路径

给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。
```
示例 1:
输入: [1,2,3]

       1
      / \
     2   3

输出: 6
示例 2:
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7
  
输出: 42
```

思路解析：
  对于任意一个节点, 如果最大和路径包含该节点, 那么只可能是两种情况:
1. 其左右子树中所构成的和路径值较大的那个加上该节点的值后向父节点回溯构成最大路径
2. 左右子树都在最大路径中, 加上该节点的值构成了最终的最大路径
这道题的遍历顺序应该是post-order（左右根） 自下向上的记录最大路径和，返回包含此节点和此节点的一个叉的最大值。

```
class Solution {
    
    private int ret = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {

        getMax(root);
        return ret;
    }
    
    private int getMax(TreeNode root) {
        if(root == null) return 0;
        int left = Math.max(0, getMax(root.left)); // 如果子树路径和为负则应当置0表示最大路径不包含子树
        int right = Math.max(0, getMax(root.right));
        ret = Math.max(ret, root.val + left + right); // 判断在该节点包含左右子树的路径和是否大于当前最大路径和
        return Math.max(left, right) + root.val;
    }
}
```
我们可以这样理解。
1.对于一个root来说，我们先记录他的左树（left）和右树（right）的值。用ret记录最大路径和（左树 + 右树 + root）
	
2.在递归过程中，不断比较每个节点（root）与原来ret的大小关系。























