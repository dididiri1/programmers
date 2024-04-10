# L2

## 1. JadenCase 문자열 만들기

### 문제 설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다.  
단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)  
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

### 제한 조건
- s는 길이 1 이상 200 이하인 문자열입니다.
- s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
    - 숫자는 단어의 첫 문자로만 나옵니다.
    - 숫자로만 이루어진 단어는 없습니다.
    - 공백문자가 연속해서 나올 수 있습니다.


### 입출력 예
첫 줄에 해당 문자의 개수를 출력한다.

|            s            |         return          |
|:-----------------------:|:-----------------------:|
| "3people unFollowed me" | "3people Unfollowed Me" |
|   "for the last week"   |  "For The Last Week"    |


### Solution.java
``` java


``` 

## 2. 최솟값 만들기

### 문제 설명

길이가 같은 배열 A, B 두개가 있습니다. 각 배열은 자연수로 이루어져 있습니다.  
배열 A, B에서 각각 한 개의 숫자를 뽑아 두 수를 곱합니다. 이러한 과정을 배열의 길이만큼 반복하며,
두 수를 곱한 값을 누적하여 더합니다.   
이때 최종적으로 누적된 값이 최소가 되도록 만드는 것이 목표입니다.     
(단, 각 배열에서 k번째 숫자를 뽑았다면 다음에 k번째 숫자는 다시 뽑을 수 없습니다.)

예를 들어 A = [1, 4, 2] , B = [5, 4, 4] 라면

- A에서 첫번째 숫자인 1, B에서 첫번째 숫자인 5를 뽑아 곱하여 더합니다. (누적된 값 : 0 + 5(1x5) = 5)
- A에서 두번째 숫자인 4, B에서 세번째 숫자인 4를 뽑아 곱하여 더합니다. (누적된 값 : 5 + 16(4x4) = 21)
- A에서 세번째 숫자인 2, B에서 두번째 숫자인 4를 뽑아 곱하여 더합니다. (누적된 값 : 21 + 8(2x4) = 29)
- 즉, 이 경우가 최소가 되므로 29를 return 합니다.

배열 A, B가 주어질 때 최종적으로 누적된 최솟값을 return 하는 solution 함수를 완성해 주세요.

### 제한사항
- 배열 A, B의 크기 : 1,000 이하의 자연수
- 배열 A, B의 원소의 크기 : 1,000 이하의 자연수


### 입출력 예
첫 줄에 해당 문자의 개수를 출력한다.

|         A |         B | answer |
|----------:|----------:|-------:|
| [1, 4, 2] | [5, 4, 4] |     29 |
|    [1, 2] |    [3, 4] |     10 |


### Solution.java
``` java
import java.util.*;

class Solution
{
    public int solution(int []A, int []B)
    {
        int answer = 0;
        
        Arrays.sort(A);
        Arrays.sort(B);
        //Integer[] arr = Arrays.stream(B).boxed().toArray(Integer[]::new);
        //Arrays.sort(arr, Collections.reverseOrder());
        
        for (int i=0; i<A.length; i++) {
            answer += A[i] * B[B.length-i-1];
        }
    
        return answer;
    }
}
``` 

## 3. 올바른 괄호

### 문제 설명

괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어
- "()()" 또는 "(())()" 는 올바른 괄호입니다.
- ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.  
  '(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면   
  false를 return 하는 solution 함수를 완성해 주세요.

### 제한사항
- 문자열 s의 길이 : 100,000 이하의 자연수
- 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.


### 입출력 예
첫 줄에 해당 문자의 개수를 출력한다.

|          A |     B |
|-----------:|------:|
|     "()()" |  true |
|   "(())()" |  true |
|     ")()(" | false |
|     "(()(" | false |


### Solution.java
``` java
import java.util.*;

class Solution
{
    public int solution(int []A, int []B)
    {
        int answer = 0;
        
        Arrays.sort(A);
        Arrays.sort(B);
        //Integer[] arr = Arrays.stream(B).boxed().toArray(Integer[]::new);
        //Arrays.sort(arr, Collections.reverseOrder());
        
        for (int i=0; i<A.length; i++) {
            answer += A[i] * B[B.length-i-1];
        }
    
        return answer;
    }
}
```
## 4. 숫자의 표현

### 문제 설명

Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다.   
예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.
- 1 + 2 + 3 + 4 + 5 = 15
- 4 + 5 + 6 = 15
- 7 + 8 = 15
- 15 = 15
  자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.
### 제한사항
- n은 10,000 이하의 자연수 입니다.

### 입출력 예
첫 줄에 해당 문자의 개수를 출력한다.

|  n | result |
|---:|-------:|
| 15 |      4 |



### Solution.java
``` java
class Solution {
    public int solution(int n) {
        int answer = 1;

        for(int i=1; i<=n; i++) {    
            int num = i;
            for(int j=i+1; j<=n; j++) {
                num += j;
                if (num == n) {
                    answer ++;
                    break;
                } else if(num > n) {
                    break;
                } 
            }
        }
        
        return answer;
    }
}
``` 

## Integer.bitCount()
int 값의 2진수 이진 표현에서 1비트 개수를 반환해주는 메소드
1111(2) -> 4
1101(2) -> 3

## 4. 숫자의 표현

### 문제 설명
자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.
- 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
- 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
- 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.
  예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.  
  자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.
### 제한사항
- n은 1,000,000 이하의 자연수 입니다.

### 입출력 예
|  n | result |
|---:|-------:|
| 78 |     83 |
| 15 |     23 |

### 입출력 예 설명
입출력 예#1
문제 예시와 같습니다.
입출력 예#2
15(1111)의 다음 큰 숫자는 23(10111)입니다.

### Solution.java
``` java
import java.util.*;

class Solution {
    public int solution(int n) {
        int answer = 0;
        
        int nextCount = Integer.bitCount(n);
        
        while(true) {
            n++;
            if (nextCount == Integer.bitCount(n)) {
                answer = n;
                break;
            }
        }
        
        return answer;
    }
}
```
## 5. 카펫


### 문제 설명
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고   
테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![](https://github.com/dididiri1/java-algorithm/blob/main/programmers/images/02_01.png?raw=true)


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

### 입출력 예 설명
입출력 예#1
문제 예시와 같습니다.
입출력 예#2
15(1111)의 다음 큰 숫자는 23(10111)입니다.

### 이 문제를 풀기 위해서는 다음 조건에 대해 이해해야합니다.
- 가로와 세로의 크기가 3이상이어야 한다.

가로와 세로의 크기가 3보다 작다면 yellow가 있을 자리가 없습니다.
![](https://github.com/dididiri1/java-algorithm/blob/main/programmers/images/02_02.png?raw=true)
- yellow의 넓이 구하기
  brown이 10, yellow가 2일 때를 예로들면,


![](https://github.com/dididiri1/java-algorithm/blob/main/programmers/images/02_03.png?raw=true)

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

