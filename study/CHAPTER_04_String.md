# CHAPTER 4 문자열

## 자연수 뒤집어 배열로 만들기 - Level 1

### 문제 설명
자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요.   
예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

### 제한 조건
- n은 10,000,000,000이하인 자연수입니다.


### 입출력 예

| n     | return      |
|:------|:------------|
| 12345 | [5,4,3,2,1] |


### Solution.java
``` java
import java.util.*;

class Solution {
    public int[] solution(long n) {
     
        int[] answer = new StringBuffer().append(n).reverse().chars().map(Character::getNumericValue).toArray();
 
        return answer;
    }
}
``` 

## 시저 암호 - Level 1

### 문제 설명
어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다.   
예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다.   
"z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

### 제한 조건
- 공백은 아무리 밀어도 공백입니다.
- s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
- s의 길이는 8000이하입니다.
- n은 1 이상, 25이하인 자연수입니다.
- 
### 입출력 예

| s       | n | result  |
|:--------|:--|:--------|
| "AB"    | 1 | "BC"    |
| "z"     | 1 | "a"     |
| "a B z" | 4 | "e F d" |


### Solution.java
``` java
import java.util.*;

class Solution {
    
    public char push(char c, int n) {
        if (!Character.isAlphabetic(c)) {
            return c;
        }
        
        int offset = Character.isUpperCase(c) ? 'A' : 'a';
        int position = c - offset;
        position = (position+n) % ('Z'-'A'+1);
        
        return (char) (offset+position);    
    }
    
    public String solution(String s, int n) {
        String answer = "";
        
        StringBuilder str = new StringBuilder();
        for(char c : s.toCharArray()) {
            str.append(push(c, n));
        }
        
        answer= str.toString();
        
        return answer;
    }
}
``` 


## 이상한 문자 만들기

### 문제 설명
문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다.   
각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

### 제한 조건
- 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
- 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.


### 입출력 예

| s                 | return            |
|:------------------|:------------------|
| "try hello world" | "TrY HeLlO WoRlD" |


### 입출력 예 설명
"try hello world"는 세 단어 "try", "hello", "world"로 구성되어 있습니다.
각 단어의 짝수번째 문자를 대문자로, 홀수번째 문자를 소문자로 바꾸면 "TrY", "HeLlO", "WoRlD"입니다.   
따라서 "TrY HeLlO WoRlD" 를 리턴합니다.

### Solution.java
``` java
import java.util.*;

class Solution {
    public String solution(String s) {
        String answer = "";
        boolean toUpper = true;
        
        for(char c : s.toCharArray()) {
            if(!Character.isAlphabetic(c)) {
                answer += c;  
                toUpper = true;
            } else {
                if (toUpper) {
                    answer += Character.toUpperCase(c);
                } else {
                    answer += Character.toLowerCase(c);
                }
                toUpper = !toUpper;
            }
        }
          
        return answer;
    }
}
``` 

## 3진법 뒤집기 - Level 1

### 문제 설명
자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후,   
이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.

### 제한 조건
- n은 1 이상 100,000,000 이하인 자연수입니다.


### 입출력 예

| n   | return |
|:----|:-------|
| 45  | 7      |
| 125 | 229    |

### 입출력 예 설명
#### 입출력 예 #1
- 답을 도출하는 과정은 다음과 같습니다.

| n (10진법) | n (3진법) | 앞뒤 반전(3진법) | 10진법으로 표현  |
|:---------|:-------|:-----------|:-----------|
| 45       | 1200      | 0021       | 7          |

- 따라서 7을 return 해야 합니다.

#### 입출력 예 #2
- 답을 도출하는 과정은 다음과 같습니다.

| n (10진법) | n (3진법) | 앞뒤 반전(3진법) | 10진법으로 표현 |
|:---------|:--------|:-----------|:----------|
| 125      | 11122   | 22111      | 229       |

- 따라서 229를 return 해야 합니다.

### Solution.java
``` java
import java.util.*;

class Solution {
    public int solution(int n) {
        int answer = 0;
        
        String str = new StringBuilder(Integer.toString(n, 3)).reverse().toString();
        answer = Integer.valueOf(str, 3);
        
        return answer;
    }
}
``` 


## 이진 변환 반복하기 - Level 2

### 문제 설명
0과 1로 이루어진 어떤 문자열 x에 대한 이진 변환을 다음과 같이 정의합니다.  
1. x의 모든 0을 제거합니다.
2. x의 길이를 c라고 하면, x를 "c를 2진법으로 표현한 문자열"로 바꿉니다.

예를 들어, x = "0111010"이라면, x에 이진 변환을 가하면 x = "0111010" -> "1111" -> "100" 이 됩니다.

0과 1로 이루어진 문자열 s가 매개변수로 주어집니다. s가 "1"이 될 때까지
계속해서 s에 이진 변환을 가했을 때, 이진 변환의 횟수와 변환 과정에서 제거된 모든 0의 개수를 각각 배열에 담아
return 하도록 solution 함수를 완성해주세요.

### 제한 조건
- s의 길이는 1 이상 150,000 이하입니다.
- s에는 '1'이 최소 하나 이상 포함되어 있습니다.


### 입출력 예

| s     |  result       |
|:-----|:--------|
|  "110010101001"    |  [3,8]       |
|  "01110"    |   [3,3]      |
| "1111111"     |   [4,1]      |


### Solution.java
``` java
import java.util.*;

class Solution {
    
    public int countZero(String s) {
        int zero = 0;
        for(char c : s.toCharArray()) {
            if (c == '0') {
                zero ++;
            }
        }
        
        return zero;
    }
    
    public int[] solution(String s) {
        
        int loop = 0;
        int zeroCount = 0;
        
        while(!s.equals("1")) {
            loop ++;
            int zeros = countZero(s);
            zeroCount += zeros; // 제거할 0의 갯수
            
            int ones = s.length()- zeros; // 0 제거 후 길이 계산
            s = Integer.toString(ones, 2);
        }
        
        int[] answer = {loop, zeroCount};
        
        return answer;
    }
}
``` 