# Merge Two Binary Trees

> [leetcode > 617 > Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Graph/BFS/DFS]

## 해결 과정

1. 주어진 Binary Trees 2개의 더한 하나의 트리 리턴
2. DFS


## 코드 1

```kotlin
fun mergeTrees(root1: TreeNode?, root2: TreeNode?): TreeNode? {
    if (root1 == null && root2 == null) return null

    if (root1 == null) {
        return root2
    }
    if (root2 == null) {
        return root1
    }

    val mergeTree = TreeNode(root1.`val` + root2.`val`)
    mergeTree.left = mergeTrees(root1?.left, root2?.left)
    mergeTree.right = mergeTrees(root1?.right, root2?.right)

    return mergeTree
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
class Solution 
{
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) 
    {//Postorder Traversal   
        if(root1 == null)//when we see that the root1 is null there is a possibility that root2 is not null so we return that and maintaining the link and continue overlapping
           return root2;//telling that root1 is not present so sending root1
      
        if(root2 == null)//when we see that the root2 is null there is a possibility that root1 is not null so we return that and maintaining the link  
           return root1;//telling that root2 is not present so sending root1
   
        //LEFT - RIGHT
        TreeNode left= mergeTrees(root1.left, root2.left);//recursing down the left subtree and knowing about the left child 
        TreeNode right= mergeTrees(root1.right, root2.right);//recursing down the right subtree and knowing about the right child 
      
        //ROOT
        //creating the node by the total information received from left and right child 
        TreeNode node= new TreeNode(root1.val+root2.val, left, right);
      
        return node;//returning the node in order to maintain the backward modified link at each instant//Telling to the parent that I am present  
    }
}//Please do Upvote, it helps a lot 
```


