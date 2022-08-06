# Number of Islands.

> [leetcode > 200 > Number of Islands.](https://leetcode.com/problems/number-of-islands)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Graph/BFS/DFS]

## 해결 과정

1. 주어진 2차원 배열에서 상하좌우 4방향으로 연결된 섬 개수를 확인하는 문제이다.
2. DFS


## 코드 1

```kotlin
fun numIslands(grid: Array<CharArray>): Int {
    var answer = 0
    grid.forEachIndexed { rowIndex, chars ->
        chars.forEachIndexed { colIndex, char ->
            if (char == '1') {
                dfs(
                    grid = grid,
                    row = rowIndex,
                    col = colIndex,
                    rowLength = grid.size,
                    colLength = grid[0].size
                )
                answer++
            }
        }
    }
    return answer
}

private fun dfs(
    grid: Array<CharArray>,
    row: Int,
    col: Int,
    rowLength: Int,
    colLength: Int
) {
    if (row < 0 || row >= rowLength
        || col < 0 || col >= colLength
        || grid[row][col] != '1') {
        return
    }
    grid[row][col] = 'v'
    dfs( // 위
        grid = grid,
        row = row - 1,
        col = col,
        rowLength = rowLength,
        colLength = colLength
    )
    dfs( // 아래
        grid = grid,
        row = row + 1,
        col = col,
        rowLength = rowLength,
        colLength = colLength
    )
    dfs( // 좌
        grid = grid,
        row = row,
        col = col - 1,
        rowLength = rowLength,
        colLength = colLength
    )
    dfs( // 우
        grid = grid,
        row = row,
        col = col + 1,
        rowLength = rowLength,
        colLength = colLength
    )
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```Python
def numIslands(self, grid):
    if not grid:
        return 0
        
    count = 0
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == '1':
                self.dfs(grid, i, j)
                count += 1
    return count

def dfs(self, grid, i, j):
    if i<0 or j<0 or i>=len(grid) or j>=len(grid[0]) or grid[i][j] != '1':
        return
    grid[i][j] = '#'
    self.dfs(grid, i+1, j)
    self.dfs(grid, i-1, j)
    self.dfs(grid, i, j+1)
    self.dfs(grid, i, j-1)
```

## 배운 점
1. 오랜만에 DFS, BFS 탐색 문제를 풀었다.
2. 연결된 섬을 체크하기 위해 DFS 탐색


