# Last Stone Weight

> [leetcode > 1046 > Last Stone Weight](https://leetcode.com/problems/last-stone-weight)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Heep]

## 해결 과정

1. PriorityQueue or 정렬을 통해 높은 값 부터 나오도록 한다.
2. 우선순위 큐가 비거나 size 가 1 이 될 때까지 두번씩 poll 하며 돌의 무게를 비교
3. 두 값이 같지 않느면 빼 나머지를 offer


## 코드 1 (Recursive, Iterative)

```kotlin (Recursive)
fun lastStoneWeight(stones: IntArray): Int {
    val priorityQueue = PriorityQueue<Int>( compareByDescending{it} )
    stones.forEach {
        priorityQueue.add(it)
    }

    while (priorityQueue.size > 1) {
        val first = priorityQueue.poll()
        val second = priorityQueue.poll()

        if (first != second) {
            priorityQueue.offer(first - second)
        }
    }

    return if (priorityQueue.isEmpty()) {
        0
    } else {
        priorityQueue.poll()
    }
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
int lastStoneWeight(vector<int>& stones) 
{
    priority_queue<int> pq(stones.begin(),stones.end());
    while(pq.size()>1)
    {
        int y=pq.top();
        pq.pop();
        int x=pq.top();
        pq.pop();
        if(x!=y) pq.push(y-x);
    }
    return pq.empty()? 0 : pq.top();
}
```

## 배운 점
1. `PriorityQueue` 복습
- 정렬 방식 IDE가 없으면 헷갈리는 외우는게 좋은것 같다.
```Kotlin
val priorityQueue = PriorityQueue<Int>( compareByDescending{it} )
val priorityQueue = PriorityQueue<Int>(compareBy { it })
val minHeap = PriorityQueue<Int>()
val maxHeap = PriorityQueue<Int>(Collections.reverseOrder())
```

