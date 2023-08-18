# Google Java Style Guide

> 이 문서는 Google Java Style Guide를 번역하며 정리한 문서입니다. 약간의 의역이 섞여 있을 수 있지만 본 의도는 해치지 않습니다.

원문 주소 : https://google.github.io/styleguide/javaguide.html

---

<details markdown="1">
  <summary>Table of Contents</summary>

- [1 개요](#s1-introduction)
    * [1.1 용어 설명](#s1-1-terminology-notes)
    * [1.2 안내 사항](#s1-2-guide-notes)
- [2 소스 파일 기본](#s2-source-file-basics)
    * [2.1 파일 이름](#s2-1-file-name)
    * [2.2 파일 인코딩](#s2-2-file-encoding)
    * [2.3 특수 문자](#s2-3-special-characters)
        + [2.3.1 공백 문자](#s2-3-1-whitespace-characters)
        + [2.3.2 특수 이스케이프 문자들](#s2-3-2-special-escape-sequences)
        + [2.3.3 Non-ASCII 문자들](#s2-3-3-non-ascii-characters)
- [3 소스 파일 구조](#s3-source-file-structure)
    * [3.1 라이센스 또는 저작권 정보](s3-1-license-or-copyright-information)
    * [3.2 Package 구문](s3-2-pcckage-statement)
    * [3.3 Import 구문](s3-3-import-statement)
        + [3.3.1 와일드 카드 가져오지 않기](#s3-3-1-no-widcard-imports)
        + [3.3.2 줄바꿈 하지 않기](#s3-3-2-no-line-wrapping)
        + [3.3.3 순서와 공간](#s3-3-3-ordering-and-spacing)
        + [3.3.4 클래스에 대한 정적 가져오기 없음](#s3-3-4-no-static-import-for-classes)
    * [3.4 Class 선언](s3-4-class-declaration)
        + [3.4.1 하나의 최상위 클래스 선언](#s3-4-1-exactly-one-top-level-class-declaration)
        + [3.4.2 클래스 본문 순서](#s3-4-2-ordering-of-class-contents)
            + [3.4.2.1 오버로드: 분할하지 않음](#s3-4-2-1-overloads)
- [4 서식](s4-formatting)
    * [4-1 중괄호](#s4-1-braces)
        + [4.1.1 선택적 중괄호 사용](#s4-1-1-use-of-optional-braces)
        + [4.1.2 비어있지 않은 블럭: K & R 스타일](#s4-1-2-nonempty-blocks)
        + [4.1.3 빈 블럭들: 간결할 수 있습니다.](#s4-1-3-empty-blocks)
    * [4-2 블럭 들여쓰기](#s4-2-block-indentation)
    * [4-3 한 줄에 하나의 문장](#s4-3-one-statement-per-line)
    * [4-4 열 제한](#s4-4-column-limit)
    * [4-5 줄 바꿈](#s4-5-line-wrapping)
        + [4.5.1 줄바꿈 위치](#s4-5-1-where-to-break)
        + [4.5.2 최소 +4칸의 연속 줄 들여쓰기](#s4-5-2-indent-continuation-lines-at-least)
    * [4-6 공백](#s4-6-whitespace)
        + [4.6.1 세로 공백](#s4-6-1-vertical-whitespace)
        + [4.6.2 수평 공백](#s4-6-2-horizontal-whitespace)
        + [4.6.3 수평 정렬](#s4-6-3-horizontal-alignment)
    * [4-7 괄호 그룹화](#s4-7-grouping-parentheses)
    * [4-8 특별한 구조](#s4-8-specific-constructs)
        + [4.8.1 열거형 클래스](#s4-8-1-enum-classes)
        + [4.8.2 변수 선언](#s4-8-2-variable-declarations)
            + [4.8.2.1 정의당 하나의 변수](#s4-8-2-1-one-variable-per-declaration)
            + [4.8.2.2 필요할 때 선언](#s4-8-2-2-declared-when-needed)
        + [4.8.3 배열](#s4-8-3-arrays)
            + [4.8.3.1 배열 초기화](#s4-8-3-1-array-initializers)
            + [4.8.3.2 C 스타일의 배열 선언문은 쓰지 말것](#s4-8-3-2-no-c-style-array-declarations)
        + [4.8.4 Switch 구문](#s4-8-4-switch-statements)
            + [4.8.4.1 들여쓰기](#s4-8-4-1-indentation)
            + [4.8.4.2 통과: 주석 처리됨](#s4-8-4-2-fall-through)
            + [4.8.4.3 default 레이블 존재](#s4-8-4-3-presence-of-the-default-label)
        + [4.8.5 Annotations](#s4-8-5-annotations)
            + [4.8.5.1 Type-use 어노테이션](#s4-8-5-1-type-use-annotations)
            + [4.8.5.2 Class 어노테이션](#s4-8-5-2-class-annotations)
            + [4.8.5.3 메소드 및 생성자 어노테이션](#s4-8-5-3-method-and-constructor-annotations)
            + [4.8.5.4 Field 어노테이션](#s4-8-5-4-field-annotations)
        + [4.8.6 주석](#s4-8-6-comments)
            + [4.8.6.1 Field 어노테이션](#s4-8-6-1-block-comment-style)
        + [4.8.7 접근 제한자](#s4-8-7-modifers)
        + [4.8.8 숫자 리터럴](#s4-8-8-numeric-literals)
- [5 네이밍](#s5-naming)
    * [5-1 모든 식벽자의 공통 규칙](#s5-1-rules-common-to-all-identifiers)
    * [5-2 식별자 타입에 대한 규칙](#s5-2-rules-by-identifier-type)
        + [5.2.1 패키지 이름](#s5-2-1-package-names)
        + [5.2.2 클래스 이름](#s5-2-2-class-names)
        + [5.2.3 함수 이름](#s5-2-3-method-names)
        + [5.2.4 상수 이름](#s5-2-4-constant-names)
        + [5.2.5 비상수 이름](#s5-2-5-non-cnstant-filed-names)
        + [5.2.6 파라미터 이름](#s5-2-6-parameter-names)
        + [5.2.7 지역 변수 이름](#s5-2-7-local-variable-names)
        + [5.2.8 타입 변수 이름](#s5-2-8-type-variable-names)
    * [5-3 카멜 케이스](#s5-3-camel-case)
- [6 프로그래밍 적용](#s6-programming-practices)
    * [6-1 오버라이드](#s6-1-override)
    * [6-2 예외 잡기](#s6-2-caught-exceptions)
    * [6-3 정적 멤버](#s6-3-static-members)
    * [6-4 종료자](#s6-4-finalizers)
- [7 Javadoc](#s7-javadoc)
    * [7.1 서식](#s7-1-formatting)
        + [7.1.1 일반 형식](#s7-1-1-general-form)
        + [7.1.2 문단](#s7-1-2-paragraphs)
        + [7.1.3 블럭 태그](#s7-1-3-block-tags)
    * [7.2 요약](#s7-2-the-summary-fragment)
    * [7.3 Javadoc이 사용되는 곳](#s7-3-where-javadoc-is-used)
        + [7.3.1 예외: 함수 설명](#s7-3-1-exception-self-explanatory-members)
        + [7.3.2 예외: 오버라이드](#s7-3-2-exception-overrides)
    * [7.4 ](#s7-4-non-required-javadoc)

</details>


<a id="s1-introduction"></a>

## 1. 개요

이 문서는 Java™ 프로그래밍 언어의 소스 코드에 대한 Google 코딩 표준의 완전한 정의 역할을 합니다. Java 소스 파일은 여기의 규칙을 준수하는 경우에만 Google 스타일에 있는 것으로 설명됩니다.

다른 프로그래밍 스타일 가이드와 마찬가지로, 다루는 문제는 서식 지정의 미적 문제뿐만 아니라 다른 유형의 규칙 또는 코딩 표준도 포함합니다. 그러나 이 문서는 주로 우리가 보편적으로 따르는 엄격한 규칙 에 초점을
맞추고 명확하게 시행할 수 없는(사람이나 도구로) 조언을 제공하지 않습니다

<a id="s1-1-terminology-notes"></a>

### 1.1 용어 설명

이 문서에는

1. class라는 용어는 "일반적인" 클래스, enum 클래스, 인터페이스 혹은 애노테이션 타입을 포괄하여 사용됩니다.
2. member(class의)라는 용어는 중첩 클래스, 필드, 메소드 혹은 생성자 즉, 초기화들과 주석들을 제외한 클래스의 모든 최상위 내용들을 포괄하여 사용됩니다.
3. comment라는 용어는 항상 구현 주석을 나타냅니다. 우리는 "documentation comments"라는 용어 대신에 "Javadoc"이라는 용어를 사용합니다.

<a id="s1-2-guide-notes"></a>

### 1.2 안내 사항

이 문서의 예제 코드는 비표준 입니다 . 즉, 예제는 Google 스타일로 되어 있지만 코드를 표현하는 유일한 스타일리쉬한 방법을 설명하지 않을 수 있습니다.

<a id="s2-source-file-basics"></a>

## 2. 소스 파일 기본

<a id="s2-1-file-name"></a>

### 2.1 파일 명

소스 파일들의 이름은 최상위 클래스들을 포함하는 대소문자를 구별하는 이름들로 되어 있고 `.java` 확장자로 구성됩니다.

<a id="s2-2-file-encoding"></a>

### 2.2 파일 인코딩: UTF-8

소스 파일은 UTF-8로 인코딩되어야 합니다.

<a id="s2-3-special-characters"></a>

### 2.3 특수 문자

<a id="s2-3-1-whitespace-characters"></a>

#### 2.3.1 공백 문자

줄 종결자 시퀀스를 제외하고 ASCII 수평 공백 문자 ( 0x20 )는 소스 파일의 모든 위치에 나타나는 유일한 공백 문자입니다.
이는 다음을 의미합니다.

- 문자열 및 문자 리터럴의 다른 모든 공백 문자는 이스케이프됩니다.
- 탭 문자는 들여쓰기에 사용되지 않습니다

<a id="s2-3-2-special-escape-sequences"></a>

#### 2.3.2. 특수 이스케이프 문자들

특수 이스케이프 문자들 (`\b`, `\t`, `\n`, `\f`, `\r`, `\"`, `\'` and `\\`)은 해당 옥텟(\012) 이나 유니코드(\u000a) 이스케이프 대신에 해당 문자가 사용됩니다.

<a id="s2-3-3-non-ascii-characters"></a>

#### 2.3.3 Non-ASCII 문자들

나머지 non-ASCII 문자들 중, 실제로 유니코드 문자 (e.g. `∞`) 인 혹은 유니코드와 동등한 이스케이프 문자 (e.g. `\u221e`) 이 사용됩니다.
비록, 유니 코드는 문자열 리터럴 밖에서 이스케이프되며 주석은 권장되지 않지만 선택은 코드를 읽고 이해하기 쉽게 만드는 것에 달려 있습니다

> 팁: 유니코드 이스케이프 사례에서 실제 유니코드 문자가 사용되는 경우에도 설명 주석이 매우 유용할 수 있습니다.

예시:

| Example                                                  | Discussion                                      |
|----------------------------------------------------------|:------------------------------------------------|
| `String unitAbbrev = "μs";`                              | 최적: 주석 없이도 명확합니다.                               |
| `String unitAbbrev = "\u03bcs"; // "μs"`                 | 허용되지만 그렇게 할 이유가 없습니다.                           |
| `String unitAbbrev = "\u03bcs"; // Greek letter mu, "s"` | 허용되지만 어색하고 실수하기 쉽습니다.                           |
| `String unitAbbrev = "\u03bcs";`                         | 나쁨: 독자는 이것이 무엇인지 전혀 모릅니다.                       |
| `return '\ufeff' + content; // byte order mark`          | 좋음: 출력할 수 없는 문자에 이스케이프를 사용하고 필요한 경우 주석을 추가합니다.. |

> 팁: 일부 프로그램이 ASCII가 아닌 문자를 제대로 처리하지 못할 수 있다는 두려움 때문에 코드를 읽기 어렵게 만들지 마십시오.
> 그런 일이 발생하면 해당 프로그램이 손상 되었으며 수정 해야 합니다.

<a id="s3-source-file-structure"></a>

## 3 소스 파일 구조

소스 파일은 다음 순서 로 구성됩니다.

1. 라이센스나 저작권 정보 (만약 있다면)
2. 패키지(Package) 구문
3. 임포트(Import) 구문
4. 정확히 하나의 최상위 클래스

<a id="s3-1-license-or-copyright-information"></a>

### 3.1 라이센스나 저작권 (만약 존제한다면)

라이센스 또는 저작권 정보가 파일에 속하는 경우 여기에 속합니다.

<a id="s3-2-pcckage-statement"></a>

### 3.2 Package 구문

패키지 문은 줄 바꿈되지 않습니다.
열 제한(섹션 4.4, 열 제한: 100 )은 패키지 문에 적용되지 않습니다.

<a id="s3-3-import-statement"></a>

### 3.3 Import 구문

<a id="s3-3-1-no-widcard-imports"></a>

#### 3.3.1 와일드 카드 가져오지 않기

정적이든 아니든 와일드카드 가져오기 는 사용되지 않습니다.

<a id="s3-3-2-no-line-wrapping"></a>

#### 3.3.2 줄바꿈 하지 않기

가져오기 문은 줄 바꿈되지 않습니다.
열 제한(섹션 4.4, 열 제한: 100 )은 import 문에 적용되지 않습니다.

<a id="s3-3-3-ordering-and-spacing"></a>

#### 3.3.3 순서와 공간

가져오기는 다음과 같이 주문됩니다.

1. 단일 블록의 모든 정적 가져오기.
2. 단일 블록의 모든 비정적 가져오기.

정적 및 비정적 가져오기가 모두 있는 경우 하나의 빈 줄이 두 블록을 구분합니다. import 문 사이에 다른 빈 줄이 없습니다.

각 블록 내에서 가져온 이름은 ASCII 정렬 순서로 나타납니다. ( 참고: 이것은 '.'이 ';'보다 먼저 정렬되기 때문에 ASCII 정렬 순서에 있는 import 문과 동일하지 않습니다 .)

<a id="s3-3-4-no-static-import-for-classes"></a>

#### 3.3.4 클래스에 대한 정적 가져오기 없음

적 가져오기는 정적 중첩 클래스에 사용되지 않습니다. 일반적인 import가 사용됩니다.

<a id="s3-4-class-declaration"></a>

### 3.4 클래스 선언

<a id="s3-4-1-exactly-one-top-level-class-declaration"></a>

#### 3.4.1 하나의 최상위 클래스 선언

각 최상위 클래스는 자체 소스 파일에 존재합니다.

<a id="s3-4-2-ordering-of-class-contents"></a>

#### 3.4.2 클래스 본문 순서

클래스의 멤버 및 이니셜라이저에 대해 선택한 순서는 학습 가능성에 큰 영향을 미칠 수 있습니다.
그러나 이를 수행하는 방법에 대한 하나의 올바른 레시피는 없습니다. 다른 클래스는 다른 방식으로 내용을 정렬할 수
있습니다.

중요한 것은 각 클래스가 논리적 순서를 사용 한다는 것입니다 . 요청 시 관리자가 설명할 수 있습니다.
예를 들어, 새로운 메서드는 클래스의 끝에 습관적으로 추가되는 것이 아닙니다. 논리적 순서가 아닌 "추가된
날짜별" 순서가 생성되기 때문입니다.

<a id=""></a>

##### 3.4.2.1 오버로드: 분할하지 않음

동일한 이름을 공유하는 클래스의 메서드는 중간에 다른 멤버가 없는 단일 연속 그룹에 나타납니다. 여러 생성자(항상 동일한 이름을 가짐)에도 동일하게 적용됩니다.
이 규칙은 메서드 간에 static 또는 private과 같은 수정자가 다른 경우에도 적용됩니다.

<a id="s4-formatting"></a>

## 4. 서식

용어 노트: block-like construct (블럭과 같은 구조, 괄호로 나타내어지는 구조를 의미)는 클래스, 함수, 생성자의 몸체를 나타낸다. 4.8.3.1에 나와있는 배열 초기화블럭은 블럭과 같은 구조로
간주될 수 있다.

<a id="s4-1-braces"></a>

### 4.1 중괄호

<a id="s4-1-1-use-of-optional-braces"></a>

#### 4.1.1 선택적 중괄호 사용

괄호는 `if`, `else`, `for`, `do`, `while` 구문에 쓰이는데 몸체가 없거나 한 줄의 구문에도 괄호가 사용됩니다.

<a id="s4-1-2-nonempty-blocks"></a>

#### 4.1.2 비어있지 않은 블럭: K & R 스타일

중괄호는 비어 있지 않은 블록 및 블록과 같은 구성 에 대해 Kernighan 및 Ritchie 스타일(" 이집트 대괄호 ") 을 따릅니다.

- 여는 괄호 앞에는 줄 바꿈이 없음
- 여는 괄호 다음에 줄 바꿈
- 닫는 괄호 전에 줄 바꿈
- 닫는 중괄호 뒤의 줄 바꿈은 해당 중괄호가 명령문을 종료하거나 메서드, 생성자 또는 명명된 클래스의 본문을 종료하는 경우에만 해당됩니다. 예를 들어 중괄호 뒤에 else 또는 쉼표가 오면 줄 바꿈이 없습니다.

예:

```java
return()->{
        while(condition()){
        method();
        }
        };

        return new MyClass(){
@Override public void method(){
        if(condition()){
        try{
        something();
        }catch(ProblemException e){
        recover();
        }
        }else if(otherCondition()){
        somethingElse();
        }else{
        lastThing();
        }
        {
        int x=foo();
        frob(x);
        }
        }
        };
```

<a id="s4-1-3-empty-blocks"></a>

#### 4.1.4 빈 블럭들: 간결할 수 있습니다.

빈 블록 또는 블록과 같은 구성은 K & R 스타일일 수 있습니다

예:

```java
    // This is acceptable
    void doNothing(){}

            // This is equally acceptable
            void doNothingElse(){
            }
```

```java
 // 허용되지 않음: 멀티 블럭 구문에서는 간결한 빈 블럭을 사용할 수 없음
    try{
            doSomething();
            }catch(Exception e){}
```

<a id="s4-2-block-indentation"></a>

### 4.2 블럭 들여쓰기: +2 스페이스

새 블록이나 블록과 유사한 구성이 열릴 때마다 들여쓰기가 두 칸씩 증가합니다. 블록이 끝나면 들여쓰기가 이전 들여쓰기 수준으로 돌아갑니다.
수준은 블록 전체의 코드와 주석 모두에 적용됩니다.

<a id="s4-3-one-statement-per-line"></a>

### 4.3 한 줄에 하나의 문장

각 명령문 다음에는 줄 바꿈이 옵니다.

<a id="s4-4-column-limit"></a>

### 4.4 열 제한: 100

Java 코드의 열 제한은 100자입니다. "문자"는 모든 유니코드 코드 포인트를 의미합니다. 아래에 명시된 경우를 제외하고 이 제한을 초과하는 줄은 4.5절 줄 바꿈 에서 설명한 대로 줄 바꿈해야 합니다.

> 각 유니코드 코드 포인트는 표시 너비가 더 크거나 작더라도 하나의 문자로 계산됩니다. 예를 들어 전각 문자를 사용하는 경우 이 규칙이 엄격하게 요구하는 위치보다 먼저 줄 바꿈을 선택할 수 있습니다.


예외:

1. 개행이 불가능한 경우 (예를들어, Javadoc의 긴 URL 혹은 긴 JSNI 메서드 레페런스)
2. `package` 나 `import` 구문들
3. 셸에 복사하여 붙여넣을 수 있는 주석의 명령줄.
4. 매우 긴 식별자는 드물게 호출되지만 열 제한을 초과할 수 있습니다

<a id="s4-5-line-wrapping"></a>

### 4.5 줄 바꿈

용어 참고: 합법적으로 한 줄을 차지할 수 있는 코드를 여러 줄로 나눌 때 이 활동을 줄 바꿈 이라고 합니다

모든 상황에서 줄바꿈하는 방법을 정확하게 보여주는 포괄적이고 결정론적인 공식은 없습니다 . 동일한 코드 조각을 줄 바꿈하는 몇 가지 유효한 방법이 있는 경우가 많습니다.

> 참고: 줄 바꿈을 하는 일반적인 이유는 열 제한을 초과하는 것을 방지하기 위한 것이지만 실제로는 열 제한에 맞는 코드라도 작성자의 재량에 따라 줄 바꿈 할 수 있습니다 .

> 팁: 메서드 또는 지역 변수를 추출하면 줄 바꿈 없이도 문제를 해결할 수 있습니다


<a id="s4-5-1-where-to-break"></a>

#### 4.5.1 줄바꿈 위치

줄 바꿈의 주요 지시어는 다음과 같습니다. 더 높은 구문 수준 에서 중단하는 것을 선호합니다.

1. 비할당 연산자 에서 줄이 끊어지면 기호 앞에 줄 바꿈이 옵니다
    - 점 구분 기호( .)
    - 메서드 참조의 두 콜론( ::)
    - 유형 바인딩의 앰퍼샌드( )<T extends Foo & Bar>
    - catch 블록의 파이프( ).catch (FooException | BarException e)
2. 대입 연산자 에서 줄이 끊기면 일반적으로 기호 뒤에 줄 바꿈이 오지만 어느 쪽이든 허용됩니다.
    - 이것은 향상된 for문의 "assignment-operator-like" 콜론에도 적용된다.
3. 메서드 또는 생성자 이름은 (뒤에 오는 여는 괄호( )에 연결된 상태로 유지됩니다.
4. 쉼표( ,)는 앞에 오는 토큰에 연결된 상태로 유지됩니다.
5. 람다의 본문이 중괄호가 없는 단일 식으로 구성된 경우 화살표 바로 뒤에 줄 바꿈이 올 수 있다는 점을 제외하고는 람다의 화살표 근처에서 줄이 끊어지지 않습니다
    ```java
    MyLambda<String, Long, Object> lambda =
       (String label, Long value, Object obj) -> {
           ...
       };

    Predicate<String> predicate = str ->
        longExpressionInvolving(str);
    ```

참고: 줄 바꿈의 목적은 깨끗한 코드를 만듦에 있지, 줄 수를 줄이는데 있지 않다.

<a id="s4-5-1-where-to-break"></a>

#### 4.5.2 최소 +4칸의 연속 줄 들여쓰기

줄바꿈을 할 때 첫 번째 줄 이후의 각 줄(각 연속 줄 )은 원래 줄에서 적어도 +4만큼 들여쓰기됩니다.

연속 줄이 여러 개 있는 경우 들여쓰기는 원하는 대로 +4 이상으로 다양할 수 있습니다. 일반적으로 두 개의 연속 행은 구문적으로 병렬 요소로 시작하는 경우에만 동일한 들여쓰기 수준을 사용합니다.

가로 정렬 에 대한 섹션 4.6.3은 특정 토큰을 이전 줄과 정렬하기 위해 가변적인 수의 공백을 사용하는 권장되지 않는 관행을 다룹니

<a id="s4-6-whitespace"></a>

### 4.6 공백

<a id="s4-6-1-vertical-whitespace"></a>

#### 4.6.1 세로 공백

1. 연속적인 멤버나 클래스의 초기화: 필드, 생성자, 메소드, 중첩 클래스, 정적 초기화 그리고 인스턴스 초기화
    - 예외: 두 개의 연속된 필드의 공백은 선택적입니다. 그러한 공백은 필드의 논리적 그룹을 형성하는데 필요하합니다.
    - 예외: enum 상수의 공백 줄은 4.8.1 절에서 다룹니다.
2. 문서의 다른 부분에서도 필요합니다.

예를 들어 코드를 논리적 하위 섹션으로 구성하기 위한 명령문 사이와 같이 가독성을 향상시키는 위치에 하나의 빈 줄이 나타날 수도 있습니다. 클래스의 첫 번째 멤버나 이니셜라이저 앞이나 클래스의 마지막 멤버나
이니셜라이저 뒤의 빈 줄은 권장되지도 권장되지도 않습니다.

여러 개의 연속된 빈 줄이 허용되지만 필수(또는 권장)는 아닙니다

<a id="s4-6-2-horizontal-whitespace"></a>

#### 4.6.1 수평 공백

언어 또는 기타 스타일 규칙에서 요구하는 위치를 넘어 리터럴, 주석 및 Javadoc과 별도로 단일 ASCII 공백도 다음 위치에만 나타 납니다 .

1. 예약어를 나누는 경우, if, for, catch 같은 예약어 이후 나오는 여는 괄호에서 사용
2. 예약어를 나누는 경우, else 나 catch 같은 예약어 이후 나오는 닫는 중괄호에서 사용
3. 중괄호는 여는 모든 경우에 사용, 예외 두가지
    - @SomeAnnotation({a, b})
    - String[][] x = {{"foo"}};
4. 이항 또는 삼항 연산자의 양쪽에 있습니다. 이는 다음과 같은 "operator-like" 기호에도 적용됩니다
    - <T extends Foo & Bar>  인접한 타입 바운딩의 앰퍼센드 연산자에서
    - catch (FooException | BarException e) 예외처리의 파이프 에서
    - `for` ("foreach") statement 향상된 for 문에서
    - `(String str) -> str.length()` 람다의 화살표에서  
      하지만
    - 메서드 참조의 두 콜론(::)은 다음과 같이 작성됩니다.Object::toString
    - 점 구분 기호( .)는 다음과 같이 작성됩니다. object.toString()
5. ',' ':' ';' 혹은 캐스팅 할때 닫는 괄호 뒤에서 사용
6. 내용과 주석을 시작하는 이중 슬래시('//') 사이에는 여러 공백이 허용됩니다.
7. 변수의 선언문 사이에서 List<String> list
8. 배열 선언문 사이에서 공백 선택
    - new int[] {5, 6}` and `new int[] { 5, 6 } 둘 다 가능
9. `type annotation` 및 '[]' 또는 `...` 사이 사용

이 규칙은 줄의 시작이나 끝에서 추가 공간을 요구하거나 금지하는 것으로 해석되지 않습니다.

<a id="s4-6-3-horizontal-alignment"></a>

#### 4.6.3 수평 정렬: 필요하지 않음

용어 참고 사항: 가로 정렬은 특정 토큰이 이전 줄의 다른 특정 토큰 바로 아래에 나타나도록 하기 위해 코드에 가변 개수의 추가 공백을 추가하는 방법입니다.

이 관행은 허용되지만 Google Style에서는 절대 요구하지 않습니다 . 이미 사용된 곳에서 수평 정렬을 유지할 필요조차 없습니다 .

다음은 정렬을 사용하지 않고 정렬을 사용하는 예입니다..

```java
private int x; // 괜찮음
private Color color; // 이것도 괜찮음

private int x;      // 허용된다, 나중에 고쳐야 함
private Color color;  // 맞춰지지 않은 상태로 둘 수도 있다
```

> 팁: 팁: 정렬은 가독성을 높일 수 있지만 향후 유지 관리에 문제를 일으킵니다. 한 줄만 터치해야 하는 미래의 변화를 고려하십시오. 이 변경으로 인해 이전에는 만족스러웠던 형식이 망가진 상태로 남을 수 있으며
> 이는 허용됩니다 . 더 자주 코더(아마도 당신)가 인근 줄의 공백을 조정하도록 프롬프트를 표시하여 계단식 일련의 재포맷을 트리거할 수 있습니다. 그 한 줄 변경에는 이제 "폭발 반경"이 있습니다. 이것은 최악의
> 경우
> 무의미한 바쁜 작업을 초래할 수 있지만 기껏해야 버전 기록 정보를 손상시키고 검토자의 속도를 늦추며 병합 충돌을 악화시킵니다.

<a id="s4-7-grouping-parentheses"></a>

### 4.7 괄호 그룹화

선택적 그룹화 괄호는 저자와 검토자가 괄호가 없으면 코드가 잘못 해석될 가능성이 없으며 코드를 더 쉽게 읽을 수 없다는 데 동의하는 경우에만 생략됩니다. 모든 독자가 전체 Java 연산자 우선 순위 테이블을 기억하고
있다고 가정하는 것은 합리적 이지 않습니다 .

<a id="s4-8-specific-constructs"></a>

### 4.8 특별한 구조

<a id="s4-8-1-enum-classes"></a>

#### 4.8.1  열거형 클래스

enum 상수 뒤에 오는 각 쉼표 뒤에는 줄 바꿈이 선택 사항입니다. 추가 빈 줄(보통 한 줄)도 허용됩니다. 이것은 한 가지 가능성입니다.

```java
private enum Answer {
    YES {
        @Override
        public String toString() {
            return "yes";
        }
    },

    NO,
    MAYBE
}
```

메서드가 없고 상수에 대한 문서가 없는 enum 클래스는 선택적으로 배열 이니셜라이저인 것처럼 형식을 지정할 수 있습니다

```java
private enum Suit {CLUBS, HEARTS, SPADES, DIAMONDS}
```

열거형 클래스는 클래스 이므로 클래스 형식화에 대한 다른 모든 규칙이 적용됩니다

<a id="s4-8-2-variable-declarations"></a>

#### 4.8.2 변수 선언

<a id="s4-8-2-1-one-variable-per-declaration"></a>

##### 4.8.2.1 정의당 하나의 변수

모든 변수 선언(필드 또는 로컬)은 하나의 변수만 선언합니다. `int a, b;`와 같은 선언은 사용되지 않습니다.

예외: for 루프의 헤더에는 여러 변수선언이 쓰일 수 있습니다.

<a id="s4-8-2-2-declared-when-needed"></a>

##### 4.8.2.2 필요할 때 선언

지역 변수는 컨테이닝 블록이나 블록과 같은 구성의 시작 부분에서 습관적으로 선언되지 않습니다 . 대신 지역 변수는 범위를 최소화하기 위해 (합리적인 범위 내에서) 처음 사용된 지점에 가깝게 선언됩니다. 지역 변수
선언에는 일반적으로 이니셜라이저가 있거나 선언 직후에 초기화됩니다.

<a id="s4-8-3-arrays"></a>

#### 4.8.3 배열

<a id="s4-8-3-1-array-initializers"></a>

##### 4.8.3.1 배열 초기화는 "block-like"

배열 이니셜라이저는 선택적으로 "블록과 같은 구성"인 것처럼 형식을 지정할 수 있습니다. 예를 들어, 다음은 모두 유효합니다.

```java
new int[]{
        0,1,2,3
        }
```

```java
new int[]{
        0,1,
        2,3,
        }
```

```java
new int[]{
        0,
        1.
        2,
        3,
        }
```

```java
new int[]
        {0,1,2,3,}
```

<a id="s4-8-3-2-no-c-style-array-declarations"></a>

##### 4.8.3.2 C 스타일의 배열 선언문은 쓰지 말것

대괄호는 변수가 아닌 타입에 사용됩니다.

```java
String args[] // no
        String[]args // yes
```

<a id="s4-8-4-switch-statements"></a>

#### 4.8.4 Switch 구문

용어 참고: Switch 블록 의 중괄호 안에는 하나 이상의 명령문 그룹이 있습니다.
각각의 그룹은 구문 이전에 한개 이상의 switch 라벨이 붙습니다. (case 혹은 default) (마지막 부분은 0개 이상의 구문)

<a id="s4-8-4-1-indentation"></a>

##### 4.8.4.1 들여쓰기

다른 블록과 마찬가지로 스위치 블록의 내용은 +2 들여쓰기됩니다.

스위치 레이블 다음에 줄바꿈이 있고 마치 블록이 열리는 것처럼 들여쓰기 수준이 +2 증가합니다. 다음 스위치 레이블은 마치 블록이 닫힌 것처럼 이전 들여쓰기 수준으로 돌아갑니다.

<a id="s4-8-4-2-fall-through"></a>

##### 4.8.4.2 통과: 주석 처리됨

Switch 블록 내에서 각 문 그룹은 갑자기 종료되거나(`break`, `continue` 또는 `throw 된 예외`) 실행이 다음 문 그룹으로 계속되거나 계속 될 수 있음을 나타내는 주석으로 표시됩니다.
통과라는 아이디어를 전달하는 모든 주석이면 충분합니다.
이 특수 주석은 스위치 블록의 마지막 명령문 그룹에 필요하지 않습니다.

```java
switch(input){
        case 1:
        case 2:
        prepareOneOrTwo();
        // fall through
        case 3:
        handleOneTwoOrThree();
        break;
default:
        handleLargeNumber(input);
        }
```

case 1: 이후에는 주석이 필요하지 않으며 문 그룹의 끝에서만 필요합니다.

<a id="s4-8-4-3-presence-of-the-default-label"></a>

##### 4.8.4.3 default 레이블 존재

각 switch 문에는 코드가 포함되어 있지 않더라도 `default`문이 포함되어 있습니다.

예외: enum 유형에 대한 switch 문은 해당 유형의 가능한 모든 값을 포함하는 명시적 사례를 포함하는 경우 기본 문 그룹을 생략할 수 있습니다.
이를 통해 IDE 또는 기타 정적 분석 도구는 사례가 누락된 경우 경고를 발행할 수 있습니다.

<a id="s4-8-5-annotations"></a>

#### 4.8.5 Annotations

<a id="s4-8-5-1-type-use-annotations"></a>

##### 4.8.5.1 Type-use 어노테이션

Type-use 어노테이션은 타입 바로 앞에 나타납니다.

```java
final @Nullable String name;

public @Nullable Person getPersonByName(String name);
```

<a id="s4-8-5-2-class-annotations"></a>

##### 4.8.5.2 Class 어노테이션

클래스에 적용되는 어노테이션은 문서 블록 바로 뒤에 나타나며 각 어노테이션은 자체 행에 나열됩니다(즉, 행당 하나의 주석).
이러한 줄 바꿈은 줄 바꿈(4.5절, 줄 바꿈)을 구성하지 않으므로 들여쓰기 수준이 증가하지 않습니다.

```java

@Deprecated
@CheckReturnValue
public final class Frozzler { ...
}
```

<a id="method-and-constructor-annotations"></a>

##### 4.8.5.2 메소드 및 생성자 어노테이션

메서드 및 생성자 선언에 대한 어노테이션 규칙은 이전 섹션과 동일합니다.

```java
@Deprecated
@Override
public String getNameIfPresent(){...}
```

<a id="s4-8-5-4-field-annotations"></a>

##### 4.8.5.3 Field 어노테이션

필드에 적용되는 어노테이션도 문서 블록 바로 뒤에 나타나지만 이 경우 여러 어노테이션(매개변수화 가능)이 같은 줄에 나열될 수 있습니다.

```java
@Partial @Mock DataLoader loader;
```

<a id="s4-8-6-comments"></a>

#### 4.8.6 주석

이 부분은 구현 주석에 대한 내용입니다.
Javadoc은 7절에에서 별도로 다룹니다.

모든 줄 바꿈 앞에는 임의의 공백과 구현 주석이 올 수 있습니다. 이러한 주석은 행을 공백이 아닌 것으로 렌더링합니다.

<a id="s4-8-6-1-block-comment-style"></a>

##### 4.8.6.1 블럭 주석 스타일

블럭 주석 스타일은 둘러 샇인 코드와 같은 들여쓰기 레벨을 가집니다.
`/* ... */` 이나 `// ...` 의 스타일을 가집니다.
여러 줄 주석의 경우 후속 줄은 이전 줄의 `*`와 정렬된 `*`로 시작해야 합니다.

```java
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```

주석은 별표 또는 기타 문자로 그려진 상자로 둘러싸이지 않습니다.

> 팁: 여러 줄의 주석을 작성할 때 문단 형식으로 re-wrap을 하고 싶으면 /* ... */ 의 형식으로 작성한다.
> 대부분 포매터들은 // ... 의 re-wrap을 지원하지 않는다.

<a id="s4-8-7-modifers"></a>

#### 4.8.7 접근 제한자

클래스 및 멤버 한정자가 있는 경우 Java 언어 사양에서 권장하는 순서대로 나타납니다.

```java
public protected private abstract default static final transient volatile synchronized native strictfp
```

<a id="s4-8-8-numeric-literals"></a>

#### 4.8.8 숫자 리터럴

긴 값 정수 리터럴은 대문자 L 접미사를 사용하며 소문자는 절대 사용하지 않습니다(숫자 1과의 혼동을 피하기 위해).
예를 들어 3000000000l이 아니라 3000000000L입니다.

<a id="s5-naming"></a>

## 5. 네이밍

<a id="s5-1-rules-common-to-all-identifiers"></a>

### 5.1 모든 식벽자의 공통 규칙

식별자는 ASCII 문자와 숫자만 사용하며 아래에 언급된 소수의 경우 밑줄을 사용합니다. 따라서 각각의 유효한 식별자 이름은 정규식 `\w+` 와 일치합니다.

Google Style에서는 특별한 접두사 또는 접미사를 사용하지 않습니다.
예를 들어 `name_`, `mName`, `s_name` 및 `kName`과 같은 이름은 Google 스타일이 아닙니다.

<a id="s5-2-rules-by-identifier-type"></a>

### 5.2 식별자 타입에 대한 규칙

<a id="s5-2-1-package-names"></a>

#### 5.2.1 패키지 이름

패키지 이름은 소문자와 숫자만 사용합니다(밑줄 없음)
연속된 단어는 단순히 함께 연결됩니다.
예를 들어 com.example.deepSpace 또는 com.example.deep_space가 아닌 com.example.deepspace입니다.

<a id="s5-2-2-class-names"></a>

#### 5.2.2 클래스 이름

클래스 이름은 UpperCamelCase로 작성됩니다.

클래스 이름은 일반적으로 명사 또는 명사구입니다.
예를 들어 Character 또는 ImmutableList입니다. 인터페이스 이름은 명사 또는 명사구(예: List)일 수도 있지만 때로는 대신 형용사 또는 형용사구(예: Readable)일 수도 있습니다.

주석 유형의 이름을 지정하기 위한 특정 규칙이나 잘 확립된 규칙이 없습니다.

테스트 클래스에는 Test로 끝나는 이름이 있습니다(예: HashIntegrationTest). 단일 클래스를 포함하는 경우 해당 이름은 해당 클래스의 이름에 Test를 더한 것입니다
(예: HashImplTest).

<a id="s5-2-3-method-names"></a>

#### 5.2.3 함수 이름

함수 이름은 lowerCamelCase로 작성됩니다.

함수 이름은 일반적으로 동사 또는 동사구입니다. 예를 들어, sendMessage 또는 stop.

밑줄은 이름의 논리적 구성 요소를 구분하기 위해 JUnit 테스트 메서드 이름에 나타날 수 있습니다. 각 구성 요소는 소문자로 작성됩니다(예: transferMoney_deductsFromSource). 테스트
방법의 이름을 지정하는 올바른 방법은 없습니다.

#### 5.2.4 상수 이름

상수 이름은 UPPER_SNAKE_CASE를 사용합니다. 모두 대문자이며 각 단어는 밑줄 하나로 구분됩니다. 그러나 상수란 정확히 무엇입니까?

상수는 내용이 완전히 변경 불가능하고 메서드에 부작용이 감지되지 않는 정적 최종 필드입니다. 예를 들면 프리미티브, 문자열, 변경할 수 없는 값 클래스 및 null로 설정된 모든 항목이 포함됩니다. 인스턴스의 관찰
가능한 상태가 변경될 수 있는 경우 이는 상수가 아닙니다. 개체를 절대 변경하지 않으려는 의도만으로는 충분하지 않습니다

이러한 이름은 일반적으로 명사 또는 명사구입니다

```java
// 상수
static final int NUMBER=5;
static final ImmutableList<String> NAMES=ImmutableList.of("Ed","Ann");
static final ImmutableMap<String, Integer> AGES=ImmutableMap.of("Ed",35,"Ann",32);
static final Joiner COMMA_JOINER=Joiner.on(','); // Joiner가 불변이기 때문
static final SomeMutableType[]EMPTY_ARRAY={};

enum SomeEnum {
    ENUM_CONSTANT
}

// 상수 아님
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap<String, SomeMutableType> mutableValues =
        ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```

<a id="s5-2-5-non-cnstant-filed-names"></a>

#### 5.2.5 비상수 이름

상수가 아닌 필드 이름은 (static 같은) lowerCamelCase로 작성합니다

이러한 이름들은 전형적으로 명사나 명사구입니다.

<a id="s5-2-6-parameter-names"></a>

#### 5.2.6 파라미터 이름

파라미터 이름은 lowerCamelCase 입니다.

public 메서드에서 한개의 문자를 가진 파라미터는 피해야 합니다.

<a id="s5-2-7-local-variable-names"></a>

#### 5.2.7 지역 변수 이름

지역변수는 lowerCamelCase 입니다.

최종적이고 변경할 수 없는 경우에도 지역 변수는 상수로 간주되지 않으며 상수로 스타일을 지정하면 안 됩니다.

<a id="s5-2-8-type-variable-names"></a>

#### 5.2.8 타입 변수 이름

각 타입들은 두 스타일중 하나를 따릅니다.

- 하나의 대문자, 혹은 뒤에 하나의 숫자가 따라올 수 있다. (예를들어, E, T, X, T2)
- 클래스를 위해서 사용되는 (5.2.2절 클래스 이름 참조) 이름의 형식에 T 대문자가 따라오는 형식 (예를들어, RequestT, FooBarT)

<a id="s5-3-camel-case"></a>

### 5.3 캐멀 케이스

"IPv6" 또는 "iOS"와 같은 두문자어 또는 특이한 구문이 있는 경우와 같이 영어 구를 카멜 표기법으로 변환하는 합리적인 방법이 두 가지 이상인 경우가 있습니다. 예측 가능성을 개선하기 위해 Google
Style은 다음과 같은 (거의) 결정적 체계를 지정합니다.

산문 형태의 이름으로 시작:

1. 문구를 일반 ASCII로 변환하고 아포스트로피를 제거하십시오. 예를 들어 "Müller's algorithm"은 "Muellers algorithm"이 될 수 있습니다.
2. 이 결과를 단어로 나누고 공백과 나머지 구두점(일반적으로 하이픈)으로 나눕니다.
    - 추천: 어떤 단어가 이미 전통적인 캐멀 케이스방식이 쓰인다면 이것을 구성하는 부분들로 나눈다. (예를들어 "AdWords"를 "ad words"로). "IOS"는 캐멀케이스가 아니다. 이 부분은 어떠한
      약속에도 위배되므로 적용되지 않는다.
3. 이제 모두 lowercase로 바꾸고 (심지어 두음문자도) 그리고 첫 번째 글자를 대문자로 바꾸는데 그 바꾸는 문자들은:
    - 각 단어
    - 각 단어지만 첫 번째를 제외, 첫 번째는 lowercase
4. 이제 하나로 조합한다.

| 산문 형태                   | 맞음                                   | 틀림                  |
|-------------------------|--------------------------------------|---------------------|
| "XML HTTP request"      | `XmlHttpRequest`                     | `XMLHTTPRequest`    |
| "new customer ID"       | `newCustomerId`                      | `newCustomerID`     |
| "inner stopwatch"       | `innerStopwatch`                     | `innerStopWatch`    |
| "supports IPv6 on iOS?" | `supportsIpv6OnIos`                  | `supportsIPv6OnIOS` |
| "YouTube importer"      | `YouTubeImporter` `YoutubeImporter`* |                     |

*는 권장되지 않음

> 참고: 참고: 일부 단어는 영어에서 모호하게 하이픈으로 연결됩니다. 예를 들어 "nonempty"와 "non-empty"는 모두 정확하므로 메서드 이름 checkNonempty와 checkNonEmpty도
> 마찬가지로 둘 다 정확합니다.

<a id="s6-programming-practices"></a>

## 6. 프로그래밍 연습

<a id="s6-1-override"></a>

### 6.1 @Override: 항상 사용한다

@Override가 사용가능할 때 이 애노테이션을 사용합니다.
여기에는

- 슈퍼클래스 메서드를 재정의하는 클래스 메서드,
- 인터페이스 메서드를 구현하는 클래스 메서드,
- 슈퍼인터페이스 메서드를 재지정하는 인터페이스 메서드

가 포함됩니다.

예외: 부모 함수가 @Deprecated가 되면 @Override를 생략할 수 있습니다.

<a id="s6-2-caught-exceptions"></a>

### 6.2 예외 잡기: 생략 하지 말것

아래에 언급된 경우를 제외하고 포착된 예외에 대해 아무 조치도 취하지 않는 것은 거의 올바른 일이 아닙니다.
(일반적인 응답은 이를 기록하거나 "불가능"하다고 간주되는 경우 'AssertionError'로 다시 던지는 것입니다)

catch 블록에서 어떠한 조치도 취하지 않는 것이 정말 적절하다면, 이에 대한 정당한 이유를 주석에 설명합니다.

```java
try{
        int i=Integer.parseInt(response);
        return handleNumericResponse(i);
        }catch(NumberFormatException ok){
        // 숫자가 아니다; 괜찮으니 그냥 넘어간다
        }
        return handleTextResponse(response);
```

예외: 테스트에서 발견된 예외는 이름이 expected이거나 예상대로 시작하는 경우 주석 없이 무시될 수 있습니다.
다음은 테스트 중인 코드가 예상 유형의 예외를 throw하는지 확인하기 위한 매우 일반적인
관용구이므로 여기에서는 주석이 필요하지 않습니다.

```java
try{
        emptyStack.pop();
        fail();
        }catch(NoSuchElementException expected){
        }
```

<a id="s6-3-static-members"></a>

### 6.3 정적 멤버: 클래스를 사용할 수 있음

정적 클래스 멤버에 대한 참조를 한정해야 하는 경우 해당 클래스 유형의 참조나 표현식이 아니라 해당 클래스의 이름으로 한정됩니다

```java
Foo aFoo=...;
        Foo.aStaticMethod(); // 좋음
        aFoo.aStaticMethod(); // 나쁨
        somethingThatYieldsAFoo().aStaticMethod(); // 아주 나쁨
```

<a id="s6-4-finalizers"></a>

### 6.4 종료자

Object.finalize를 재정의하는 것은 극히 드뭅니다.
> 팁: 하지 마세요. 꼭 해야 한다면 먼저 Effective Java Item 8, "Avoid finalizers and cleaners"를 매우 주의 깊게 읽고 이해하시기 바랍니다.

<a id="s7-javadoc"></a>

## 7. Javadoc

<a id="s7-1-formatting"></a>

### 7.1 서식

<a id="s7-1-1-general-form"></a>

#### 7.1.1 일반 형식

Javadoc의 일반적인 형태는 다음과 같습니다.

```java
/**
 * Multiple lines of Javadoc text are written here,
 * wrapped normally...
 */
public int method(String p1){...}
```

혹은 한줄의 예는:

```java
/** An especially short bit of Javadoc. */
```

기본 형식은 항상 허용됩니다.
한 줄 형식은 전체 Javadoc 블록(주석 마커 포함)이 한 줄에 맞을 때 대체될 수 있습니다.
이는 @return과 같은 블록 태그가 없는 경우에만 적용됩니다.

<a id="s7-1-2-paragraphs"></a>

#### 7.1.2 문단

하나의 빈 줄, 즉 정렬된 선행 별표(*)만 포함하는 줄은 단락 사이와 블록 태그 그룹(있는 경우) 앞에 나타납니다.
첫 번째를 제외한 각 단락은 첫 번째 단어 바로 앞에 `<p>`가 있고 그 뒤에 공백이 없습니다.
`<ul>` 또는 `<table>`과 같은 다른 블록 수준 요소에 대한 HTML 태그 앞에 `<p>`가 붙지 않습니다.

<a id="s7-1-3-block-tags"></a>

#### 7.1.3 블럭 태그

사용되는 모든 표준 "블록 태그"는 `@param`, `@return`, `@throws`, `@deprecated` 순서로 나타나며 이 네 가지 유형은 빈 설명과 함께 나타나지 않습니다.
블록 태그가 한 줄에 맞지 않으면 연속 줄은 @ 위치에서 4개(또는 그 이상) 공백으로 들여쓰기됩니다.

<a id="s7-2-the-summary-fragment"></a>

### 7.2 요약

각 Javadoc 블록은 간략한 요약 조각으로 시작합니다. 이 조각은 매우 중요합니다. 클래스 및 메서드 인덱스와 같은 특정 컨텍스트에 나타나는 텍스트의 유일한 부분입니다.

이것은 완전한 문장이 아니라 명사구 또는 동사구인 단편입니다.
`A {@code Foo} is a...` 또는 `This method returns...`로 시작하지 않으며 `Save the record.`와 같은 완전한 명령문을 형성하지도 않습니다.


> 팁: 주로 하는 실수: /** @return the customer ID */ 이것은 잘못 되었고 /** Returns the customer ID. */로 바뀌어야 한다.

<a id="s7-3-where-javadoc-is-used"></a>

### 7.3 Javadoc이 사용되는 곳

최소한 Javadoc은 모든 공개 클래스와 이러한 클래스의 모든 공개 또는 보호 멤버에 대해 존재하며 아래에 언급된 몇 가지 예외가 있습니다.

<a id="s7-3-1-exception-self-explanatory-members"></a>

#### 7.3.1 예외: 함수 설명

Javadoc은 getFoo()와 같은 "단순하고 명백한" 멤버에 대해선 선택 사항입니다.
("Returns the foo"와 같이 "foo를 반환한다" 이외에는 외에는 추가적으로 설명할 것이 없는 경우)


> 중요: 그렇다고 해서 독자가 알아야할 정보를 빠트리는 것은 안됩니다.
> 예를들어 getCanonicalName의 경우 문서화를 빠트리리면 안됩니다. 왜냐하면 일반적 독자는 canonical name이 무슨 뜻인지 모르기 때문입니다.

<a id="s7-3-2-exception-overrides"></a>

#### 7.3.2 예외: 오버라이드

상위 유형 메소드를 대체하는 메소드에 Javadoc이 항상 있는 것은 아닙니다.

<a id="s7-4-non-required-javadoc"></a>

#### 7.3.4 Javadoc이 필요없는 경우

다른 클래스 및 멤버는 필요에 따라 또는 원하는대로 Javadoc을 가집니다.

구현 주석이 클래스 또는 멤버의 전반적인 용도 또는 동작을 정의하는 데 사용될 때마다 해당 주석은 대신 Javadoc으로 작성됩니다.(/ ** 사용).


