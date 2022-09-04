#  Invert Binary Tree

> [leetcode > 226 >  Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree)
- 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. Bfs 재귀로 푸는 방법
2. iteration Queue or DeQueee 이용해 비교


## 코드 1

```kotlin
fun invertTree(root: TreeNode?): TreeNode? {
    if (root == null) {
        return root
    }

    val left = root.left
    val right = root.right
    root.left = invertTree(right)
    root.right = invertTree(left)

    return root
}
```

## 코드 2

```kotlin
fun inverTreeQueue(root: TreeNode?): TreeNode? {
    if (root == null) {
        return root
    }
    val queue = LinkedList<TreeNode>()
    queue.offer(root)
    while (queue.isNotEmpty()) {
        val current = queue.poll()
        val left = current?.left
        current?.left = current?.right
        current?.right = left

        current?.left ?.let {
            queue.offer(it)
        }
        current?.right ?.let {
            queue.offer(it)
        }
    }
    return root
}
```

## 배운 점
1. `root.left = invertTree(right)` 을 써서 참조 값이 바뀌어서 오답이 나왔다. value 대입 시에는 별도의 변수 할당해서 사용하자
2. dfs, bfs 복습

