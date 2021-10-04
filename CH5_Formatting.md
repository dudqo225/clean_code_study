# Chapter 5. Formatting

질서정연하면서 깔끔하고, 일관적인 코드가 사람들에게 전문가가 짰다는 인상을 심어줄 것이다. 반대로 코드가 어수선해보이면 무성의한 태도롤 코도를 작성했다고 생각할 것이다.

<br>

### 목차

> 1. 형식을 맞추는 목적
> 2. 적절한 행 길이를 유지하라
>    1. 신문 기사처럼 작성하라
>    2. 개념은 빈 행으로 분리하라
>    3. 세로 밀집도
>    4. 수직 거리
>    5. 세로 순서
> 3. 가로 형식 맞추기
>    1. 가로 공백과 밀집도
>    2. 가로 정렬
>    3. 들여쓰기
>    4. 가짜 범위
> 4. 팀 규칙
> 5. 밥 아저씨의 형식 규칙

<br>

### 1. 형식을 맞추는 목적

- 코드 형식을 맞추는 것은 매우 중요하다.
- 코드 형식(Format)은 의사소통의 일환이고, 의사소통은 전문 개발자의 일차적인 의무이다.

- 오늘 구현한 코드의 스타일, 가독성 수준은 유지보수의 용이성과 확정성에 영향을 미친다.

<br>

### 2. 적절한 행 길이를 유지하라

- 500줄을 넘기지 않고 대부분 200줄 정도인 파일로 커다란 시스템을 구축할 수 있다.
- 코드 길이를 200줄로 제한하는 것이 반드시 지켜야할 엄격한 규칙은 아니지만, 일반적으로 큰 파일보단 작은 파일이 이해하기 쉽다.

<br>

#### 신문 기사처럼 작성하라

- 좋은 신문 기사란
  - 최상단에 표제(기사 내용을 요약하는 문구)
  - 첫 문단에 전체 기사 내용을 요약
  - 기사를 읽어가면서 세부사항이 나오게 됨
- 소스파일 이름(표제)은 간단하고 설명 가능하게 지어서 이름만 보고도 올바른 모듈을 보고있는지 판단할 수 있도록 한다.
- 소스파일 첫 부분(요약 내용)은 고차원의 개념과 알고리즘을 설명
- 코드 아래로 내려갈수록 의도를 세세하게 묘사하고, 마지막에는 가장 저차원의 함수와 세부 내역이 나온다.

#### 개념은 빈 행으로 분리하라

- 코드의 각 줄은 수식 또는 절을 나타내고 여러 줄의 묶음은 하나의 완결된 생각을 표현한다.
- 생각 사이에는 빈 행을 넣어서 분리해야 한다. 그렇지 않으면 가독성이 떨어진다.

#### 세로 밀집도

- 줄바꿈이 개념을 분리한다면,
- 세로 밀집도는 연관성을 의미한다.
- 서로 밀집한/관련 있는 코드 행은 세로로 가까이 놓여야 한다.

#### 수직 거리

- 서로 밀접한 개념은 세로로 가까이 두어야 한다.
- 변수 선언
  - 변수는 사용하는 위치에서 최대한 가까이 선언한다.
- 인스턴스 변수
  - 인스턴스 변수는 클래스 맨 처음에 선언(Java의 경우)
  - 변수 간 세로로 거리를 두지 않는다.
  - C++의 경우에는 마지막에 선언하는 것이 일반적
- 종속 함수
  - 한 함수가 다른 함수를 호출한다면, 두 함수는 세로로 가까이 배치한다.
  - 가능하면 호출되는 함수를 호출하는 함수보다 뒤에 배치한다.
- 개념의 유사성
  - 개념적인 친화도가 높을수록 코드를 서로 가까이 배치

#### 세로 순서

- 호출되는 함수를 호출하는 함수보다 뒤에 배치한다.
- 그러면 코드가 자연스럽게 고차원 > 저차원으로 내려간다.
- 가장 중요한 개념을 먼저 표현하고, 세세한 사항을 마지막에 표현 (두괄식)

<br>

### 3. 가로 형식 맞추기

- 대부분의 프로그래머들은 짧은 행을 선호한다.
- Hollerith가 제안한 80자 제한은 다소 인위적이므로 더 늘여도 되지만, 120자 이상을 넘어가는 것은 주의하자.

#### 가로 공백과 밀집도

