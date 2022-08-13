# Spiral Matrix

> [leetcode > 54 > Spiral Matrix](https://leetcode.com/problems/spiral-matrix)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [matrix]

## 해결 과정

1. 달팽이 배열 형태로 회전하면서 값을 채운다.


## 코드 1

```kotlin
fun spiralOrder(matrix: Array<IntArray>): List<Int> {
    val answer = mutableListOf<Int>()

    if (matrix.isEmpty()) return answer
    var rowEnd = matrix.size
    var colEnd = matrix[0].size
    val visit = Array(rowEnd) {
        BooleanArray(
            colEnd
        )
    }

    val dx = intArrayOf(0, 1, 0, -1)
    val dy = intArrayOf(1, 0, -1, 0)
    var x = 0
    var y = 0
    var di = 0
    for (i in 0 until rowEnd * colEnd) {
        answer.add(matrix[x][y])
        visit[x][y] = true
        val nx = x + dx[di]
        val ny = y + dy[di]

        if (0 <= nx && nx < rowEnd && 0 <= ny && ny < colEnd && !visit[nx][ny]) {
            x = nx
            y = ny
        } else {
            di = (di + 1) % 4
            x += dx[di]
            y += dy[di]
        }
    }
    return answer
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```java
public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> res = new ArrayList<Integer>();
    if(matrix.length == 0 || matrix[0].length == 0) return res;

    int top = 0;
    int bottom = matrix.length-1;
    int left = 0;
    int right = matrix[0].length-1;

    while(true){
        for(int i = left; i <= right; i++) res.add(matrix[top][i]);
        top++;
        if(left > right || top > bottom) break;

        for(int i = top; i <= bottom; i++) res.add(matrix[i][right]);
        right--;
        if(left > right || top > bottom) break;

        for(int i = right; i >= left; i--) res.add(matrix[bottom][i]);
        bottom--;
        if(left > right || top > bottom) break;

        for(int i = bottom; i >= top; i--) res.add(matrix[i][left]);
        left++;
        if(left > right || top > bottom) break;
    }

    return res;
}

```

## 배운 점
1. 회전하는 방향을 정하고 방문하지 않은 곳을 이동하면서 탐색
- `if (0 <= nx && nx < rowEnd && 0 <= ny && ny < colEnd && !visit[nx][ny])`
- 방향 변경 `di = (di + 1) % 4`
2. `val dx = intArrayOf(0, 1, 0, -1)` `val dy = intArrayOf(1, 0, -1, 0)` 형태로 2차원 배열 탐색(미로 등)에서 많이 쓰인다.



