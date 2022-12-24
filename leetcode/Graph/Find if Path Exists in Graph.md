# Find if Path Exists in Graph

> [leetcode > 1971 > Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/description)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Graph/BFS/DFS]

## 해결 과정

1. 연결된 노드 edges에 시작점, 도착점이 주어지면 도착 가능한 그래프인지 리턴하는 문제이다.
2. DFS, BFS


## 코드 1

```kotlin (bfs)
fun validPath(n: Int, edges: Array<IntArray>, source: Int, destination: Int): Boolean {
    val graph = hashMapOf<Int, MutableList<Int>>()
    for (v in 0 until n) graph[v] = mutableListOf()

    for (edge in edges) {
        graph[edge[0]]?.add(edge[1])
        graph[edge[1]]?.add(edge[0])
    }

    val visited = BooleanArray(n)
    val queue = LinkedList<Int>()
    queue.offer(source)
    visited[source] = true

    while (queue.isNotEmpty()) {
        val currentNode = queue.poll()
        if (currentNode == destination) {
            return true
        }

        for (nextNode in graph[currentNode] ?: mutableListOf()) {
            if (!visited[nextNode]) {
                visited[nextNode] = true
                queue.offer(nextNode)
            }
        }
    }
    return false
}
```

```kotlin (dfs)
fun validPath(n: Int, edges: Array<IntArray>, source: Int, destination: Int): Boolean {
    val graph = MutableList(n) { hashSetOf<Int>() }
    val seen = hashSetOf<Int>().apply {
        add(source)
    }

    for ((u, v) in edges) {
        graph[u].add(v)
        graph[v].add(u)
    }

    return dfs(
        graph,
        seen,
        source,
        destination
    )
}

private fun dfs(
    graph: MutableList<HashSet<Int>>,
    seen: HashSet<Int>,
    current: Int,
    destination: Int
): Boolean {
    if (current == destination) {
        return true
    }

    for (next in graph[current]) {
        if (seen.add(next)) {
            if (dfs(graph, seen, next, destination)) {
                return true
            }
        }
    }

    return false
}
```


## 배운 점
1. 오랜만에 DFS, BFS 탐색 문제를 풀었다.
2. 중복된 데이터를 넣을때 `hashMapOf<Int, MutableList<Int>>` or `MutableList(n) { hashSetOf<Int>() }`

