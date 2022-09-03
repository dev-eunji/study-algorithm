#  Same Tree

> [leetcode > 100 >  Same Tree](https://leetcode.com/problems/same-tree)
- 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. Bfs 재귀로 푸는 방법
2. iteration Stack 이용해 비교


## 코드 1

```kotlin
fun isSameTree(p: TreeNode?, q: TreeNode?): Boolean {   
    if (p == null && q == null) {
        return true
    }
    if (p == null || q == null) {
        return false
    }
    if (p.`val` != q.`val`) {
        return false
    }
    val left = isSameTree(p?.left, q?.left)
    val rigth = isSameTree(p?.right, q?.right)

    return left && rigth
}
```

## 코드 2

```kotlin
fun isSameTree(p: TreeNode?, q: TreeNode?): Boolean {

    if (p == null && q == null) {
        return true
    }
    if (p == null || q == null) {
        return false
    }
    val pStack = Stack<TreeNode>()
    val qStack = Stack<TreeNode>()
    pStack.push(p)
    qStack.push(q)

    while (pStack.isNotEmpty() && qStack.isNotEmpty()) {
        val pCurrent = pStack.pop()
        val qCurrent = qStack.pop()

        if (pCurrent.`val` != qCurrent.`val`) {
            return false
        }

        if (pCurrent?.left != null && qCurrent?.left != null)  {
            pStack.push(pCurrent?.left)
            qStack.push(qCurrent?.left)
        } else if (pCurrent?.left == null && qCurrent?.left == null) {
        } else {
            return false
        }

        if (pCurrent?.right != null && qCurrent?.right != null)  {
            pStack.push(pCurrent?.right)
            qStack.push(qCurrent?.right)
        } else if (pCurrent?.right == null && qCurrent?.right == null) {
        } else {
            return false
        }
    }
    return true
}
```

## 배운 점
1. `stack`를 사용하여 풀ㄷ 때 `pCurrent?.left == null && qCurrent?.left == null` 조건이 안맞아서 사이즈가 다를때 오답이 나온다.
2. 조건에 괄호를 잘못 치면 다른 답이 나온다.ㅠ
```
else if (pCurrent?.left != null && qCurrent?.left == null
          || pCurrent?.left == null && qCurrent?.left != null)
```

## 궁금 점
```
if (pCurrent?.right != null && qCurrent?.right != null)  {
    pStack.push(pCurrent?.right)
    qStack.push(qCurrent?.right)
} else if (pCurrent?.right == null && qCurrent?.right == null) {
} else {
    return false
}

vs

if (pCurrent?.left != null && qCurrent?.left != null)  {
    pStack.push(pCurrent?.left)
    qStack.push(qCurrent?.left)
} else if ((pCurrent?.left != null && qCurrent?.left == null)
          || (pCurrent?.left == null && qCurrent?.left != null)) {
    return false
}
```

