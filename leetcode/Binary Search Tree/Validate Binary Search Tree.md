# Validate Binary Search Tree

> [leetcode > 98 > Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Binary Search Tree]

## 해결 과정

1. root 노드부터 isValidBST() 함수를 호출한다.
- 최소 한계값 및 최대 한계값은 없으므로 null을 입력한다.

2. isValidBST() 함수 내에서 입력받은 node의 값이 null이면 true를 반환한다.

3. 최소 한계값인 minLimit이 존재한다면, node의 값이 최소 한계값보다 작거나 같다면 false를 반환한다.

4. 최대 한계값인 maxLimit이 존재한다면, node의 값이 최대 한계값보다 크거나 같다면 false를 반환한다.

5. 왼쪽 자식노드가 유효한지 확인한다.
-  5-1. isValidBST() 함수를 재귀 호출하며, 인자로 왼쪽 자식노드 node.left, 최소 한계값 minLimit 그리고 최대 한계값으로 현재 노드의 값 node.val을 전달한다.
(왼쪽 자식노드는 부모 노드보다 작아야 하기 때문에 최대 한계값으로 현재 노드의 값을 전달한다.)
- 5-2. 왼쪽 자식노드가 유효하지 않다면 false를 반환한다. 

6. 오른쪽 자식노드가 유효한지 확인한다.
- isValidBST() 함수를 재귀 호출하며, 인자로 오른쪽 자식노드 node.right, 최소 한계값으로 현재 노드의 값 node.val 그리고 최대 한계값 maxLimit을 전달한다.
(오른쪽 자식노드는 부모 노드보다 커야 하기 때문에 최소 한계값으로 현재 노드의 값을 전달한다.)
- 오른쪽 자식노드가 유효하지 않다면 false를 반환한다. 
7. 최종적으로 모든 노드가 유효하다면 true를 반환한다.


## 코드 1

```kotlin (Recursive)
fun isValidBST(node: TreeNode?, minLimit: Int?, maxLimit: Int?): Boolean {

    if(node == null) return true

    val currentValue = node.`val`
    minLimit?.let { minLimit ->
        if (minLimit >= currentValue) return false
    }
    maxLimit?.let { maxLimit ->
        if (maxLimit <= currentValue) return false
    }

    return isValidBST(node.left, minLimit, currentValue) && isValidBST(node.right, currentValue, maxLimit)
}
```

```kotlin (Iterative Stack)
fun isValidBST(node: TreeNode?, minLimit: Int?, maxLimit: Int?): Boolean {

    val nodeStack: Stack<TreeNode> = Stack()
    var untilMinVal: Int? = null
    var node = root
    while (nodeStack.isNotEmpty() || node != null) {
        while (node != null) {
            nodeStack.push(node)
            node = node.left
        }
        node = nodeStack.pop()
        if (untilMinVal != null && untilMinVal >= node.`val`) {
            return false
        }
        untilMinVal = node.`val`
        node = node.right
    }
    return true
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```Java
public boolean isValidBST(TreeNode root) {
   if (root == null) return true;
   Stack<TreeNode> stack = new Stack<>();
   TreeNode pre = null;
   while (root != null || !stack.isEmpty()) {
      while (root != null) {
         stack.push(root);
         root = root.left;
      }
      root = stack.pop();
      if(pre != null && root.val <= pre.val) return false;
      pre = root;
      root = root.right;
   }
   return true;
}
```

## 배운 점
1. 노드 유효성 탐색을 배움 
2. 부모노드 하고만 비교하는 것이 아니라, 조상 노드도 고려해야 한다.
3. 특정 노드를 기준으로 왼쪽 자식노드는 부모노드 보다 값이 작아야 하며, 오른쪽 자식노드는 부모노드 보다 값이 커야 합니다.
   뿐만 아니라, 왼쪽 자식노드의 오른쪽 자식노드는 부모노드 보다는 커야하며, 조상노드 보다는 작아야 하는 조건을 만족해야 한다는 부분이 중요합니다.
   
