---
title:  "[백준] 카드2"
excerpt: "N장의 카드가 있다. 각각의 카드는 차례로 1부터 N까지의 번호가 붙어 있으며, 1번 카드가 제일 위에, N번 카드가 제일 아래인 상태로 순서대로 카드가 놓여 있다.

이제 다음과 같은 동작을 카드가 한 장 남을 때까지 반복하게 된다. 우선, 제일 위에 있는 카드를 바닥에 버린다. 그 다음, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮긴다.

예를 들어 N=4인 경우를 생각해 보자. 카드는 제일 위에서부터 1234 의 순서로 놓여있다. 1을 버리면 234가 남는다. 여기서 2를 제일 아래로 옮기면 342가 된다. 3을 버리면 42가 되고, 4를 밑으로 옮기면 24가 된다. 마지막으로 2를 버리고 나면, 남는 카드는 4가 된다.

N이 주어졌을 때, 제일 마지막에 남게 되는 카드를 구하는 프로그램을 작성하시오."

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2022-06-08
last_modified_at: 2022-06-08
---

## 문제

N장의 카드가 있다. 각각의 카드는 차례로 1부터 N까지의 번호가 붙어 있으며, 1번 카드가 제일 위에, N번 카드가 제일 아래인 상태로 순서대로 카드가 놓여 있다.

이제 다음과 같은 동작을 카드가 한 장 남을 때까지 반복하게 된다. 우선, 제일 위에 있는 카드를 바닥에 버린다. 그 다음, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮긴다.

예를 들어 N=4인 경우를 생각해 보자. 카드는 제일 위에서부터 1234 의 순서로 놓여있다. 1을 버리면 234가 남는다. 여기서 2를 제일 아래로 옮기면 342가 된다. 3을 버리면 42가 되고, 4를 밑으로 옮기면 24가 된다. 마지막으로 2를 버리고 나면, 남는 카드는 4가 된다.

N이 주어졌을 때, 제일 마지막에 남게 되는 카드를 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 정수 N(1 ≤ N ≤ 500,000)이 주어진다.

## 출력
첫째 줄에 남게 되는 카드의 번호를 출력한다.

## 문제풀이

처음에는 ArrayList를 사용하여 풀려고 했으나 계속 시간 초과가 뜨길래 무엇이 문제인지 몰랐다. 지금까지 ArrayList들을 사용했을 때 대부분 시간초과가 뜨길래 그냥 바꿔서 풀었는데 이유를 찾아보니 ArrayList는 add나 remove시 모든 index를 copy해오기 때문에 시간복잡도가 O(n)이 나온다는 것이었다. 그래서 다음부터는... 웬만하면 arraylist는 사용하면 안된다고 생각했다. 그래서 그냥 바로 queue를 적용해서 풀었다. queue도 add는 똑같이 시간복잡도 O(n)이 나오니 반드시 offer를 사용하자!

```java
import java.io.*;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        Queue<Integer> q = new LinkedList<>();

        for(int i=0; i<n; i++) q.offer(i+1);

        while(q.size()>1){
            q.poll();
            q.offer(q.poll());
        }

        System.out.println(q.poll());
    }
}
```

코드도 엄청 짧고 간단하다. 지금까지 대부분 문제들은 scanner를 사용했지만 bufferedreader를 사용하도록 연습중이다. 인풋과 아웃풋이 자주반복될때는 bufferedreader가 시간을 덜잡아먹기 때문에 당분간은 bufferedreader만 사용할 예정이다.