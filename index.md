---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# **[03_[구현] 보드 게임](https://urclass.codestates.com/classroom/32)**

## **문제**

N * N의 크기를 가진 보드판 위에서 게임을 하려고 합니다. 게임의 룰은 다음과 같습니다.

1. 좌표 왼쪽 상단(0, 0)에 말을 놓는다.
2. 말은 상, 하, 좌, 우로 이동할 수 있고, 플레이어가 조작할 수 있다.
3. 조작의 기회는 딱 한 번 주어진다.
4. 조작할 때 U, D, L, R은 각각 상, 하, 좌, 우를 의미하며 한 줄에 띄어쓰기 없이 써야 한다.
    - 예시: `UDDLLRRDRR`, `RRRRR`
5. 한 번 움직일 때마다 한 칸씩 움직이게 되며, 그 칸 안의 요소인 숫자를 획득할 수 있다.
6. 방문한 곳을 또 방문해도 숫자를 획득할 수 있다.
7. 보드 밖을 나간 말은 OUT 처리가 된다.
8. 칸 안의 숫자는 0 또는 1이다.
    1. 단, 좌표 왼쪽 상단(0, 0)은 항상 0이다.
9. 획득한 숫자를 합산하여 숫자가 제일 큰 사람이 이기게 된다.

보드판이 담긴 board와 조작하려고 하는 문자열 operation이 주어질 때, 말이 해당 칸을 지나가면서 획득한 숫자의 합을 구하는 함수를 작성하세요.

## **입력**

### **인자 1: board**

- `int` 타입의 2차원 배열
- 2 <= board.length <= 1,000
- 예: `[ [0, 0, 1], [1, 0, 1], [1, 1, 1] ]`

### **인자 2: operation**

- `string` 타입의 대문자 영어가 쓰여진 문자열
- 1 <= operation.length <= board.length * 2
- U, L, D, R 이외의 문자열은 없습니다.

## **출력**

- `int` 타입을 반환해야 합니다.
    - board와 operation이 입력값의 예시 (`[ [0, 0, 1], [1, 0, 1], [1, 1, 1] ]`, `DDR`)일 때, (0, 0) -> (1, 0) -> (2, 0) -> (2, 1) 순서로 이동하게 되고, 각 0, 1, 1, 1을 얻어 `3`을 반환합니다.

## **주의사항**

- 만약, 말이 보드 밖으로 나갔다면 즉시 `null` 을 반환합니다.

## **입출력 예시**

```java
int[][] board1 = new int[]{
  {0, 0, 0, 1},
  {1, 1, 1, 0},
  {1, 1, 0, 0},
  {0, 0, 0, 0}
}
int output1 = boardGame(board1, "RRDLLD");
System.out.println(output1); // 4

int[][] board2 = new int[]{
  {0, 0, 1},
  {1, 1, 1},
  {1, 0, 0}
}
int output2 = boardGame(board2, "UUUDD");
System.out.println(output2); // null

int[][] board3 = new int[][]{
  {0, 0, 0, 0, 0},
  {0, 0, 1, 0, 0},
  {0, 0, 0, 0, 0},
  {0, 0, 0, 1, 0},
  {0, 0, 0, 0, 0}
}
int output3 = boardGame(board3, "DDRRRUDUDUD");
System.out.println(output3); // 0
```

## 풀이

```java
package com.codestates.coplit; 
import java.util.*;

public class Solution { 
	public Integer boardGame(int[][] board, String operation) {
    // TODO:
		// 구현은 길고 긴 수많은 조건들을 만족해줘야 한다.
		// 수도코드 필수
		// [참고 룰]
		// 방문한 곳을 또 방문해도 숫자를 획득할 수 있다.(중복 허용)
		// 칸 안의 숫자는 0 또는 1이다. 단, 좌표 왼쪽 상단(0, 0)은 항상 0이다.
		// 획득한 숫자를 합산하여 숫자가 제일 큰 사람이 이기게 된다. 
		
		// [게임 룰]
		// 점수 
		int score = 0;
		// 좌표 왼쪽 상단(0,0)에 말을 놓는다.		
		// 위아래를 움직일 ud, 좌우를 움직일 lr 
		int ud = 0;
		int lr = 0;

		// 조작을 마무리할 때까지 반복
		for(int i = 0; i < operation.length(); i++) {
		// (조건1)말은 상, 하, 좌, 우로 이동할 수 있다.
		// 한 번 움직일 때마다 한 칸씩 움직이게 되며, 그 칸 안의 요소인 숫자를 획득할 수 있다.
		// U(n+1, n)D(n-1, n)L(n, n-1)R(n, n+1)은 각각 상하좌우를 의미한다. 한 줄에 띄어쓰기 없이 써야 한다. 
			switch(operation.charAt(i)) {
				case 'U': ud -= 1;
									break;
				case 'D': ud += 1;
									break;
				case 'L': lr -= 1;
									break;
				case 'R': lr += 1;
									break;
			}
		// 보드 밖을 나간 말은 OUT 처리가 된다.
		if(ud < 0 || ud >= board.length) return null;
		if(lr < 0 || lr >= board.length) return null;
		// 해당 위치의 숫자 score에 더함
		score += board[ud][lr];
		}
		// 최종 score 리턴
		return score;
	} 
}
```

## 레퍼런스

```java
package com.codestates.coplit; 
import java.util.*;

public class Solution { 
	public Integer boardGame(int[][] board, String operation) {
		//HashMap을 선언한 후, 입력되는 명령어에 따라 이동할 좌표를 넣어줍니다.
    HashMap<String, int[]> DIR = new HashMap<String, int[]>(){{
      put("U", new int[]{-1, 0});
      put("D", new int[]{1, 0});
      put("L", new int[]{0, -1});
      put("R", new int[]{0, 1});
    }};
		//보드의 길이를 선언합니다.
    int LEN = board.length;
		//시작 좌표와, 점수를 0으로 할당합니다.
    int Y = 0;
    int X = 0;
    int score = 0;

		//입력받은 operation을 char배열로 변환합니다.
    char[] chars = operation.toCharArray();

		//해당 배열만큼 반복합니다.
    for(int i = 0; i < chars.length; i++) {
      int dY = DIR.get(String.valueOf(chars[i]))[0];
      int dX = DIR.get(String.valueOf(chars[i]))[1];
      Y += dY;
      X += dX;
			//isValid 함수를 이용하여, 이동이 불가능한 경우 null을 반환합니다.
      if (!isValid(Y, X, LEN)) return null;
			//이동이 가능한 경우, 해당 보드의 값만큼 전체 점수에 더해줍니다.
      score += board[Y][X];
    }
		//전체 점수를 반환합니다.
    return score;
  }
	//이동이 가능한지 확인하여 boolean으로 결과를 반환하는 함수
  public boolean isValid(int y, int x, int LEN) {
		//최소값과, 최대값을 벗어나면 false, 가능하다면 true를 반환합니다.
    return 0 <= y && y < LEN && 0 <= x && x < LEN;
  }
}
```