- 가로로 공백을 사용하여 밀접 or 느슨한 개념을 표현한다.
- 연산자의 우선순위를 강조하기 위해서도 공백을 사용

#### 가로 정렬

```java
public class FitNesseExpediter implements ResponseSender {
	private		Socket		  	socket;
	private 	InputStream 	input;
	private 	OutputStream    output;
	private 	Reques		  	request; 		
	private 	Response 	  	response;	
	private 	FitNesseContex	context; 
	protected 	long		  	requestParsingTimeLimit;
	private 	long		  	requestProgress;
	private 	long		  	requestParsingDeadline;
	private 	boolean		  	hasError;
	
	... 
```

- 보기에 깔끔해 보일 수도 있지만, 코드가 엉뚱한 부분을 강조해서 변수의 유형은 자연스레 무시되고 이름부터 읽게 됨
- 선언문과 할당문을 별도로 정렬할 필요 X 

#### 들여쓰기

- 들여쓰기를 잘 해놓으면 구조가 한 눈에 들어온다. (가독성)

> 애초에 들여쓰기를 잘 안하면 코드가 작동안하는 경우도 생기지 않나...?

#### 가짜 범위

- 빈 while 문 혹은 for문을 접할 때가 있다. 가능한한 이런 경우는 피해야 하지만 그러지 못할 경우에는 빈 블록을 올바로 들여쓰고 괄호로 감싸라.

<br>

### 4. 팀 규칙

- 팀에 속해있다면, 가장 우선시 되어야 할 것은 팀 규칙이다.
- 처음 코딩을 시작하기 전, 코딩 스타일을 의논해서 IDE Formatter로 지정하여 구현하는 것이 올바른 방식이다.

<br>

### 5. 밥 아저씨의 형식 규칙

- Clean Code 저자가 사용하는 규칙이 명확히 드러나는 코드

```java
public class CodeAnalyzer implements JavaFileAnalysis { 
	private int lineCount;
	private int maxLineWidth;
	private int widestLineNumber;
	private LineWidthHistogram lineWidthHistogram; 
	private int totalChars;
	
	public CodeAnalyzer() {
		lineWidthHistogram = new LineWidthHistogram();
	}
	
	public static List<File> findJavaFiles(File parentDirectory) { 
		List<File> files = new ArrayList<File>(); 
		findJavaFiles(parentDirectory, files);
		return files;
	}
	
	private static void findJavaFiles(File parentDirectory, List<File> files) {
		for (File file : parentDirectory.listFiles()) {
			if (file.getName().endsWith(".java")) 
				files.add(file);
			else if (file.isDirectory()) 
				findJavaFiles(file, files);
		} 
	}
	
	public void analyzeFile(File javaFile) throws Exception { 
		BufferedReader br = new BufferedReader(new FileReader(javaFile)); 
		String line;
		while ((line = br.readLine()) != null)
			measureLine(line); 
	}
	
	private void measureLine(String line) { 
		lineCount++;
		int lineSize = line.length();
		totalChars += lineSize; 
		lineWidthHistogram.addLine(lineSize, lineCount);
		recordWidestLine(lineSize);
	}
	
	private void recordWidestLine(int lineSize) { 
		if (lineSize > maxLineWidth) {
			maxLineWidth = lineSize;
			widestLineNumber = lineCount; 
		}
	}

	public int getLineCount() { 
		return lineCount;
	}

	public int getMaxLineWidth() { 
		return maxLineWidth;
	}

	public int getWidestLineNumber() { 
		return widestLineNumber;
	}

	public LineWidthHistogram getLineWidthHistogram() {
		return lineWidthHistogram;
	}
	
	public double getMeanLineWidth() { 
		return (double)totalChars/lineCount;
	}

	public int getMedianLineWidth() {
		Integer[] sortedWidths = getSortedWidths(); 
		int cumulativeLineCount = 0;
		for (int width : sortedWidths) {
			cumulativeLineCount += lineCountForWidth(width); 
			if (cumulativeLineCount > lineCount/2)
				return width;
		}
		throw new Error("Cannot get here"); 
	}
	
	private int lineCountForWidth(int width) {
		return lineWidthHistogram.getLinesforWidth(width).size();
	}
	
	private Integer[] getSortedWidths() {
		Set<Integer> widths = lineWidthHistogram.getWidths(); 
		Integer[] sortedWidths = (widths.toArray(new Integer[0])); 
		Arrays.sort(sortedWidths);
		return sortedWidths;
	} 
}
```

