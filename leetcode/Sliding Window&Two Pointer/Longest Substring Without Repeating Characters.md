# 3Sum

> [leetcode > 3 > Longest Substring Without Repeating Characters]([https://leetcode.com/problems/3sum](https://leetcode.com/problems/longest-substring-without-repeating-characters)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Sliding Window]

## 해결 과정

1. 문자열에서 중복되지 않은 문자열을 가진 최대로 연속된 문자열의 길이를 반환하는 문제
2. 현재 문자가 시작점 이후에 사용됐을 경우 중복 체크하고, 없다면 포인터만 옮긴다.
3. 최대 중복 길이 계산


## 코드 1

```kotlin
fun lengthOfLongestSubstring(s: String): Int {
    val hashMap = HashMap<Char, Int>()

    var maxLength = 0
    var start = 0
    s.forEachIndexed { index, char ->
        if (hashMap.containsKey(char)) {
            start = start.coerceAtLeast(hashMap[char]?.plus(1) ?: 1) // 중복된 문자의 마지막위치 +1로 start 인덱스 이동
        }
        hashMap[char] = index // 해당 문자의 마지막 위치 기록
        maxLength = maxLength.coerceAtLeast(index - start + 1) // 유효한 최대 길이 계산. 진행중인 index에서 start 까지의 거리
    }
    return maxLength
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
public int lengthOfLongestSubstring(String s) {        
    int maxLen = 0;
    Set<Character> window = new HashSet<>(); 
    
    int left = 0, right = 0;
    while(right < s.length()) { 
        while(window.contains(s.charAt(right)))
            window.remove(s.charAt(left++));  
        window.add(s.charAt(right++)); 
        maxLen = Math.max(maxLen, right - left);
    }
     
    return maxLen;
}
```

## 배운 점
1. 중복 계산을 하기 위해 `HashMap`, `Set` 사용.
2. 슬라이딩 윈도우 (고정된 범위를 이동 시키면서 해답을 찾는 방식) 
- 최대 중복문자 길이 계산 : 중복된 문자의 index로 이동하고, 현재 인텍스 - 중복된 문자 index + 1

