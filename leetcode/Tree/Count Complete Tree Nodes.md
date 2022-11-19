#  Count Complete Tree Nodes

> [leetcode > 222 >  Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes)
- 출처: leetcode, [https://leetcode.com]

- Level Medium

## 해결 과정

1. 이진 트리의 노드를 반환하는 문제
2. Bfs 재귀로 푸는 방법


## 코드 1

```kotlin
fun countNodes(root: TreeNode?): Int {
    if (root == null) return 0

    if (root?.left == null && root?.right == null) {
        return 1
    }

    var counter = 0
    counter += root?.left?.let { node ->
        countNodes(node)
    } ?: 0

    counter += root?.right?.let { node ->
        countNodes(node)
    } ?: 0

    return counter + 1
}
```

## 코드 2

```kotlin
fun countNodes(root: TreeNode?): Int {
    when(root){
        null -> return 0
        else -> return 1 + countNodes(root.left) + countNodes(root.right)
    }
}
```

## 배운 점
1. 트리 순회는 재귀형태로 탐색한다. (복습)
2. `1 + countNodes(root.left) + countNodes(root.right)` 형태의 1 + 로 카운트 할 수 있다.

