# Find the Town Judge

> [leetcode > 997 > Find the Town Judge](https://leetcode.com/problems/find-the-town-judge/description/)

> 출처: leetcode, [https://leetcode.com]

- Level Easy [Graph]

## 해결 과정
> 1. 마을판사는 아무도 신뢰하지 않는다.
> 2. 모든사람들(마을판사를 제외한)은 마을판사를 신뢰한다.  
> 3. 위의 1,2 조건을 만족하는 사람은 딱 한명 뿐이다.  
  입력으로 trust 배열이 주어진다. trust[i]=trust[a,b]는 a가 b를 신뢰한다는 의미이다.  
  마을판사가 존재한다면 그사람의 번호를 리턴하고 존재하지 않는다면 -1을 리턴하라.

## 코드 1

```kotlin (bfs)
fun findJudge(n: Int, trust: Array<IntArray>): Int {
    if (trust.size == 0 && n == 1) {
        return 1
    }

    val count = IntArray(n + 1) { 0 }
    trust.forEach { person ->
        count[person[0]]--
        count[person[1]]++
    }

    count.forEachIndexed { index, person ->
        if (person == n - 1) {
            return index
        }
    }
    return -1
}
```

## 배운 점
1. 예외처리를 통한 빠른 리턴하는 방법

