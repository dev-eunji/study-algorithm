# Keys and Rooms

> [leetcode > 841 > Keys and Rooms](https://leetcode.com/problems/keys-and-rooms/description)

> 출처: leetcode, [https://leetcode.com]

- Level Medium [Graph/BFS/DFS]

## 해결 과정

1. 0 ~ n-1 방이 있고, 0번 방을 제외한 모든 방이 잠겨 있을때 rooms에 해당 방의 키를 이용하여 모든 방을 방문하는지 확인하는 문제
2. DFS, BFS


## 코드 1

```kotlin (dfs)
fun canVisitAllRooms(rooms: List<List<Int>>): Boolean {
    val visited = hashSetOf<Int>()
    dfs(0, rooms, visited)
    return visited.size == rooms.size
}

private fun dfs(
    room: Int,
    rooms: List<List<Int>>,
    visited: HashSet<Int>
) {
    visited.add(room)
    for (key in rooms[room]) {
        if (!visited.contains(key)) {
            dfs(key, rooms, visited)
        }
    }
}
```

```kotlin (bfs queue)
fun canVisitAllRooms(rooms: List<List<Int>>): Boolean {
    val visited = HashSet<Int>()
    val queue = LinkedList<Int>()
    queue.offer(0)

    while (queue.isNotEmpty()) {
        val current = queue.poll()
        visited.add(current)

        for (key in rooms[current]) {
            if (!visited.contains(key)) {
                queue.push(key)
            }
        }
    }

    return visited.size == rooms.size
}
```

```kotlin (bfs stack)
fun canVisitAllRooms(rooms: List<List<Int>>): Boolean {
    val visited = HashSet<Int>()
    val stack = Stack<Int>()
    stack.push(0)

    while (stack.isNotEmpty()) {
        val current = stack.pop()
        visited.add(current)

        for (key in rooms[current]) {
            if (!visited.contains(key)) {
                stack.push(key)
            }
        }
    }

    return visited.size == rooms.size
}
```

