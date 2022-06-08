---
title:  "[프로그래머스] 정수삼각형"
excerpt: "삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요."

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2022-02-21
last_modified_at: 2022-02-21
---

# 정수 삼각형

문제 설명

![image](https://grepp-programmers.s3.amazonaws.com/files/production/97ec02cc39/296a0863-a418-431d-9e8c-e57f7a9722ac.png)

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

제한사항
삼각형의 높이는 1 이상 500 이하입니다.
삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

#접근방법

처음에는 이것을 DFS로 해서 풀려고 했다. 그랬더니 계속 시간 초과가 나오길래 무언가
시간을 많이 잡아먹는 요소가 있구나 했다.
```java
    class Solution {
        int answer = 0;
        public int solution(int[][] triangle) {
            
            DFS(0,0,triangle,answer);
            return answer;
        }
        
        public void DFS(int depth,int row,int[][] triangle,int sum){
            if(depth+1==triangle.length){
                sum += triangle[depth][row];
                answer=Math.max(sum,answer);
                return;
            }
            sum += triangle[depth][row];
            DFS(depth+1,row,triangle,sum);
            DFS(depth+1,row+1,triangle,sum);
        }
    }

처음에 내가 풀었던 방식인데 이 방식으로 하면 맨처음 7이 depth 0이라고 할 때,
depth 1의 3과 8의 경우 둘 다 1을 더하게 되는 중복이 일어나게 되었다.
그래서 이것을 탑다운 방식으로 풀게되면 이 사단이 일어나겠구나 해서 다운탑방식으로
풀게되었다.

    class Solution {
        public int solution(int[][] triangle) {
            for(int i=triangle.length-2;i>=0;i--){
                for(int j=0; j<triangle[i].length;j++){
                    triangle[i][j]=Math.max(triangle[i+1][j],triangle[i+1][j+1])
                    + triangle[i][j];
                }
            }
        return triangle[0][0];
        }
    }
```