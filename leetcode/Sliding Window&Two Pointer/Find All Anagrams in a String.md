# Find All Anagrams in a String

> [leetcode > 438 > Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Sliding Window/Two Pointer]

## 해결 과정

1. a - z를 담을 수 있는 배열 array를 생성 후, 문자열 p의 문자를 array의 해당 값에 +1을 한다. 
2. 그 후 문자열 s의 substring을 (0, p.length) 만큼의 원소를 array의 해당 값에 -1 한다. 즉, array의 모든 값이 0이라면 이는 anagram이다


## 코드 1

```kotlin
fun findAnagrams(s: String, p: String): List<Int> {
    val answer = mutableListOf<Int>()
    val length = 'z' - 'a' + 1
    val array = IntArray(length)

    if (p.length > s.length) return emptyList()

    p.forEach { // p의 문자가 있는 array[index]를 1로 만든다.(array[it - 'a']++
        array[it - 'a']++
    }
    var start = 0
    s.forEachIndexed { index, char ->
        array[char - 'a']--
        if (index - start >= p.length) { // window 크기가 3이 되면
            array[s[start++] - 'a']++
        }
        if (isAnagram(array)) {
            answer.add(start)
        }
    }

    return answer.toList()
}

private fun isAnagram(array: IntArray): Boolean {
    array.forEach {
        if (it != 0) return false
    }
    return true
}
```

## 코드 2

```kotlin
fun findAnagrams_sliding(s: String, p: String): List<Int> {
    val answer = mutableListOf<Int>()
    val length = 'z' - 'a' + 1
    val array = IntArray(length)

    if (p.length > s.length) return emptyList()

    p.forEach { // p의 문자가 있는 array[index]를 1로 만든다.(array[it - 'a']++
        array[it - 'a']++
    }
    var start = 0
    var end = 0
    var count = p.length
    while (end < s.length) {
        if (array[s[end++] - 'a']-- >= 1) {
            count--
        }
        if (count == 0) {
            answer.add(start)
        }
        if (end - start == p.length && array[s[start++] - 'a']++ >= 0) {
            count++
        }
    }
    return answer.toList()
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
vector<int> findAnagrams(string s, string p) {
    int s_len = s.length();
    int p_len = p.length();

    if(s.size() < p.size()) return {};

    vector<int> freq_p(26,0);
    vector<int> window(26,0);

    //first window
    for(int i=0;i<p_len;i++){
        freq_p[p[i]-'a']++;
        window[s[i]-'a']++;
    }

    vector<int> ans;
    if(freq_p == window) ans.push_back(0);

    for(int i=p_len;i<s_len;i++){
        window[s[i-p_len] - 'a']--;
        window[s[i] - 'a']++;

        if(freq_p == window) ans.push_back(i-p_len+1);
    }
    return ans;
}
```

## 배운 점
1. 슬라이딩 윈도우를 배웠다(복습).
2. 순서 없는 아나그램을 검사 할때는 배열을 생성해 해당 문자(char)가 있는지 검사 `array[it - 'a']++` window 구간에서 해당 문자를 빼서 0이면 아나그램이다.
3. `hashMap`으로 검사 할 수도 있다.



