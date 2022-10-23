# Set Mismatch

> [leetcode > 645 > Set Mismatch](https://leetcode.com/problems/set-mismatch)
- 출처: leetcode, [https://leetcode.com]

- Level Easy [Brute Force, Hash, Sort]

## 해결 과정

1. 변경된 배열이 주어질 때 중복된 수와 누락된 수를 구하는 문제 
2. Brute Force, Hash, Sort로 구할수 있다.


## 코드 1 (Recursive, Iterative)

```kotlin (HashMap)
fun findErrorNums(nums: IntArray): IntArray {
    val hashMap = hashMapOf<Int, Int>()
    val answer = IntArray(2) // [duplicate, missing]

    nums.forEach { num ->
        hashMap[num] = hashMap.getOrDefault(num, 0) + 1
    }

    for (i in 1 .. nums.size) {
        if (hashMap.containsKey(i)) {
            if (hashMap[i] == 2) {
                answer[0] = i
            }
        } else {
            answer[1] = i
        }
    }
    return answer
}

fun findErrorNumsSort(nums: IntArray): IntArray {
    nums.sort()
    var duplicate = -1
    var missing = 1
    for (i in 1 until nums.size) {
        if (nums[i] == nums[i -1]) {
            duplicate = nums[i]
        } else if (nums[i] > nums[i - 1] + 1) {
            missing = nums[i - 1] + 1
        }
    }
    val answer = if (nums[nums.size - 1] != nums.size) {
        nums.size
    } else {
        missing
    }
    return intArrayOf(duplicate,  answer)
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```C++
public static int[] findErrorNums(int[] nums) {
    int[] res = new int[2];
    for (int i : nums) {
        if (nums[Math.abs(i) - 1] < 0) res[0] = Math.abs(i);
      	else nums[Math.abs(i) - 1] *= -1;
    }
    for (int i=0;i<nums.length;i++) {
        if (nums[i] > 0) res[1] = i+1;
    }
    return res;
}
```
