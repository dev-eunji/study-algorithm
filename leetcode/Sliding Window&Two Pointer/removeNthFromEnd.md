# removeNthFromEnd

> [leetcode > 19 > removeNthFromEnd](https://leetcode.com/problems/remove-nth-node-from-end-of-list)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Two Pointer]

## 해결 과정

1. linked list 에서 End에서 n번째 노드 삭제 후 linked list 리턴하는 문제
2. slow, fast 만들고, n만큼 fast 이동
3. `fast == null` 경우 체크 (Input: head = [1], n = 1Output: [])
4. `fast.next` null 이 아닐때 까지 이동 (slow, fast)
5. slow는 End에서 n번째 노드 앞에 있는데 next = next.next 대입으로 해당 노드 삭제


## 코드 1

```kotlin
fun removeNthFromEnd(head: ListNode?, n: Int): ListNode? {
    if (head == null) {
        return null
    }

    var slow = head
    var fast = head

    for (index in 0 until n) {
        fast = fast?.next
    }

    if (fast == null) {
        return head?.next
    }

    while (fast?.next != null) {
        slow = slow?.next
        fast = fast?.next
    }
    slow?.next = slow?.next?.next

    return head
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` Java
public ListNode removeNthFromEnd(ListNode head, int n) {
    
    ListNode start = new ListNode(0);
    ListNode slow = start, fast = start;
    slow.next = head;
    
    //Move fast in front so that the gap between slow and fast becomes n
    for(int i=1; i<=n+1; i++)   {
        fast = fast.next;
    }
    //Move fast to the end, maintaining the gap
    while(fast != null) {
        slow = slow.next;
        fast = fast.next;
    }
    //Skip the desired node
    slow.next = slow.next.next;
    return start.next;
}
```

## 배운 점
1. 투포인터를 이용하여 특정 노드로 이동하는 방법을 배움


