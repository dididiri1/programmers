
# CHAPTER 6 완전탐색

## 모의고사 - Level 1

### 문제 설명
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다.   
수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...  
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...  
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이   
누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한 조건
- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.


### 입출력 예

| answers     | return  |
|:------------|:--------|
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |


### 입출력 예 설명
### 입출력 예 #1

- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.
따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

### 입출력 예 #2
- 모든 사람이 2문제씩을 맞췄습니다.

### Solution.java
``` java
import java.util.*;
import java.util.stream.IntStream;

class Solution {
    
    private static final int[][] RULES = {
            {1,2,3,4,5},
            {2,1,2,3,2,4,2,4},
            {3,3,1,1,2,2,4,4,5,5}
    };
    
    public int[] solution(int[] answers) {
        int max = Integer.MIN_VALUE;
        int[] corrects = new int[3];

        for (int person =0; person < 3; person++) {
            int cnt = 0;
            for (int problem =0; problem<answers.length; problem++) {
                if(answers[problem] == RULES[person][problem]) {
                    cnt++;
                }
            }
            corrects[person] = cnt;
            max = Math.max(max, cnt);
        }

        int maxCount = max;
        int[] answer = IntStream.range(0, 3)
                .filter(i -> corrects[i] == maxCount)
                .map(i -> i + 1)
                .toArray();

        return answer;
    }
}
``` 

## 카펫 - Level 2 

### 문제 설명
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고   
테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![](https://github.com/dididiri1/java-algorithm/blob/main/programmers/images/06_01.png?raw=true)


Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만,
전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때   
카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

### 입출력 예
|  brown | yellow |     return |
|---:|-------:|-----------:|
| 10 |      2 |     [4, 3] |
| 8 |      1 |     [3, 3] |
| 24 |     24 |     [8, 6] |


### 이 문제를 풀기 위해서는 다음 조건에 대해 이해해야합니다.
- 가로와 세로의 크기가 3이상이어야 한다.

가로와 세로의 크기가 3보다 작다면 yellow가 있을 자리가 없습니다.
![](https://github.com/dididiri1/java-algorithm/blob/main/programmers/images/06_02.png?raw=true)
- yellow의 넓이 구하기
  brown이 10, yellow가 2일 때를 예로들면,


![](https://github.com/dididiri1/java-algorithm/blob/main/programmers/images/06_03.png?raw=true)

yellow의 넓이를 구하는 공식은 yellow의 가로 길이는 직사각형의 가로길이에서 2를 뺀 값과 같고, 세로의 길이 또한 직사각형의 길에서 2를 뺀 값과 같습니다.

**즉, yellow의 넓이를 구하는 공식은 (가로 - 2) * (세로 - 2)가 됩니다.**


### Solution.java
``` java
class Solution {

    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
      
        int carpet = brown + yellow;  12
        
        // yellow가 존재하기 위해서는 가로와 세로의 길이가 3이상이여야 한다.
        for (int i = 3; i <= carpet; i++) { // i= 4이면
            // 세로
            int col = i; // col= 4
            // 가로
            int row = carpet / col; // 12/4 = 3 
            
            // 가로의 갯수가 3 이하라면 다음 인덱스
            if (row < 3) {
                continue;
            }
            
            // "가로는 세로의 길이보다 크거나 같다" 조건
            if (row >= col) {
                if ((row - 2) * (col - 2) == yellow) {
                    answer[0] = row;
                    answer[1] = col;
                    return answer;
                }
            }
        }
        
        return answer;
    }
}
``` 


## 소수 찾기 - Level 2

### 문제 설명
한자리 숫자가 적힌 종이 조각이 흩어져있습니다.    
흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때,   
종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

### 제한 조건
- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.


### 입출력 예
| numbers    | return |
|:-----------|:-------|
| "17"       | 3      |
| "011"      | 2      |

### 입출력 예 설명
#### 예제 #1  
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

#### 예제 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.
- 11과 011은 같은 숫자로 취급합니다.

### Solution.java
``` java
import java.util.HashSet;
import java.util.Iterator;

class Solution {
    private HashSet<Integer> set = new HashSet<>();

    private boolean isPrime(Integer num) {
        // 1. 0과 1은 소수가 아니다.
        if (num == 0 || num == 1) {
            return false;
        }
            

        // 2. 에라토스테네의 체의 limit를 계산한다.
        // 제곱근 까지만 약수 검증, 시간복잡도 O(N^(1/2))
        int end = (int) Math.sqrt(num);

        // 3. 에라토스테네스의 체에 따라 limit까지만 배수 여부를 확인한다.
        // i <= end 주의! 제곱근을 계산하는 부분에서 off-by-one error가 존재함. 
        // 즉, i <= end를 사용해야 한다. 정확히 제곱근까지 나누어떨어지는지 검사할 수 있다.
        for (int i = 2; i <= end; i++) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }

    public void DFS(String comb, String others) {
        // 1. 현재 조합을 set에 추가한다.
        if(!comb.equals("")) {
            set.add(Integer.valueOf(comb));
        }

        //2. 남은 숫자 중 한개를 더 해 새로운 조합을 만든다.
        for (int i = 0; i < others.length(); i++) {
            DFS(comb + others.charAt(i), others.substring(0, i) + others.substring(i+1));
        }
    }

    public int solution(String numbers) {
        int answer = 0;

        // 1. 모든 숫자의 조합을 만든다.
        DFS("", numbers);

        // 2. 소수의 개수만 센다
        Iterator<Integer> it = set.iterator();
        while (it.hasNext()) {
            int num = it.next();
            if (isPrime(num)) {
                answer ++;
            }
        }

        // 3. 소수의 개수를 반환한다.
        return answer;
        // return (int) set.stream().filter(this::isPrime).count();
    }
}
``` 