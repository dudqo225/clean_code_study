# Chapter 4. Comments

주석은 필요악이다. 주석 없이 코드를 표현할 방법이 없어서 할 수 없이 주석을 사용하는 것이다.

코드는 유지보수 할 수 있어도, 주석을 계속 유지보수하는 것은 현실적으로 어렵다.

<br>

### 목차

> 1. 주석은 나쁜 코드를 보완하지 못한다
> 2. 코드로 의도를 표현하라!
> 3. 좋은 주석
>    1. 법적인 주석
>    2. 정보를 제공하는 주석
>    3. 의도를 설명하는 주석
>    4. 의미를 명료하게 밝히는 주석
>    5. 결과를 경고하는 주석
>    6. TODO 주석
>    7. 중요성을 강조하는 주석
>    8. 공개 API에서 Javadocs
> 4. 나쁜 주석
>    1. 주절거리는 주석
>    2. 같은 이야기를 중복하는 주석
>    3. 오해할 여지가 있는 주석
>    4. 의무적으로 다는 주석
>    5. 이력을 기록하는 주석
>    6. 있으나 마나 한 주석
>    7. 무서운 잡음
>    8. 함수나 변수로 표현할 수 있다면 주석을 달지 마라
>    9. 위치를 표시하는 주석
>    10. 닫는 괄호에 다는 주석
>    11. 공로를 돌리거나 저자를 표시하는 주석
>    12. 주석으로 처리한 코드
>    13. HTML 주석
>    14. 전역 정보
>    15. 너무 많은 정보
>    16. 모호한 관계
>    17. 함수 헤더
>    18. 비공개 코드에서 Javadocs
>    19. 예제

<br>

### 1. 주석은 나쁜 코드를 보완하지 못한다

- 코드에 주석을 추가하는 일반적인 이유
  - 코드의 품질이 나빠서
- 깔끔하고 주석이 없는 코드가, 복잡하고 어수선하고 주석이 많은 코드보다 훨씬 좋다.
- 주석을 설명하려 애쓰지 말고, 난장판인 주석을 깨끗이 치우고 지우는 것에 시간을 써라!

<br>

### 2. 코드로 의도를 표현하라!

```python
if (employee.isEligibleForFullBenefits())
```

- 주석 없이도 함수 이름만으로 충분히 코드를 표현하였다.

<br>

### 3. 좋은 주석

#### 법적인 주석

- 각 소스 파일 첫머리에 들어가는 저작권 정보와 소유권 정보 등

```
// Copyright (C) 2003, 2004, 2005 by Object Montor, Inc. All right reserved.
```

#### 정보를 제공하는 주석

```
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
```

#### 의도를 설명하는 주석

#### 의미를 명료하게 밝히는 주석

#### 결과를 경고하는 주석

#### TODO 주석

- TODO 주석은 프로그래머에게 필요하다 여기지만 당장 구현하기 어려운 업무를 기술한다. 필요 없는 기능을 삭제하라는 알림, 더 좋은 이름을 떠올려달라는 부탁 등에 유용하게 사용 가능.

#### 중요성을 강조하는 주석

#### 공개 API에서 Javadocs

- 공개 API를 구현한다면 반드시 Javadocs를 작성할 것을 추천한다.
- 하지만 Javadocs가 독자를 오도하고, 잘못된 정보를 전달할 가능성이 있다는 것을 잊으면 안된다.

<br>

### 4. 나쁜 주석

- 대다수의 주석이 이 범주에 속한다.
- 일반적으로 대부분의 주석이 허술한 코드를 지탱하고, 엉성한 코드를 변명하거나 미숙한 결정을 합리화한다.

#### 주절거리는 주석

- 특별한 이유 없이 달리는 주석

```
public void loadProperties() {
    try {
        String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
        FileInputStream propertiesStream = new FileInputStream(propertiesPath);
        loadedProperties.load(propertiesStream);
    } catch (IOException e) {
        // 속성 파일이 없다면 기본값을 모두 메모리로 읽어 들였다는 의미다. 
    }
}
```

- 위의 catch 블록에 있는주석의 의미를 알아내려면 다른 코드를 뒤져봐야 한다. 이해가 안되서 다른 모듈을 찾아봐야하는 주석은 제대로 된 주석이 아니다.

#### 같은 이야기를 중복하는 주석

- 코드 내용을 그대로 중복하는 주석. 전혀 필요없다.

#### 오해할 여지가 있는 주석

#### 의무적으로 다는 주석

#### 이력을 기록하는 주석

- 소스 코드 관리 시스템이 있기때문에 전혀 필요없다.

#### 있으나 마나 한 주석

#### 무서운 잡음

#### 함수나 변수로 표현할 수 있다면 주석을 달지 마라

```
// 전역 목록 <smodule>에 속하는 모듈이 우리가 속한 하위 시스템에 의존하는가?
if (module.getDependSubsystems().contains(subSysMod.getSubSystem()))
```

- 주석을 제거하고 다시 표현하면 아래와 같다.

```
ArrayList moduleDependencies = smodule.getDependSubSystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```

#### 위치를 표시하는 주석

#### 닫는 괄호에 다는 주석

#### 공로를 돌리거나 저자를 표시하는 주석

#### 주석으로 처리한 코드

#### HTML 주석

#### 전역 정보

#### 너무 많은 정보

#### 모호한 관계

#### 함수 헤더

#### 비공개 코드에서 Javadocs

- 공개하지 않을 코드는 Javadocs가 필요없다.
