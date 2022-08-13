# Spiral Matrix II

> [leetcode > 59 > Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [matrix]

## 해결 과정

1. 달팽이 배열 형태로 회전하면서 값을 채운다.


## 코드 1

```kotlin
fun generateMatrix(n: Int): Array<IntArray> {
    val matrix = Array(n) {
        IntArray(n)
    }
    if (n <= 0) return matrix

    var row = 0
    var col = 0
    var rowEnd = matrix.size - 1
    var colEnd = matrix[0].size - 1
    var number = 1

    while (col <= colEnd && row <= rowEnd) {
        for (i in col .. colEnd) { // top
            matrix[row][i] = number++
        }
        row++
        for (i in row .. rowEnd) { // right
            matrix[i][colEnd] = number++
        }
        colEnd--
        for (i in colEnd downTo col) { // bottom
            matrix[rowEnd][i] = number++
        }
        rowEnd--
        for (i in rowEnd downTo row) {// left
            matrix[i][col] = number++
        }
        col++
    }
    return matrix
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
public int[][] generateMatrix(int n) {
    // Declaration
    int[][] matrix = new int[n][n];

    // Edge Case
    if (n == 0) {
        return matrix;
    }

    // Normal Case
    int rowStart = 0;
    int rowEnd = n-1;
    int colStart = 0;
    int colEnd = n-1;
    int num = 1; //change

    while (rowStart <= rowEnd && colStart <= colEnd) {
        for (int i = colStart; i <= colEnd; i ++) {
            matrix[rowStart][i] = num ++; //change
        }
        rowStart ++;

        for (int i = rowStart; i <= rowEnd; i ++) {
            matrix[i][colEnd] = num ++; //change
        }
        colEnd --;

        for (int i = colEnd; i >= colStart; i --) {
            if (rowStart <= rowEnd)
                matrix[rowEnd][i] = num ++; //change
        }
        rowEnd --;

        for (int i = rowEnd; i >= rowStart; i --) {
            if (colStart <= colEnd)
                matrix[i][colStart] = num ++; //change
        }
        colStart ++;
    }

    return matrix;
}

```

## 배운 점
1. 코딩 테스트 및 라이브 코테에서 많이 출제 되는 문제이다.
2. 2차원 배열을 회전하면서 완전 탐색하는 방법을 배웠다.
3. 인덱스 증가 지키는 부분이 헷갈린다.


