# Reverse Linked List.

> [leetcode > 206 > TwoIsomorphic Stringsm](https://leetcode.com/problems/reverse-linked-list)
> 출처: leetcode, [https://leetcode.com]

- Level easy

## 해결 과정

1. head node를 순회하면서 reverseList를 헤더노드의 next에 계속 이어 붙힌다.

## 코드 1

```kotlin
fun reverseList(head: ListNode?): ListNode? {
    if (head == null) return null

    var headNode = head
    var reverseList: ListNode? = null
    while (headNode != null) {
        val next = headNode.next
        headNode.next = reverseList
        reverseList = headNode
        headNode = next
    }

    return reverseList
}
```

## 코드 2: 다른 사람 코드

```java
private ListNode reverseListInt(ListNode head, ListNode newHead) {
    if (head == null)
        return newHead;
    ListNode next = head.next;
    head.next = newHead;
    return reverseListInt(next, head);
}
```

## 배운 점
1. head.next = newHead 를 대입하여 리버스 한다.
2. 어렵다ㅠ

