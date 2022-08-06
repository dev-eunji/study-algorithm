# Binary Tree Level Order Traversal

> [leetcode > 102 > Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Tree]

## 해결 과정

1. queue를 활용한 BFS 이진트리 탐색


## 코드 1

``` kotlin (BFS)
fun levelOrder(root: TreeNode?): List<List<Int>> {
    val levelOrder: ArrayList<List<Int>> = ArrayList()
    if (root == null) {
        return levelOrder
    }

    val queue = LinkedList<TreeNode>()
    queue.offer(root)
    while (queue.isNotEmpty()) {

        val childList = mutableListOf<Int>()
        for (i in 0 until queue.size) {
            val currentNode = queue.poll()
            childList.add(currentNode.`val`)

            if (currentNode.left != null) {
                queue.offer(currentNode.left)
            }
            if (currentNode.right != null) {
                queue.offer(currentNode.right)
            }
        }

        levelOrder.add(childList)
    }
    return levelOrder
}
```

``` kotlin (재귀)
private fun groupByLevelTraversal(
    levels: MutableList<List<Int>>,
    queue: Queue<TreeNode>
): List<List<Int>> {

    if (queue.isEmpty()) {
        return levels
    }

    val currentNodes: MutableList<Int> = LinkedList()
    for (i in 0 until queue.size) {
        val node = queue.poll()
        currentNodes.add(node.`val`)
        if (node.left != null) queue.add(node.left)
        if (node.right != null) queue.add(node.right)
    }
    levels.add(currentNodes)
    return groupByLevelTraversal(levels, queue)
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` java
public List<List<Integer>> levelOrder(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    List<List<Integer>> wrapList = new LinkedList<List<Integer>>();

    if(root == null) return wrapList;

    queue.offer(root);
    while(!queue.isEmpty()){
        int levelNum = queue.size();
        List<Integer> subList = new LinkedList<Integer>();
        for(int i=0; i<levelNum; i++) {
            if(queue.peek().left != null) queue.offer(queue.peek().left);
            if(queue.peek().right != null) queue.offer(queue.peek().right);
            subList.add(queue.poll().val);
        }
        wrapList.add(subList);
    }
    return wrapList;
}
```

## 배운 점
1. 이차원 배열 및 리스트 생성 복습 (IDE 없이 사용 할 수 있도록..)
 - `val levelOrder: ArrayList<List<Int>> = ArrayList()`
 - `val levelOrder: MutableList<List<Int>> = mutableListOf()`
 - `val levelOrder: MutableList<List<Int>> = LinkedList()`

2. 이진트리 탐색 너무 오랜만에 복습

