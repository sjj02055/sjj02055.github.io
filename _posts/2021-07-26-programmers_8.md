---
title:  "[프로그래머스] 네트워크"
excerpt: "컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오."

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2021-07-26
last_modified_at: 2021-07-26
---

# 네트워크

네트워크
문제 설명
네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

제한사항
컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
computer[i][i]는 항상 1입니다.

    입출력 예
    n	computers	return
    3	[[1, 1, 0], [1, 1, 0], [0, 0, 1]]	2
    3	[[1, 1, 0], [1, 1, 1], [0, 1, 1]]	1

입출력 예 설명
예제 #1
아래와 같이 2개의 네트워크가 있습니다.
![image](https://user-images.githubusercontent.com/64392631/126938690-ce4b5533-b877-4432-8df5-827c729bdb6b.png)

예제 #2
아래와 같이 1개의 네트워크가 있습니다.
![image](https://user-images.githubusercontent.com/64392631/126938707-c40469bd-22b8-4419-9916-43cd0e399690.png)

# 접근법
당연히 처음에 생각을 할 때 DP를 써야한다는 생각을 갖고 시작을 했다.

DP를 써서 computers[i][i]=1 인 상황만 제외하고 들르는 모든 지점에 갔었다는 check[i]=1 을 사용하여 방문하지 않은 지점을 갔을 때, answer++를 한 번씩 하여 답을 구하면 된다고 생각했다.


문제를 거의 다 풀었는데 이 for문에서 i=row+1로 해서 만약에 3컴퓨터에서 2컴퓨터로 돌아가는 생각을 못하고 풀어서 이거 하나에 1시간 반을 넘게 고민했던 것 같다. 이거 발견했을 때, 10년 묵은 체증이... 휴우...


    for(int i=0; i<check.length; i++)
                if(check[i]==0 && computers[row][i] == 1)
                {
                    DP(computers, i);
                }
            return;

내가 푼 코드는 다음과 같다.


    class Solution {
        int check[];
        int count=0;
        public int solution(int n, int[][] computers) {
            int answer = 0;
            check = new int[computers.length];
            
            for(int i=0; i<computers.length; i++)
                check[i]=0;
            
            for(int i=0; i<computers.length; i++)
            {
                if(check[i]==0) //DP를 돌렸는데 0이면
                    answer++;   //새로운 네트워크 추가
                DP(computers, i);   //DP 돌려~
            }
            
            return answer;
        }
        
        public void DP(int[][] computers, int row)
        {
            if(check[row]==1)   //방문했던 컴퓨터인지 확인
            {
                return;
            }
            check[row]=1;   //방문했다고 체크
            for(int i=0; i<check.length; i++)
                if(check[i]==0 && computers[row][i] == 1)
                {
                    DP(computers, i);
                }
            return;
        }
    }

