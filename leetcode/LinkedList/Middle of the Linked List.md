# Middle of the Linked List

> [leetcode > 876 > Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list)
> 출처: leetcode, [https://leetcode.com]

- Level easy

## 해결 과정

1. index를 이용하는 방법
2. 배열을 이용하는 방법
3. slow, fast 방법 (two point)

## 코드 1

```kotlin
fun middleNode(head: ListNode?): ListNode? {
    if (head == null) return head

    var slow = head
    var fast = head
    while (slow != null && fast?.next != null) {
        slow = slow.next
        fast = fast?.next?.next
    }
    return slow
}
```

## 코드 2

```kotlin
fun middleNodeArray(head: ListNode?): ListNode? {
    if (head == null) return head

    var nodeLength = 0
    var headNode = head
    val list = Array<ListNode>(100) { ListNode(0) }
    while (headNode != null) {
        list[nodeLength++] = headNode
        headNode = headNode.next
    }
    return list[nodeLength/2]
}

fun middleNodeLength(head: ListNode?): ListNode? {
    if (head == null) return head

    var nodeLength = 0
    var headNode = head
    while (headNode != null) {
        nodeLength++
        headNode = headNode.next
    }

    val mid = nodeLength / 2 + 1
    headNode = head
    for (i in 0 until mid) {
        headNode = headNode?.next
    }
    return headNode
}
```

## 배운 점
1. slow, fast two point로 중간 지점을 알 수 있다.

