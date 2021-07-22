---
title:  "[프로그래머스] 섬 연결하기"
excerpt: "n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요."

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2021-07-22
last_modified_at: 2021-07-22
---

# 섬 연결하기

문제 설명
n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

제한사항

섬의 개수 n은 1 이상 100 이하입니다.
costs의 길이는 ((n-1) * n) / 2이하입니다.
임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
연결할 수 없는 섬은 주어지지 않습니다.
입출력 예

n	costs	return
4	[[0,1,1],[0,2,2],[1,2,5],[1,3,1],[2,3,8]]	4
입출력 예 설명

costs를 그림으로 표현하면 다음과 같으며, 이때 초록색 경로로 연결하는 것이 가장 적은 비용으로 모두를 통행할 수 있도록 만드는 방법입니다.

![image](https://user-images.githubusercontent.com/64392631/126606038-be03c224-fcf5-4edf-bb2a-daa1d4f68f83.png)

아직 알고리즘 유형에 대해 해박하지 못한 나는 MST(Minimum Spannin Tree)라는 것을 이용해 푸는 거라고 생각하지 못했다. MST는 크루스칼 알고리즘으로 해결하는 것이다.

크루스칼 알고리즘 해결방법은

1. 비용이 최소인 것들을 오름차순으로 정렬

2. 비용이 최소인 것들부터 간선을 연결하고 사이클이 생성되지 않도록 한다.
   
이 문제에서 코드를 한 메소드씩 끊어서 보면,
find 메소드는 현재 노드의 최상위 부모를 찾는 것이다. 만약 내가 최상위 부모이면 return으로 자신이 나올 것이고 아니면 최상위 부모의 값이 나올 것이다.

    public int find(int x)
    {
        
        if(x==parent[x])

            return x;
        return parent[x]=find(parent[x]);
    }

다음은 check메소드다. 각 노드들의 최상위 부모를 찾은 후 만약 둘이 같다면 연결할 필요가 없으니 false값을 주고 만약 둘이 다르다면 새로 합치고 true값을 반환한다.

    public boolean check(int x, int y){
            int a = find(x);
            int b = find(y);
            if(a==b)
                return false;
            return true;
        }

다음은 union메소드다. 방금 전 check메소드에서 true값이게 되면 합쳐주면서 부모를 설정해주게 된다.

    public void union(int x, int y){
            int a= find(x);
            int b= find(y);
            
            if(a>b){
                int temp=a;
                a=b;
                b=temp;
            }
            parent[b]=a;
        }

제일 중요한 가중치에 따라 오름차순으로 정리하는 방법이다. Comparable과 compareTo를 사용하여 Node들 중에 weight에 따라서 작은 것부터 큰 것까지 정리하는 sort다.

    class Node implements Comparable<Node>{
            int from, to, weight;
            Node(int from, int to, int weight){
                this.from = from;
                this.to = to;
                this.weight = weight;
            }
            @Override
            public int compareTo(Node o){
                return this.weight - o.weight;
            }
        }

마지막은 모든 코드와 같이 첨부하겠다. 처음엔 모두 자기 자신이 부모노드라고 설정한 뒤 weight가 낮은 것 부터 순서대로 만약 최상위 부모가 새로 들어온 노드와 겹치지 않는다면 합쳐주면서 weight를 answer에 합쳐주는 방법으로 문제를 풀 수 있다.


    import java.util.*;

    class Solution {

        int parent[];

        public int solution(int n, int[][] costs) {
            int answer = 0;
            parent = new int[n];
            ArrayList<Node> list = new ArrayList<>();
            
            for(int i=0; i<costs.length; i++){
                list.add(new Node(costs[i][0],costs[i][1],costs[i][2]));
            }
            
            for(int i=0; i<n; i++)
            {
                parent[i]=i;
            }
            
            Collections.sort(list);
            
            for(int i=0; i<list.size(); i++)
            {
                Node a=list.get(i);
                if(check(a.from, a.to)){
                    answer+=a.weight;
                    union(a.from, a.to);
                }
            }
            
            return answer;
        }
        public int find(int x){
            if(x==parent[x])
                return x;
            return parent[x]=find(parent[x]);
        }
        
        public boolean check(int x, int y){
            int a = find(x);
            int b = find(y);
            if(a==b)
                return false;
            return true;
        }
        
        public void union(int x, int y){
            int a= find(x);
            int b= find(y);
            
            if(a>b){
                int temp=a;
                a=b;
                b=temp;
            }
            parent[b]=a;
        }
        
        class Node implements Comparable<Node>{
            int from, to, weight;
            Node(int from, int to, int weight){
                this.from = from;
                this.to = to;
                this.weight = weight;
            }
            @Override
            public int compareTo(Node o){
                return this.weight - o.weight;
            }
        }
    }