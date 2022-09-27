---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# 의사코드(pseudocode) 작성법

> 의사코드는 프로그래밍 언어로 코드를 작성하기 전에 우리가 쓰는 일상 언어로 프로그램이 작동하는 논리를 먼저 작성하는 것을 말한다.
> 

## 의사코드를 쓰면 어떤 장점이 있을까?

1. **시간이 단축된다.**

문제가 복잡하고 코드 양이 길어질수록 구체적이고 세세한 로직이 기억나지 않을 것이다. 결국 작성하는 시간보다 헤매는 시간이 더 길어질 가능성이 크다. 그러나 수도코드를 남겨 놓으면 지표가 되어 헤매는 시간이 줄어든다. 

1. **디버깅에 용이하다.**

의사코드를 확인하면서 디버깅을 하면 원인 파악이 쉬워진다.

1. **프로그래밍 언어를 모르는 사람과 소통할 수 있다.**

프로그래밍 언어에 익숙하지 않은 사람도 나의 수도 코드를 보며 로직을 이해하는 데 도움이 될 수 있다. 우리가 쓰는 일상 언어로 쓰여있기 때문에 현업에서 비개발자와도 소통하기 용이하다. 

## 의사코드는 구체적으로 써야한다.

컴퓨터는 0과 1밖에 모르는 바보다. 컴퓨터에게 땅콩잼 토스트 만들어달라고 하면 치킨을 만드는 로직을 기초적인 부분부터 구체적이고 상세하게 명령해야 한다. 

```java
// 마스크 착용을 컴퓨터에게 명령해야 한다면?

1. 마스크를 꺼낸다.
2. 마스크 날개를 펼치고 날개 끝을 잡아 오므린다.
3. 고정심 부분을 위로 잡고 턱에서 시작하여 코와 입을 완전히 가린다.
4. 만약 귀걸이 마스크라면 왼쪽 귀와 오른쪽 귀에 걸어준다.
		만약 귀걸이 마스크가 아니라면 마스크를 머리 뒤쪽으로 걸어준다.
5. 고정심을 코에 밀착되도록 누른다.
6. 양 손으로 마스크 전체를 누르며 공기 누설이 있는지 체크한다.
7. 만약 공기 누설이 있다면, 5번으로 돌아간다.
8. 공기 누설이 없다면 마스크 착용 완료.
```

## 의사코드 작성 양식

대표적으로 두 가지 방식이 있다.

- 다른 사람도 이해할 수 있는 자연어(영어나 한국어처럼 일상에서 사용되는 언어)만 사용한다.

```java
// 배열의 각 요소들이 그 이전의 요소들의 합보다 큰지 여부를 확인하는 함수
public Boolean superIncreasing(int[] arr) {

// 변수 sum을 선언하고, 0번째 요소를 할당한다.

// 1번째 요소부터, 가장 마지막 요소까지 순회하는 반복문을 만든다.

	// 만약 arr[i]가 sum보다 작거나 같으면 false를 반환한다.

	// 그렇지 않으면, 기존의 sum에 arr[i]를 더한다.

//반복문이 끝나면 true를 반환한다.

}
```

```java
// 배열의 각 요소들이 그 이전의 요소들의 합보다 큰지 여부를 확인하는 함수
public Boolean superIncreasing(int[] arr) {

  // 변수 sum을 선언하고, 0번째 요소를 할당한다.
  int sum = arr[0];

  // 1번째 요소부터, 가장 마지막 요소까지 순회하는 반복문을 만든다.
  for (int i = 1; i < arr.length; i++) {

    // 만약 arr[i]가 sum보다 작거나 같으면
    if (arr[i] <= sum) {
      // false를 반환한다.
      return false;
    } else {
      // 그렇지 않으면, 기존의 sum에 arr[i]를 더한다.
      sum = sum + arr[i];
    }
    //반복문이 끝나면 true를 반환한다.
  }
  return true;
}
```

- 자연어와 프로그램 언어의 조합을 사용한다.

```java
// 문자열을 입력받아 연속된 한자리 홀수 숫자 사이에 '-'를 추가한 문자열을 리턴하는 함수

public String insertDash(String str) {
	//입력된 String을 char을 요소로 가지는 배열로 변환합니다.

	//for(1번째 요소부터, 가장 마지막 요소까지 순회)

		//if(str[i-1], str[i] 둘다 홀수라면)

			//result에 str[i]와 '-' 를 추가한다.

		// else() result에 str[i]만 추가한다.

		//예외 케이스로 문자열의 마지막을 추가한다.

	//반복문이 끝나면 result를 반환한다.

}
```

```java
// 문자열을 입력받아 연속된 한자리 홀수 숫자 사이에 '-'를 추가한 문자열을 리턴하는 함수

public String insertDash(String str) {
	//입력된 String을 char을 요소로 가지는 배열로 변환합니다.
  char[] arrCh = str.toCharArray();
	//결과를 저장할 result 변수를 선언, 빈 값을 할당합니다.
  String result = "";

  for(int i = 1; i < arrCh.length; i++) {
		//앞선 문자열과 이후 문자열을 비교할 변수를 선언후, 해당 값을 int로 변환합니다.
    int preChar = Character.getNumericValue(arrCh[i - 1]);
    int curChar = Character.getNumericValue(arrCh[i]);
		//두 문자열이 모두 홀수라면
    if(preChar % 2 == 1 && curChar % 2 == 1) {
			//결과에 이전값과 "-"를 함께 저장합니다.
      result = result + preChar + "-";
    } else {
			//하나라도 홀수가 아니라면, 결과에 이전값만 추가로 저장합니다.
      result = result + preChar;
    }
		//인덱스가 마지막일 경우, 맨 마지막 char을 추가합니다(예외 케이스)
    if(i == arrCh.length - 1) result = result + curChar;
  }
  return result;
}
```

<aside>
💡 중요한 것은 자신만의 원칙을 만들어, 일관성 있고 다른 사람도 이해할 수 있는 수도코드를 작성하는 것이다.

</aside>