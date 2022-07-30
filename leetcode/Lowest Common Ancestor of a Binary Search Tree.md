# Binary Search Tree

> [leetcode > 235 > Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Binary Search Tree]

## 해결 과정

1. 재귀 방식, Iterative 동일한 조건으로 탐색
 - root가 주어진 두노드보다 클 경우 작은 값인 왼쪽 노드를 재귀로 탐색
 - root가 두노드보다 작을 경우는 더 큰값을 탐색하기 위해 오른쪽 노드를 탐색
 - else root 반환


## 코드 1 (Recursive, Iterative)

```kotlin (Recursive)
fun lowestCommonAncestor(root: TreeNode?, p: TreeNode?, q: TreeNode?): TreeNode? {
    if (root == null) {
        return null
    }
    val rootValue = root.`val`
    val pValue = requireNotNull(p).`val`
    val qValue = requireNotNull(q).`val`

    if (rootValue > pValue && rootValue > qValue) { // root가 주어진 두노드보다 클 경우 작은 값인 왼쪽 노드를 재귀로 탐색
        return lowestCommonAncestor(
            root = root.left,
            p = p,
            q = q
        )
    } else if (rootValue < pValue && rootValue < qValue) { // root가 두노드보다 작을 경우는 더 큰값을 탐색하기 위해 오른쪽 노드를 탐색
        return lowestCommonAncestor(
            root = root.right,
            p = p,
            q = q
        )
    }
    return root
}
```

```kotlin (Iterative)
fun lowestCommonAncestor(root: TreeNode?, p: TreeNode?, q: TreeNode?): TreeNode? {
    var rootNode = root

    while (rootNode != null) {
        val rootValue = rootNode.`val`
        val pValue = requireNotNull(p).`val`
        val qValue = requireNotNull(q).`val`
        rootNode = if (rootValue > pValue && rootValue > qValue) {
            rootNode.left
        } else if (rootValue < pValue && rootValue < qValue) {
            rootNode.right
        } else {
            return rootNode
        }
    }
    return null
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```Python
def lowestCommonAncestor(self, root, p, q):
    while (root.val - p.val) * (root.val - q.val) > 0:
        root = (root.left, root.right)[p.val > root.val]
    return root
```

```Java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    while ((root.val - p.val) * (root.val - q.val) > 0)
        root = p.val < root.val ? root.left : root.right;
    return root;
}
```

## 배운 점
1. `requireNotNull` 매개변수의 값이 null이 아니면 value를 반환, null이면  throw IllegalArgumentException
- 알고리즘 테스트에 유용 하게 사용하면 좋을것 같다. !! 보다는 좋을 것 같음
```Kotlin
public inline fun <T : Any> requireNotNull(value: T?): T {
    contract {
        returns() implies (value != null)
    }
    return requireNotNull(value) { "Required value was null." }
}
```
