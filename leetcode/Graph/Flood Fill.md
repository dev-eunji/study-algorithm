# Flood Fill.

> [leetcode > 121 > Flood Fill.](https://leetcode.com/problems/flood-fill/submissions)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Graph/BFS/DFS]

## 해결 과정

1. 주어진 2차원 배열에서 상하좌우 4방향으로 시작위치의 색과 같은 색이면 새로운 색으로 칠하면 되는 문제이다.
2. DFS, BFS


## 코드 1

```kotlin
fun floodFill(image: Array<IntArray>, sr: Int, sc: Int, color: Int): Array<IntArray> {

    if (image[sr][sc] == color) { // same color -> no need to replace
        return image
    }
    dfsFill(image, sr, sc, image[sr][sc], color)
    return image
}

private fun dfsFill(
    image: Array<IntArray>,
    sr: Int,
    sc: Int,
    oldColor: Int,
    newColor: Int
) {
    if (sr < 0 || sr >= image.size
        || sc < 0 || sc >= image[0].size
        || image[sr][sc] != oldColor) {
        return
    }

    var mutableImage = image
    mutableImage[sr][sc] = newColor // also mean we marked it as visited!

    dfsFill(image, sr - 1, sc, oldColor, newColor)
    dfsFill(image, sr + 1, sc, oldColor, newColor)
    dfsFill(image, sr, sc - 1, oldColor, newColor)
    dfsFill(image, sr, sc + 1, oldColor, newColor)
}

private fun bfsFill(
    image: Array<IntArray>,
    sr: Int,
    sc: Int,
    newColor: Int
): Array<IntArray> {
    val oldColor = image[sr][sc]
    if (oldColor == newColor) {
        return image
    }

    val directions: List<Pair<Int, Int>> = listOf(
        Pair(-1, 0),
        Pair(1, 0),
        Pair(0, -1),
        Pair(0, 1)
    )

    var mutableImage = image
    val queue = LinkedList<Pair<Int, Int>>()
    queue.offer(Pair(sr, sc))
    while (queue.isNotEmpty()) {
        val current = queue.poll()
        mutableImage[current.first][current.second] = newColor

        directions.forEach { directions ->
            val row = current.first + directions.first
            val col = current.second + directions.second
            if (row < 0 || row == image.size
                || col < 0 || col == image[0].size
                || image[row][col] != oldColor) {
                return@forEach
            }

            queue.add(Pair(row, col))
        }
    }
    return mutableImage
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
class Solution {
  int[] DIRS = {0, 1, 0, -1, 0};
  int m, n;
  public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
      if (image[sr][sc] == newColor) return image; // same color -> no need to replace
      m = image.length; n = image[0].length;
      dfs(image, sr, sc, image[sr][sc], newColor);
      return image;
  }

  void dfs(int[][] image, int r, int c, int oldColor, int newColor) {
      if (r < 0 || r == m || c < 0 || c == n || image[r][c] != oldColor) return;
      image[r][c] = newColor; // also mean we marked it as visited!
      for (int i = 0; i < 4; i++)
          dfs(image, r + DIRS[i], c + DIRS[i+1], oldColor, newColor);
  }
}

class Solution {
    int[] DIRS = {0, 1, 0, -1, 0};
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        if (image[sr][sc] == newColor) return image; // same color -> no need to replace

        int m = image.length, n = image[0].length;
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{sr, sc});
        int oldColor = image[sr][sc];
        image[sr][sc] = newColor;
        while (!q.isEmpty()) {
            int[] top = q.poll();
            for (int i = 0; i < 4; i++) {
                int nr = top[0] + DIRS[i];
                int nc = top[1] + DIRS[i + 1];
                if (nr < 0 || nr == m || nc < 0 || nc == n || image[nr][nc] != oldColor) continue;
                image[nr][nc] = newColor; // also mean we marked it as visited!
                q.offer(new int[]{nr, nc});
            }
        }
        return image;
    }
}
```

## 배운 점
1. 오랜만에 DFS, BFS 탐색 문제를 풀었다.
2. 플러드 필 알고리즘: https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9F%AC%EB%93%9C_%ED%95%84
3. 2차원 배열에 4뱡항 이동 
```
val directions: List<Pair<Int, Int>> = listOf(
    Pair(-1, 0),
    Pair(1, 0),
    Pair(0, -1),
    Pair(0, 1)
)
```
4. forEach continue는 `return@forEach` 

