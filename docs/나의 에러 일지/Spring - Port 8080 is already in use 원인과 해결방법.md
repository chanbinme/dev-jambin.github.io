---
layout: default
title: Spring - Port 8080 is already in use 원인과 해결방법
parent: 나의 에러 일지
nav_order: 2
---

# **Spring - PortInUseException: Port 8080 is already in use 원인과 해결방법**

![스크린샷 2022-10-24 오후 11.06.28.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5671b3de-743b-4210-8f94-fd08d29bde06/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-24_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.06.28.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221025%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221025T072115Z&X-Amz-Expires=86400&X-Amz-Signature=2918f5bf8c886c6398b3201bb2267c307f066a2589fda1dabb92a951f2f11d87&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202022-10-24%2520%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE%252011.06.28.png%22&x-id=GetObject)

```java
org.springframework.boot.web.server.PortInUseException: Port 8080 is already in use
```

오늘 소개할 친구는 `PortInUseException: Port 8080 is already in use` 요 녀석이다.

SpringMVC를 연습하던 중 로컬을 확인하기 위해 실행하다가 만난 에러다.

사실 이전에도 한 번 만난적 있는데 생각보다 자주 만나게 되서 블로그에 남기기로 했다.  원인과 해결방법 모두 생각보다 간단하다.

## 원인

원인은 2가지 정도로 볼 수 있다.

- 이미 사용중인 포트를 다른 애플리케이션에서 사용하려고 할 때
- IDE에서는 프로세스가 종료되었지만 실제로 프로세스가 종료되지 않고 계속해서 실행중일 때

보통 두 번째 이유때문에 해당 에러가 발생한다. 나도 IDE를 한 번 종료했다가 다시 실행시키면서 해당 에러가 발생했다.

## 해결 방법

해결방법은 간단하다. cmd에서 실행중인 포트를 종료하면 된다.

종료 방법은 OS에따라 다르기대문에 Mac과 Window로 나누어서 설명하겠다.

### Mac

1. cmd를 열어 아래 명령어로 PID를 찾는다.

```java
lsof -i : [포트 번호]
```

1. 해당 PID를 아래 명령어에 입력해 프로세스를 강제 종료한다.

```java
kill -9 [PID]
```

![스크린샷 2022-10-25 오후 4.02.12.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/816ed7b3-4a39-4d87-a167-81a9d67a3588/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-25_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_4.02.12.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221025%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221025T072138Z&X-Amz-Expires=86400&X-Amz-Signature=453197dcd630a2df62e921ee52bf6a8cb8632e6223e93a60a180a6cd2bf13aff&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202022-10-25%2520%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE%25204.02.12.png%22&x-id=GetObject)

### Window

1. cmd를 열어 아래 명령어를 입력한다.

```java
netstat -ano
```

1. 종료해야하는 포트 번호를 가진 로컬 주소의 PID를 확인한 후 아래 명령어에 입력한다.

```java
taskkill /f /pid [PID]
```

필자는 Mac을 사용하고 있기 때문에 Window 이미지는 없다. 미안합니다ㅠ