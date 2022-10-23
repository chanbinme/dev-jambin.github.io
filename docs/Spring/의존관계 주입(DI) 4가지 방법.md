---
layout: default
title: 의존관계 주입(DI) 4가지 방법
parent: Spring
nav_order: 2
---

# **Spring - 의존관계 주입(DI) 4가지 방법**

의존성 주입은 크게 4가지 방법이 있다. 4가지 주입 방법과 어떤 방법을 사용하는 것이 바람직한지 알아보자

- 생성자 주입
- setter 주입
- 필드 주입
- 일반 메서드 주입

## 생성자 주입

- 생성자를 통해서 의존 관계를 주입하는 방법이다.
- 생성자 주입은 생성자 호출시점에 딱 1번만 호출되는 것이 보장된다.
- 변하지 않으며(불변), 반드시 필요한(필수) 의존관계에 사용한다.

```java
@Component
public class ServiceImpl implements Service {
	
	private final MemberRepository memberRepository;

	// 생성자 주입
	@Autowired // 생성자가 1개만 있으면 생략 가능(스프링에서만 가능)
	pulic ServiceImpl(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
}
	
```

## setter 주입

- setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법
- 변경 가능하며(변경), 선택적인 의존관계에서 사용한다.

```java
@Component
public class ServiceImpl implements Service {
	
	private MemberRepository memberRepository;

	@Autowired
	public void setMemberRepository(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
}
```

## 필드 주입

- 필드에 바로 주입하는 방법
- 코드가 간결해지지만 외부에서 변경이 불가능하기때문에 테스트하기 어렵다는 단점이 있다.
- DI 프레임워크가 없으면 아무것도 할 수 없다.
- 스프링 설정을 목적으로 하는 @Configuration 같은 곳에서만 특별한 목적으로 사용한다.
- **왠만하면 사용하지 말자**

```java
@Component
public class ServiceImpl implements Service {

	@Autowired
	private MmeberRepository membeRepository;
}
```

## 일반 메서드 주입

- 일반 메서드를 통해 주입하는 방법
- 한 번에 여러 필드를 주입 받을 수 있다.
- 일반적으로 잘 사용하지 않는다.

```java
@Component
public class ServiceImpl implements Service {
	
	private MemberRepository memberRepository;

	@Autowired
	public void init(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
}
```

## 생성자 주입을 사용하자!

과거에는 수정자 주입과 필드 주입을 많이 사용했지만, 최근에는 스프링을 포함한 DI 프레임워크 대부분이 생성자 주입을 권장한다.

왜 생성자 주입을 권장하는걸까?

### 불변

- 일반적으로 의존관계 주입은 한 번 일어나면 애플리케이션이 종료될 때까지 변경할 일이 없다. 오히러 대부분의 의존관계는 불변해야 한다.
- setter 주입을 사용하게 되면 메서드를 public으로 열어두어야 하기 때문에 누군가 실수로 코드를 변경할 수도 있고,  불변해야하는 메서드를 열어두는 것도 좋은 설계 방법이 아니다.
- 생성자 주입은 객체를 생성할 때 딱 1번만 호출된다. 이후에 호출되는 일이 없기 때문에 불변하게 설계할 수 있다.

### 누락

- 프레임워크가 없는 상태에서 주입 데이터가 누락되었을 때 setter 의존관계는 실행은 되지만 NPE(Null Point Exception)이 발생한다.
- 반면, 생성자 주입은 주입 데이터가 누락되어있으면 컴파일 오류가 발생한다. 그리고 IDE에서 어떤 값을 필수로 주입해야 하는지 알려준다.

### final

- 생성자 주입은 필드에 `final` 키워드를 사용할 수 있다. 그래서 혹시라도 값이 설정되지 않는 오류를 컴파일 시점에서 알 수 있고 실행 전에 문제를 해결할 수 있다.
- 나머지 주입 방식(setter 주입, 필드 주입, 메서드 주입)은 모두 생성자 이후에 호출되기 때문에 필드에 `final` 키워드를 사용할 수 없다. 생성자 주입 방식만 `fina` 키워드를 사용 가능하다.

```java
@Component
  public class ServiceImpl implements Service {

      private final MemberRepository memberRepository;
      private final DiscountPolicy discountPolicy;

@Autowired
      public ServiceImpl(MemberRepository memberRepository, DiscountPolicy
  discountPolicy) {
          // discountPolicy 필드 누락
          this.memberRepository = memberRepository;
      }
      //...   
}

// 컴파일 오류 발생
java: variable discountPolicy might not have been initialized
```

## 한 줄 정리

일반적으로는 생성자 주입을 사용하고 필수 값이 아닌 경우에 옵션으로 setter 주입을 사용하는 것이 좋다. (필드 주입과 메서드 주입은 사용하지 말자)

## 참고

[김영한님의 인프런 스프링 핵심 원리 - 기본편](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)