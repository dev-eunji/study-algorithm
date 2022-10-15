# Delete the Middle Node of a Linked List

> [leetcode > 2095 > Delete the Middle Node of a Linked List](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list)
> 출처: leetcode, [https://leetcode.com]

- Level Medium

## 해결 과정

1. LinkedList 중간 노드를 삭제 하는 문제
2. twoPoint를 이용하여 중간 노드를 찾아서 중간 노드 .next 노드를 이어줘서 중간 노드를 삭제 한다.


## 코드 1

```kotlin
fun deleteMiddle(head: ListNode?): ListNode? {
    if (head == null || head.next == null) {
        return null
    }
    var slow = head
    var fast = head.next.next

    while (fast != null && fast.next != null) {
        slow = slow?.next
        fast = fast.next?.next
    }
    slow?.next = slow?.next?.next

    return head
}
```

## 코드 2 (Most Votes)

```Java
public ListNode deleteMiddle(ListNode head) {
// Base Condition
    if(head == null || head.next == null) return null;
// Pointers Created
    ListNode fast = head;
    ListNode slow = head;
    ListNode prev = head;

    while(fast != null && fast.next != null){
        prev = slow;
        slow = slow.next;
        fast = fast.next.next;
    }
    prev.next = slow.next;
    return head;
}
```

## 배운 점
1. slow, fast two point로 중간 노드를 알 수 있다.

