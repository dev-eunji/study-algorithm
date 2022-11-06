# Max Area of Island

> [leetcode > 695 > Max Area of Island](https://leetcode.com/problems/max-area-of-island)
> 출처: leetcode, [https://leetcode.com]

- Level MeDium [Graph/BFS/DFS]

## 해결 과정

1. 유효한값(1)을 가지는 4방향으로 연속된 최대 면적을 구하는 문제
2. DFS, BFS


## 코드 1

```kotlin (dfs)
fun maxAreaOfIsland(grid: Array<IntArray>): Int {
    var answer = 0
    for (row in grid.indices) {
        for (col in grid[0].indices) {
            if (grid[row][col] == 1) {
                answer = maxOf(answer, dfs(grid, row, col))
            }
        }
    }
    return answer
}

private fun dfs(
    grid: Array<IntArray>, 
    row: Int, 
    col: Int
): Int {
    if (row < 0 || row >= grid.size
        || col < 0 || col >= grid[0].size
        || grid[row][col] != 1) {
        return 0
    }
    grid[row][col] = 0
    return 1 + 
    dfs(grid, row + 1, col) +
    dfs(grid, row - 1, col) +
    dfs(grid, row, col + 1) +
    dfs(grid, row, col - 1)
}
```

```kotlin (bfs)
private val DIRECTIONS =
        arrayOf(intArrayOf(-1, 0), intArrayOf(0, 1), intArrayOf(1, 0), intArrayOf(0, -1))
        
fun maxAreaOfIsland(grid: Array<IntArray>): Int {
    var answer = 0
    val visited = Array(grid.size) {
        BooleanArray(
            grid[0].size
        )
    }
    for (row in grid.indices) {
        for (col in grid[0].indices) {
            if (grid[row][col] == 1 && !visited[row][col]) {
               answer = maxOf(answer, bfs(grid, row, col, visited))
            }
        }
    }
    return answer
}

private fun bfs(
    grid: Array<IntArray>, 
    row: Int, 
    col: Int,
    visited: Array<BooleanArray>
): Int {
    var area = 0

    val queue = LinkedList<IntArray>()
    queue.offer(intArrayOf(row, col))
    visited[row][col] = true

    while (queue.isNotEmpty()) {
        val current: IntArray = queue.poll()
        area++
        for (direction in DIRECTIONS) {
            val x = current[0] + direction[0]
            val y = current[1] + direction[1]
            if (x < 0 || x >= grid.size 
                || y < 0 || y >= grid[0].size 
                || visited[x][y] || grid[x][y] != 1) {
                continue
            } else {
                queue.offer(intArrayOf(x, y))
                visited[x][y] = true
            }
        }
    }
    return area
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` java
class Solution {
    int m, n;
    int[] DIR = new int[]{0, 1, 0, -1, 0};
    public int maxAreaOfIsland(int[][] grid) {
        m = grid.length;
        n = grid[0].length;
        int ans = 0;
        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                ans = Math.max(ans, dfs(grid, r, c));
            }
        }
        return ans;
    }
    int dfs(int[][] grid, int r, int c) {
        if (r < 0 || r == m || c < 0 || c == n || grid[r][c] == 0) return 0;
        int ans = 1;
        grid[r][c] = 0; // Mark this square as visited
        for (int i = 0; i < 4; i++)
            ans += dfs(grid, r + DIR[i], c + DIR[i+1]);
        return ans;
    }
}
```

## 배운 점
1. DFS, BFS 탐색 문제 복습
2. BFS 경우 visited 체크를 하지 않고 모든 경로를 돌면 타임 아웃 발생된다.
3. 2차원 배열에 4뱡항 이동 
```
val directions: List<Pair<Int, Int>> = listOf(
    Pair(-1, 0),
    Pair(1, 0),
    Pair(0, -1),
    Pair(0, 1)
)
```

