# 정렬

## 문자열 내 마음대로 정렬하기 - Level 1

### 문제 설명
문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때,   
각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다.   
예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.

### 제한 조건
- strings는 길이 1 이상, 50이하인 배열입니다.
- strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
- strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
- 모든 strings의 원소의 길이는 n보다 큽니다.
- 인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

### 입출력 예

| strings                   | n | return                   |
|:--------------------------|:--|:-------------------------|
| ["sun", "bed", "car"]     | 1 | ["car", "bed", "sun"]    |
| ["abce", "abcd", "cdx"]   | 2 | ["abcd", "abce", "cdx"]  |


### 입출력 예 설명
#### 입출력 예 1
"sun", "bed", "car"의 1번째 인덱스 값은 각각 "u", "e", "a" 입니다.   
이를 기준으로 strings를 정렬하면 ["car", "bed", "sun"] 입니다.


#### 입출력 예 2
"abce"와 "abcd", "cdx"의 2번째 인덱스 값은 "c", "c", "x"입니다.  
따라서 정렬 후에는 "cdx"가 가장 뒤에 위치합니다. "abce"와 "abcd"는   
사전순으로 정렬하면 "abcd"가 우선하므로, 답은 ["abcd", "abce", "cdx"] 입니다.

### Solution.java
``` java
import java.util.Arrays;

class Solution {
    public String[] solution(String[] strings, int n) {
        String[] answer = {};
        
        Arrays.sort(strings, (s1, s2)-> {
            if (s1.charAt(n) != s2.charAt(n)) {
                return s1.charAt(n) - s2.charAt(n);
            }

            return s1.compareTo(s2);
        });
        
        answer= strings;
        
        return answer;
    }
}
```

## 가장 큰 수 - Level 1

### 문제 설명
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.  

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.  

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록   
solution 함수를 작성해주세요.




### 제한 조건
- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

### 입출력 예

| numbers           | return    |
|:------------------|:----------|
| [6, 10, 2]        | "6210"    |
| [3, 30, 34, 5, 9] | "9534330" |


### Solution.java
``` java
import java.util.Arrays;
import java.util.stream.Collectors;

class Solution {
    public String solution(int[] numbers) {
        String answer = Arrays.stream(numbers)
                .mapToObj(String::valueOf)
                .sorted((s1, s2) ->{
                    int original = Integer.parseInt(s1+s2);
                    int reversed = Integer.parseInt(s2+s1);

                    return reversed-original;
                })
                .collect(Collectors.joining(""))
                .replaceAll("^0+", "0");
        return answer;
    }
}
``` 

