# Chapter 8. Boundaries



### 목차

> 1. 외부 코드 사용하기
> 2. 경계 살피고 익히기
> 3. log4j 익히기
> 4. 학습 테스트는 공짜 이상이다
> 5. 아직 존재하지 않는 코드를 사용하기
> 6. 깨끗한 경계

<br>

### 1. 외부 코드 사용하기

- 인터페이스를 제공하는 Provider와 사용하는 User 사이에는 긴장감(tension)이 존재한다.
- Provider는 좀 더 다양한 환경에서 많은 사용자가 사용할 수 있도록 넓은 사용성(broad applicability)을 지향한다.
- 반면 User는 그들의 Needs에 알맞는 인터페이스를 원한다.
- 이를 "경계에서의 긴장" 이라고 한다.



<br>

### 2. 경계 살피고 익히기

- 서드파티 코드를 사용할 때, 우리는 사용할 코드에 대해서 테스트할 필요가 있다.
- learning tests를 통해서 우리는 사용할 서드파티 API에 대해서 통제 가능한 실험을 해볼 수 있다. 

<br>

### 3. log4j 익히기

```java
    // 1.
    // log4j 라이브러리를 다운한다.
    // 고민 많이 하지 말고 본능에 따라 "hello"가 출력되길 바라면서 아래의 테스트 코드를 작성해보자.
    @Test
    public void testLogCreate() {
        Logger logger = Logger.getLogger("MyLogger");
        logger.info("hello");
    }

    // 2.
    // 위 테스트는 "Appender라는게 필요하다"는 에러 메시지를 출력한다.
    // 조금 더 읽어보니 ConsoleAppender라는게 있는걸 알아냈다.
    // 그래서 ConsoleAppender라는 객체를 만들어 넣어보았다.
    @Test
    public void testLogAddAppender() {
        Logger logger = Logger.getLogger("MyLogger");
        ConsoleAppender appender = new ConsoleAppender();
        logger.addAppender(appender);
        logger.info("hello");
    }

    // 3.
    // 위와 같이 하면 "Appender에 출력 스트림이 없다"고 한다.
    // 이상하다. 가지고 있는게 이성적일것 같은데...
    // 구글의 도움을 빌려, 다음과 같이 해보았다.
    @Test
    public void testLogAddAppender() {
        Logger logger = Logger.getLogger("MyLogger");
        logger.removeAllAppenders();
        logger.addAppender(new ConsoleAppender(
            new PatternLayout("%p %t %m%n"),
            ConsoleAppender.SYSTEM_OUT));
        logger.info("hello");
    }
    
    // 성공했다. 하지만 ConsoleAppender를 만들어놓고 ConsoleAppender.SYSTEM_OUT을 받는건 이상하다.
    // 그래서 빼봤더니 잘 돌아간다.
    // 하지만 PatternLayout을 제거하니 돌아가지 않는다.
    // 그래서 문서를 살펴봤더니 "ConsoleAppender의 기본 생성자는 unconfigured상태"란다.
    // 명백하지도 않고 실용적이지도 않다. 버그이거나, 적어도 "일관적이지 않다"고 느껴진다.
```

```java
	// 조금 더 구글링, 문서 읽기, 테스트를 거쳐 log4j의 동작법을 알아냈고 그것을 간단한 유닛테스트로 기록했다.
	// 이제 이 지식을 기반으로 log4j를 래핑하는 클래스를 만들수 있다.
	// 나머지 코드에서는 log4j의 동작원리에 대해 알 필요가 없게 됐다.

	public class LogTest {
        private Logger logger;

        @Before
        public void initialize() {
            logger = Logger.getLogger("logger");
            logger.removeAllAppenders();
            Logger.getRootLogger().removeAllAppenders();
        }

        @Test
        public void basicLogger() {
            BasicConfigurator.configure();
            logger.info("basicLogger");
        }

        @Test
        public void addAppenderWithStream() {
            logger.addAppender(new ConsoleAppender(
                new PatternLayout("%p %t %m%n"),
                ConsoleAppender.SYSTEM_OUT));
            logger.info("addAppenderWithStream");
        }

        @Test
        public void addAppenderWithoutStream() {
            logger.addAppender(new ConsoleAppender(
                new PatternLayout("%p %t %m%n")));
            logger.info("addAppenderWithoutStream");
        }
    }
```



<br>

### 4. 학습 테스트는 공짜 이상이다

- learning tests는 돈이 들지 않는다. 
- 써드파티 API에 대한 우리의 이해를 높일 수있는 훌륭하고 정확한 실험이다.
- 써드파티 코드가 바뀔 경우 Learning test를 돌려 "아직 우리가 필요한 기능이 잘 동작하는지" 테스트할 수 있다.

<br>

### 5. 아직 존재하지 않는 코드를 사용하기

- 아직 개발되지 않은 모듈이 필요하지만, 기능은 커녕 인터페이스조차 구현되지 않은 경우가 있을 수 있다.
- ex.
  - 무선 통신 시스템을 구축하는 프로젝트가 진행중이었다.
  - 팀의 하위 팀으로 '송신기'를 담당하는 팀이 있었는데 나머지 팀원들이 송신기에 대한 지식이 전혀 없었다.
  - '송신기' 팀은 인터페이스를 제공하지 않았고, 저자는 '송신기' 팀을 기다리는 대신 원하는 기능을 정의하고 인터페이스를 만들었다.
  - 인터페이스를 스스로 정의함으로써 메인 로직을 깔끔하게 짤 수 있었고 목표를 명확하게 나타낼 수 있었다.

<br>

### 6. 깨끗한 경계

- 좋은 SW 디자인이란, 변경이 생길 경우 많은 재작업 없이 변경을 반영할 수 있는 디자인이다.
- 경계의 코드는 명확한 분리와 테스트가 필요하다. 내부 코드가 써드파티 코드에 대해서 알지 못하게 해야 한다.

- Map 객체를 래핑하거나 Adapter를 사용하여 최상의 인터페이스를 변경하든, 코드는 보기 편해지고 경계 인터페이스를 일관적으로 사용할 수 있게 해주며 써드파티 코드의 변경에도 유연하게 대응할 수 있게 해준다.
