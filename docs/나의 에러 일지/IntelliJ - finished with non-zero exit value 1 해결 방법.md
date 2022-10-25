---
layout: default
title: IntelliJ Error - finished with non-zero exit value 1 해결 방법
parent: 나의 에러 일지
nav_order: 2
---

# **IntelliJ Error - finished with non-zero exit value 1 해결 방법**

![에러 Image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fcb9887b-76c7-4641-bd2b-d19e5220fb3f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-25_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.04.26.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221025%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221025T072335Z&X-Amz-Expires=86400&X-Amz-Signature=35d62beb3ca4b333e2c7ef53b97a00188d452c81ef7a5b57b6a29a7c426c5767&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202022-10-25%2520%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE%25203.04.26.png%22&x-id=GetObject)

```java
Execution failed for task ':Application.main()'.

> Process 'command 'JDK경로/bin/java.exe'' finished with non-zero exit value 1
```

이번에 소개할 에러는 `finishi with non-zero exit value 1`  이 녀석이다.

Intellij, Gradle 환경에서 Spring 코드를 실행한 후 해당 에러를 만났다.

## 해결 방법

1. [File > Settings > Build, Excution, Deployment > Build Tools > Gradle] 이 경로로 이동
2. [Build and run using]과 [Run tests using]을 IntelliJ IDEA로 변경
3. [Gradle JVM] 버전을 현재 프로젝트 버전과 동일한 버전으로 변경
4. 다시 실행

![사진](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ff82af70-e792-4ca0-9f66-230a2ab52cbb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-24_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_10.54.03.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221024%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221024T142434Z&X-Amz-Expires=86400&X-Amz-Signature=37193993bc48a32f2cfc90a1889bb374014b85076197a97d2b471350d20adfa9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202022-10-24%2520%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE%252010.54.03.png%22&x-id=GetObject)

1. 그래도 에러가 발생한다면 IntelliJ를 재부팅해보자
2. 해결!

![스크린샷 2022-10-24 오후 11.18.25.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e9d842c1-0750-466f-be63-1f664ee3a2ba/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-24_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.18.25.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221024%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221024T142513Z&X-Amz-Expires=86400&X-Amz-Signature=dfbb6a1900d262d90398051d87abf28a055477e6756f61f8a9ecfc59cf5cab92&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA%25202022-10-24%2520%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE%252011.18.25.png%22&x-id=GetObject)