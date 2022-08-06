# N-ary Tree Preorder Traversal

> [leetcode > 589 > N-ary Tree Preorder Traversal.md](https://leetcode.com/problems/n-ary-tree-preorder-traversal)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Tree]

## 해결 과정

1. 깊이 우선 탐색으로 Tree 순회 탐색
2. Iterator 방식으로 stack을 이용하기 때문에 node의 children 탐색


## 코드 1

```kotlin (dfs)
private val answer = mutableListOf<Int>()
  fun preorder(root: Node?): List<Int> {
      if (root == null) {
          return answer
      }

      dfs(root)
      return answer
  }

  private fun dfs(root: Node?) {
      if (root == null) {
          return
      }

      answer.add(root.`val`)
      root.children.forEach { children ->
          dfs(children)
      }
  }
```

```kotlin (Iterator)
fun preorderIterative(root: Node?): List<Int> {
    val preorder = LinkedList<Int>()
    val stack = Stack<Node>()
    stack.push(root)
    if (root == null) {
        return preorder
    }

    while (!stack.isEmpty()) {
        var currentNode = stack.pop()
        preorder.add(currentNode.`val`)

        for (i in currentNode.children.lastIndex downTo 0) {
            stack.push(currentNode.children[i])
        }

//            currentNode.children.reversed().forEach {
//                if (it != null) {
//                    stack.push(it)
//                }
//            }
    }
    return preorder
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` java
public List<Integer> list = new ArrayList<>();
public List<Integer> preorder(Node root) {
    if (root == null)
        return list;

    list.add(root.val);
    for(Node node: root.children)
        preorder(node);

    return list;
}
```

## 배운 점
1. dfs 복습
2. stack을 활용한 트리 탐색

