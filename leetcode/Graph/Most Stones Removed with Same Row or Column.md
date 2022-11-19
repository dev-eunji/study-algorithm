# Most Stones Removed with Same Row or Column

> [leetcode > 947 > Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column)
> 출처: leetcode, [https://leetcode.com]

- Level MeDium [BFS/DFS]

## 해결 과정

1. 열과, 행이 같은 돌을 지우고 남은 돌의 개수 리턴하는 문제
2. DFS, union find


## 코드 1

```kotlin (dfs)
fun removeStones(stones: Array<IntArray>): Int {
    val visited = hashSetOf<IntArray>()

    var numOfIslands = 0
    stones.forEach { stone ->
        if (!visited.contains(stone)) {
            dfs(stone, stones, visited)
            numOfIslands++ 
        }
    }
    return stones.size - numOfIslands
}

private fun dfs(
    stone : IntArray,
    stones: Array<IntArray>,
    visited: HashSet<IntArray>
) {
    visited.add(stone)
    stones.forEach { nextStone ->
        if (!visited.contains(nextStone) && (stone[0] == nextStone[0] || stone[1] == nextStone[1])) {
            dfs(nextStone, stones, visited)
        }
    }
}
```

```kotlin (union find)
var count = 0
fun removeStones(stones: Array<IntArray>): Int {
    val parent = hashMapOf<String, String>()
    count = stones.size

    stones.forEach { stone ->
        val key = "${stone[0]} ${stone[1]}"
        parent[key] = key
    }

    stones.forEach { stone ->
       val first = "${stone[0]} ${stone[1]}"
        stones.forEach { stoneNext ->
            if (stone[0] == stoneNext[0] || stone[1] == stoneNext[1]) {
                val second = "${stoneNext[0]} ${stoneNext[1]}"
                union(parent, first, second)
            }
        }
    }
    return stones.size - count
}

private fun union(
    parent: HashMap<String, String>, 
    first: String, 
    second: String
) {
    val x = find(parent, first)
    val y = find(parent, second)
    if (x == y) {
        return
    }

    parent[x] = y
    count--
}

private fun find(parent: HashMap<String, String>, findS: String): String {
    if (parent.getOrDefault(findS, "") != findS) {
        parent[findS] = find(parent, parent.getOrDefault(findS, ""))
    }
    return parent.getOrDefault(findS, "")
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` java
Map<Integer, Integer> f = new HashMap<>();
int islands = 0;

public int removeStones(int[][] stones) {
    for (int i = 0; i < stones.length; ++i)
        union(stones[i][0], ~stones[i][1]);
    return stones.length - islands;
}

public int find(int x) {
    if (f.putIfAbsent(x, x) == null)
        islands++;
    if (x != f.get(x))
        f.put(x, find(f.get(x)));
    return f.get(x);
}

public void union(int x, int y) {
    x = find(x);
    y = find(y);
    if (x != y) {
        f.put(x, y);
        islands--;
    }
}
```

## 배운 점
1. union find (교집합)에 대해 배웠다.


