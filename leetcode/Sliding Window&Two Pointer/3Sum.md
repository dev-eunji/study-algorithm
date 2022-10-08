# 3Sum

> [leetcode > 15 > 3Sum](https://leetcode.com/problems/3sum)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Two Pointer]

## 해결 과정

1. 주어진 배열에서 3개의 합이 0이되는 모든 경우를 출력하라
2. 배열 루프를 도는 first + twoPoint left + twoPoint right의 합을 계산한다.
3. 조건에 맞으면 결과에 담고 left, right 포인터 줄여주고, 조건이 크면 right--, 작으면 left++ 범위를 좁혀간다.


## 코드 1

```kotlin
fun threeSum(nums: IntArray): List<List<Int>> {
    if (nums.size < 3) return emptyList()

    val result = hashSetOf<List<Int>>()
    nums.sort()

    for (first in 0 until nums.size - 2) {
        var left = first + 1
        var right = nums.size - 1

        while (left < right) {
            val sum = nums[first] + nums[left] + nums[right]
            if (sum == 0) {
                result.add(listOf(nums[first], nums[left], nums[right]))
            } else if (sum > 0) {
                right--
            } else if (sum < 0) {
                left++
            }
        }
    }
    return result.toList()
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
vector<vector<int> > threeSum(vector<int> &num) {
    
    vector<vector<int> > res;

    std::sort(num.begin(), num.end());

    for (int i = 0; i < num.size(); i++) {
        
        int target = -num[i];
        int front = i + 1;
        int back = num.size() - 1;

        while (front < back) {

            int sum = num[front] + num[back];
            
            // Finding answer which start from number num[i]
            if (sum < target)
                front++;

            else if (sum > target)
                back--;

            else {
                vector<int> triplet = {num[i], num[front], num[back]};
                res.push_back(triplet);
                
                // Processing duplicates of Number 2
                // Rolling the front pointer to the next different number forwards
                while (front < back && num[front] == triplet[1]) front++;

                // Processing duplicates of Number 3
                // Rolling the back pointer to the next different number backwards
                while (front < back && num[back] == triplet[2]) back--;
            }
            
        }

        // Processing duplicates of Number 1
        while (i + 1 < num.size() && num[i + 1] == num[i]) 
            i++;

    }
    
    return res;
    
}
```

## 배운 점
1. 투포인터에 타켓(결과) 값 찾는 법을 배웠다.
 - 기본적인 투포인터 검색에서 조건에 맞는 값이 추가 된 형태이다.
2. 중복 값이 제거 하기 위해 `set` 사용 
3. `set` to `list` -> `toList()` 컬렉션 변환에 익수해 지자.

