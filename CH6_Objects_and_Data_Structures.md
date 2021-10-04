# Chapter 6. Objects & Data Structures

시스템을 구현할 때, 새로운 자료 타입을 추가하는 유연성이 필요할 때는 객체가 적합.

반대로, 새로운 동작을 추가하는 유연성이 필요할 때에는 자료 구조와 절차적 코드가 적합하다.

<br>

### 목차

> 1. 자료 추상화
> 2. 자료/객체 비대칭
> 3. 디미터 법칙
>    1. 기차 충돌
>    2. 잡종 구조
>    3. 구조체 감추기
> 4. 자료 전달 객체
>    1. 활성 레코드

<br>

### 1. 자료 추상화

- 추상화 (Abstraction)
  - 구현을 숨기는 것
  - 단순히 변수를 private으로 선언하고, getter와 setter를 제공하는 것을 의미하는 것이 X
  - 추상 인터페이스를 제공해서 사용자가 코드의 구현을 모른채 자료의 핵심을 조작 가능하게 하는 것

- 6-1 구체적인 Point 클래스

```java
public class Point { 
  public double x; 
  public double y;
}
```

- 6-2 추상적인 Point 클래스

```java
public interface Point {
  double getX();
  double getY();
  void setCartesian(double x, double y); 
  double getR();
  double getTheta();
  void setPolar(double r, double theta); 
}
```

- 6-2는 구현을 완전히 숨기지만, 6-1은 내부 구조를 노출하고 개별적으로 좌표값을 읽고 설정하게 강제한다.

<br>

### 2. 자료/객체 비대칭

- **객체**는 추상화 뒤로 자료를 숨긴 채 자료를 다루는 함수만 공개한다.
  - 기존 함수를 변경하지 않으면서 새 클래스를 추가하기 쉽다.
  - 객체 지향 코드는 새로운 함수를 추가하기 어렵다. 그러려면 모든 클래스를 고쳐야 한다.
- **자료 구조**는 자료를 그대로 공개하며 별다른 함수를 제공하지 않는다.
  - 자료 구조를 사용하는 절차적인 코드는 기존 자료 구조를 변경하지 않으면서 새 함수를 추가하기 쉽다.
  - 절차적인 코드는 새로운 자료 구조를 추가하기 어렵다. 그러려면 모든 함수를 고쳐야 한다.
- 두 정의는 본질적으로 정반대의 개념이다.
- 상황에 따라 **클래스 & 객체 지향 기법**을 사용하거나 or **절차적인 코드 & 자료 구조**를 적절하게 사용하는 것이 좋다.

<br>

### 3. 디미터 법칙

- 디미터 법칙이란
  - 휴리스틱(heuristic) - 경험에 기반하여 문제를 해결, 학습, 발견해 내는 방법
  - **모듈은 자신이 조작하는 객체의 속사정을 몰라야 한다**는 법칙

#### 기차 충돌

- 다음과 같은 코드를 기차 충돌 train wreck 이라고 부른다.

```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

- 여러 객체가 한 줄로 이어진 기차로 보이기 때문이다. 일반적으로 이와 같은 방식은 조잡하다 여기지므로 피하는 편이 좋다. 위 코드는 아래와 같이 나누는 편이 좋다. 

```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

- 위 예제가 객체라면, 내부 구조를 숨겨야 하므로 디미터 법칙을 위반한다.
- 반면, 자료 구조라면 내부 구조를 노출하므로 문제되지 않는다.

#### 잡종 구조

- 절반은 객체, 절반은 자료 구조인 잡종 구조가 나온다.
- 이러한 구조는 양쪽(객체/자료구조) 세상의 단점만 모아놓은 구조이다.
- 프로그래머가 함수나 타입을 보호할지, 공개할지 확신하지 못해서 어중간하게 설계한 것이다.

#### 구조체 감추기

<br>

### 4. 자료 전달 객체

- 자료 구조체의 전형적인 형태는 공개 변수만 있고 함수가 없는 클래스이다.
- 이를 때로는, 자료 전달 객체 (Data Transfer Object, DTO)라고 한다.

```java
public class Address { 
  public String street; 
  public String streetExtra; 
  public String city; 
  public String state; 
  public String zip;
}
```

#### 활성 레코드

- DTO의 특수한 형태이다. 활성 레코드는 DB 테이블이나 다른 소스에서 자료를 직접 변환한 결과이다.
- 활성레코드에 비즈니스 규칙 메서드를 추가해서 이러한 자료 구조를 객체로 취급하는 개발자가 흔하다. 하지만 이럴 경우, 잡종 구조가 나오게 된다.
- 해결방법은, **활성레코드를 자료구조로 취급하는 것**이다. 비즈니스 규칙을 담으면서 내부 자료를 숨기는 객체를 따로 생성한다.
