# Two Sum IV - Input is a BST

> [leetcode > 653 > Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst)
- 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. 주어진 유효한 이진검색트리에서 두개의 요소의 합이 k가 되는 경우가 있는지 여부를 반환하는 문제
2. DFS + HashTable or BFS + HashTable

## 코드 1

```kotlin
fun findTarget(root: TreeNode?, k: Int): Boolean {
    val hashSet = HashSet<Int>()
    return dfs(root, k, hashSet)
}

private fun dfs(
    root: TreeNode?,
    k: Int,
    hashSet: HashSet<Int>
): Boolean {
    if (root == null) return false
    if (hashSet.contains(k - root.`val`)) { // left + right == k -> k - left == right
        return true
    }
    hashSet.add(root.`val`)
    return dfs(root.left, k, hashSet) || dfs(root.right, k, hashSet)
}

private fun bfs(
    root: TreeNode?,
    k: Int
): Boolean {
    if (root == null) return false
    val hashSet = HashSet<Int>()
    val queue = LinkedList<TreeNode>()
    queue.offer(root)
    while (queue.isNotEmpty()) {
        val treeNode = queue.poll()
        if (hashSet.contains(k - treeNode.`val`)) {
            return true
        }
        hashSet.add(treeNode.`val`)
        if (treeNode.left != null) {
            queue.offer(treeNode.left)
        }
        if (treeNode.right != null) {
            queue.offer(treeNode.right)
        }
    }
    return false
}
```

## 배운 점
1. 균형 이진 트리는 두 하위 트리의 깊이(depth)가 1이 넘게 차이나지 않는 것을 의미힌다.
2. 두 노드의 합이 k와 같은지 비교 `leftNode + rightNpde == k` -> `k - leftNode == rightNpde`
3. 오랜만에 dfs, bfs 복습


