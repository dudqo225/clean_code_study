# Chapter 7. Error Handling

오류 처리(Error Handling)는 중요하다. 하지만 로직을 헷갈리고 애매하게 한다면, 잘못된 것이다. 

<br>

### 목차

> 1. Return 코드 대신 Exceptions을 사용해라
> 2. Try-Catch-Finally 구문을 먼저 작성해라
> 3. Unchecked Exceptions를 사용해라
> 4. Exceptions로 의미를 제공해라
> 5. 호출자(Caller)를 고려해서 Exceptions 클래스를 정의하라
> 6. 정상 흐름을 정의하라
> 7. null을 반환하지 마라
> 8. null을 전달하지 마라

<br>

### 1. Return 코드 대신 Exceptions을 사용해라

- 과거에 많은 프로그래밍 언어는 exceptions 기능이 없었다. 오류를 처리하고 다루는 것이 제한적이었음.
- eror flag를 set하거나 error code를 반환해야 했다.

→ caller가 코드 호출 후에 바로 에러를 체크해야 하지만, 잊어버리기 쉽다!

- **exception을 사용하는 것이 훨씬 쉽고 좋다.**

<br>

### 2. Try-Catch-Finally 구문을 먼저 작성해라

- 예외처리를 통해서 scope의 정의가 가능하다. (???)
- catch는 try문에서 발생되는 일에 관계없이 프로그램이 일관적인 상태를 유지하도록 한다.

<br>

### 3. Unchecked Exceptions를 사용해라

- Checked Exceptions ? Unchecked Exceptions ?
- Checked 예외처리를 사용하는 것이 그만큼 가치있고 이익이 되는지 생각해보아야 한다.
- ex.
  - 하나의 메서드 안에서 checked exceptions을 사용하고
  - catch는 세 단계 위에 있다면
  - 메서드와 catch 사이의 모든 부분에서 exception을 선언해야 한다.
- 대부분의 경우 checked exceptions는 비용이 이익보다 크다.

<br>

### 4. Exceptions로 의미를 제공해라

- error에 대한 정보를 담고 있는 메시지를 작성할 것.

<br>

### 5. 호출자(Caller)를 고려해서 Exceptions 클래스를 정의하라

- Exceptions 클래스를 정의할 때 가장 중요한 부분은 '어떻게 예외를 catch할 것인가'이다.
- 써드파티 API를 활용하여 wrapping하는 것이 유용할 것이다.
- 일반적으로 특정 부분의 코드는 하나의 exception으로 예외처리를 할 수 있다.
- 하나의 exception을 처리하고 다시 throw 할 경우 또다른 exception 클래스를 만들자.

<br>

### 6. 정상 흐름을 정의하라

- 보통 위에서 봤던 여러가지 방식들(외부 API를 통해 하나의 예외처리를 할 수도 있고, 코드 윗 부분에 handler를 정의하여)을 통해서 오류를 처리할 수 있을 것이다.
- Special Case가 발생할 경우 코드가 더러워질 수 있고, 이런 경우 SPECIAL CASE PATTERN을 사용해라.
  - 예외적인 상황을 신경쓰지 않아도 되며
  - 예외상황은 special case의 object 안에 캡슐화된다.

<br>

### 7. null을 반환하지 마라

- null을 리턴해야 할 경우 Special Case Object를 리턴해라.
- 써드파티 라이브러리에서 null을 리턴해야 할 경우 Exception을 throw하거나 Special Case Object를 리턴하는 메서드로 wrapping해라.
- <br>

### 8. null을 전달하지 마라

- null을 리턴하는 것은 나쁘지만, null을 메서드로 넘기는 것은 더 나쁘다.
- null을 argument로 활용해야 하는 API를 사용하는 경우가 아니면, null을 전달하지 마라.
- 대부분의 프로그래밍 언어에는 null을 처리하는 적절한 방법이 없다.
- 합리적인 접근법은 **null을 전달하는 것 자체를 금지**하는 것이다.
