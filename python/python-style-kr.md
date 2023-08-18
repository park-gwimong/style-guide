# 구글 Python 스타일 가이드

> 이 문서는 Google Python Style Guide를 번역하며 정리한 문서입니다. 약간의 의역이 섞여 있을 수 있지만 본 의도는 해치지 않습니다.

원문 주소 : https://google.github.io/styleguide/pyguide.html

---

<details markdown="1">
  <summary>Table of Contents</summary>

- [1 Background](#s1-background)
- [2 Python Language Rules](#s2-python-language-rules)
    * [2.1 Lint](#s2.1-lint)
    * [2.2 Imports](#s2.2-imports)
    * [2.3 Packages](#s2.3-packages)
    * [2.4 Exceptions](#s2.4-exceptions)
    * [2.5 Mutable Global State](#s2.5-global-variables)
    * [2.6 Nested/Local/Inner Classes and Functions](#s2.6-nested)
    * [2.7 Comprehensions & Generator Expressions](#s2.7-comprehensions)
    * [2.8 Default Iterators and Operators](#s2.8-default-iterators-and-operators)
    * [2.9 Generators](#s2.9-generators)
    * [2.10 Lambda Functions](#s2.10-lambda-functions)
    * [2.11 Conditional Expressions](#s2.11-conditional-expressions)
    * [2.12 Default Argument Values](#s2.12-default-argument-values)
    * [2.13 Properties](#s2.13-properties)
    * [2.14 True/False Evaluations](#s2.14-truefalse-evaluations)
    * [2.16 Lexical Scoping](#s2.16-lexical-scoping)
    * [2.17 Function and Method Decorators](#s2.17-function-and-method-decorators)
    * [2.18 Threading](#s2.18-threading)
    * [2.19 Power Features](#s2.19-power-features)
    * [2.20 Modern Python: from \_\_future\_\_ imports](#s2.20-modern-python)
    * [2.21 Type Annotated Code](#s2.21-type-annotated-code)
- [3 Python Style Rules](#s3-python-style-rules)
    * [3.1 Semicolons](#s3.1-semicolons)
    * [3.2 Line length](#s3.2-line-length)
    * [3.3 Parentheses](#s3.3-parentheses)
    * [3.4 Indentation](#s3.4-indentation)
        + [3.4.1 Trailing commas in sequences of items?](#s3.4.1-trailing-commas)
    * [3.5 Blank Lines](#s3.5-blank-lines)
    * [3.6 Whitespace](#s3.6-whitespace)
    * [3.7 Shebang Line](#s3.7-shebang-line)
    * [3.8 Comments and Docstrings](#s3.8-comments-and-docstrings)
        + [3.8.1 Docstrings](#s3.8.1-comments-in-doc-strings)
        + [3.8.2 Modules](#s3.8.2-comments-in-modules)
        + [3.8.2.1 Test modules](#s3.8.2.1-test-modules)
        + [3.8.3 Functions and Methods](#s3.8.3-functions-and-methods)
        + [3.8.4 Classes](#s3.8.4-comments-in-classes)
        + [3.8.5 Block and Inline Comments](#s3.8.5-block-and-inline-comments)
        + [3.8.6 Punctuation, Spelling, and Grammar](#s3.8.6-punctuation-spelling-and-grammar)
    * [3.10 Strings](#s3.10-strings)
        + [3.10.1 Logging](#s3.10.1-logging)
        + [3.10.2 Error Messages](#s3.10.2-error-messages)
    * [3.11 Files, Sockets, and similar Stateful Resources](#s3.11-files-sockets-closeables)
    * [3.12 TODO Comments](#s3.12-todo-comments)
    * [3.13 Imports formatting](#s3.13-imports-formatting)
    * [3.14 Statements](#s3.14-statements)
    * [3.15 Accessors](#s3.15-accessors)
    * [3.16 Naming](#s3.16-naming)
        + [3.16.1 Names to Avoid](#s3.16.1-names-to-avoid)
        + [3.16.2 Naming Conventions](#s3.16.2-naming-conventions)
        + [3.16.3 File Naming](#s3.16.3-file-naming)
        + [3.16.4 Guidelines derived from Guido's Recommendations](#s3.16.4-guidelines-derived-from-guidos-recommendations)
    * [3.17 Main](#s3.17-main)
    * [3.18 Function length](#s3.18-function-length)
    * [3.19 Type Annotations](#s3.19-type-annotations)
        + [3.19.1 General Rules](#s3.19.1-general-rules)
        + [3.19.2 Line Breaking](#s3.19.2-line-breaking)
        + [3.19.3 Forward Declarations](#s3.19.3-forward-declarations)
        + [3.19.4 Default Values](#s3.19.4-default-values)
        + [3.19.5 NoneType](#s3.19.5-nonetype)
        + [3.19.6 Type Aliases](#s3.19.6-type-aliases)
        + [3.19.7 Ignoring Types](#s3.19.7-ignoring-types)
        + [3.19.8 Typing Variables](#s3.19.8-typing-variables)
        + [3.19.9 Tuples vs Lists](#s3.19.9-tuples-vs-lists)
        + [3.19.10 Type variables](#s3.19.10-typevars)
        + [3.19.11 String types](#s3.19.11-string-types)
        + [3.19.12 Imports For Typing](#s3.19.12-imports-for-typing)
        + [3.19.13 Conditional Imports](#s3.19.13-conditional-imports)
        + [3.19.14 Circular Dependencies](#s3.19.14-circular-dependencies)
        + [3.19.15 Generics](#s3.19.15-generics)
        + [3.19.16 Build Dependencies](#s3.19.16-build-dependencies)
- [4 Parting Words](#4-parting-words)

</details>

<a id="s1-background"></a>
<a id="1-background"></a>

<a id="background"></a>

## 1 Background

코드 형식을 올바르게 지정할 수 있도록 [settings file for Vim](python_style.vim)을 지원합니다.   
Emacs의 경우 기본값 설정이 바람직해야 합니다.

많은 팀에서 서식에 대한 논쟁을 피하기 위해 [Black](https://github.com/psf/black) 또는 [Pyink](https://github.com/google/pyink) 와 같은 자동 포맷터를 사용합니다.

<a id="s2-python-language-rules"></a>
<a id="2-python-language-rules"></a>

<a id="python-language-rules"></a>

## 2 Python Language Rules

<a id="s2.1-lint"></a>
<a id="21-lint"></a>

<a id="lint"></a>

### 2.1 Lint

`pylint`를 실행하여 [pylintrc](https://google.github.io/styleguide/pylintrc)를 당신의 코드에서 사용하세요. 

<a id="s2.1.1-definition"></a>
<a id="211-definition"></a>

<a id="lint-definition"></a>

#### 2.1.1 Definition

`pylint`는 Python 소스 코드에서 버그 및 스타일 문제를 찾는 도구입니다.  
C, C++ 같이 덜 동적인 언어에 대해 컴파일러가 일반적으로 포착하는 문제를 찾습니다.  
Python의 동적 특성으로 인해 일부 경고가 올바르지 않을 수 있습니다.  
그러나, 이러한 경고는 매우 드물게 발생합니다.

<a id="s2.1.2-pros"></a>
<a id="212-pros"></a>

<a id="lint-pros"></a>

#### 2.1.2 Pros
오타, 할당 전 변수 사용 등과 같이 놓치기 쉬운 오류를 포착합니다.

<a id="s2.1.3-cons"></a>
<a id="213-cons"></a>

<a id="lint-cons"></a>

#### 2.1.3 Cons

`pylint`는 완벽하지 않습니다.  
이를 활용하기 위해 때로는 추가로 작성하거나, 경고를 표시하지 않거나, 수정해야 합니다. 


<a id="s2.1.4-decision"></a>
<a id="214-decision"></a>

<a id="lint-decision"></a>


#### 2.1.4 Decision

코드에서 `pylint`를 실행해야 합니다. 

다른 문제가 숨겨지지 않도록 부적절한 경우 경고를 억제합니다.  
경고를 표시하지 않으려면 줄 수준의 주석을 설정 할 수 있습니다.

```python
def do_PUT(self):  # WSGI name, so pylint: disable=invalid-name
    ...
```

`pylint` 경고는 각각 기호 이름(`empty-docstring`)으로 식별됩니다.  
구굴 관련 경고는 `g-`으로 시작합니다.  

경고에 대한 엊게 이유가 기호 이름에서 명확하지 않은 경우 설명을 추가하세요.  
이러한 방식으로 억제하는 것은 쉽게 억제를 검색하고, 다시 방문 할 수 있다는 장점이 있습니다.  

다음을 수행하여 `pylint` 경고 목록을 확인 할 수 있습니다.
```shell
pylint --list-msgs
```

특정 메시지에 대한 자세한 정보를 얻으려면 다음을 사용하세요.  
```shell
pylint --help-msg=invalid-name
```

더 이상 사용되지 않는 이전 형식인  
`pylint: disable`보다 `pylint: disable-msg`을 권장합니다.  

사용되지 않은 인수 경고는 함수 시작 부분에서 변수를 삭제하여 억제할 수 있습니다.  
삭제 이유를 설명하는 주석을 항상 포함하세요.    
"Unused."이면 충분합니다.

예시:
```python
def viking_cafe_order(spam: str, beans: str, eggs: str | None = None) -> str:
    del beans, eggs  # Unused by vikings.
    return spam + spam + spam
```

이 경고를 억제하는 다른 일반적인 형태로는 사용되지 않는 인수의 식별자로 '`_`'를 사용하거나, 인수 이름 앞에 '`unused_`' 또는 '`_`'를 할당합니다.
이러한 양힉은 허용되지만, 더이상 권장되지 않습니다. 이러한 중단 호출자는 이름으로 인수를 전달하고 인수가 실제로 사용되지 않도록 강제하지 않습니다.  


<a id="s2.2-imports"></a>
<a id="22-imports"></a>

<a id="imports"></a>


### 2.2 Imports
개별 클래스나 함수가 아닌 패키지와 모듈에만 `import`을 사용하세요.

<a id="s2.2.1-definition"></a>
<a id="221-definition"></a>

<a id="imports-definition"></a>

#### 2.2.1 Definition
한 모듈에서 다른 모듈로 코드를 공유하기 위한 재사용성 메커니즘입니다.

<a id="s2.2.2-pros"></a>
<a id="222-pros"></a>

<a id="imports-pros"></a>

#### 2.2.2 Pros
네임스페이스 관리 규칙은 간단합니다.  각 식별자의 출처는 일괄된 방식으로 표시됩니다.  
`x.Obj`는 `Obj`가 모듈 `x`에 정의 되어 있다고 알려줍니다.  

<a id="s2.2.3-cons"></a>
<a id="223-cons"></a>

<a id="imports-cons"></a>


#### 2.2.3 Cons
모듈 이름은 여전히 충돌할 수 있습니다. 일부 모듈 이름은 불편할 정도로 깁니다.

<a id="s2.2.4-decision"></a>
<a id="224-decision"></a>

<a id="imports-decision"></a>

#### 2.2.4 Decision

* 패키지 및 모듈을 가져오려면 `import x`를 사용하십시오.
* `from x import y`를 사용하십시오. 여기서 `x`는 패키지 접두어이고 `y`는 접두어가 없는 모듈 이름입니다.
* 다음 상황에서 `from x import y as z`를 사용하십시오.
    - `y`라는 이름의 두 모듈을 가져옵니다.
    - `y`는 현재 모듈에 정의된 최상위 이름과 충돌합니다.
    - `y`는 공개 API의 일부인 공통 매개변수 이름(예: `features`)과 충돌합니다.
    - `y`는 불편할 정도로 긴 이름입니다.
    - `y`는 코드 컨텍스트에서 너무 일반적입니다.
      (예: `from storage.file_system import options as fs_options`).
* `z`가 표준 약어인 경우에만 `import y as z`를 사용하십시오.
  (예: `np로 numpy 가져오기`).

예를 들어 `sound.effects.echo` 모듈은 다음과 같이 가져올 수 있습니다.
```python
from sound.effects import echo
...
echo.EchoFilter(input, output, delay=0.7, atten=4)
```

가져오기에 상대 이름을 사용하지 마십시오. 모듈이 동일한 패키지에 있더라도 전체 패키지 이름을 사용하십시오. 
이렇게 하면 의도치 않게 패키지를 두 번 가져오는 것을 방지할 수 있습니다.

<a id="imports-exemptions"></a>


##### 2.2.4.1 Exemptions

이 규칙의 예외:
* 다음 모듈의 기호는 정적 분석 및 유형 검사를 지원하는 데 사용됩니다.
    * [`typing` module](#typing-imports)
    * [`collections.abc` module](#typing-imports)
    * [`typing_extensions` module](https://github.com/python/typing_extensions/blob/main/README.md)
* [six.moves module](https://six.readthedocs.io/#module-six.moves)에서 리다이렉션 되었습니다.

<a id="s2.3-packages"></a>
<a id="23-packages"></a>

<a id="packages"></a>

### 2.3 Packages

모듈의 전체 경로 이름 위치를 사용하여 각 모듈을 가져옵니다.

<a id="s2.3.1-pros"></a>
<a id="231-pros"></a>

<a id="packages-pros"></a>

#### 2.3.1 Pros

작성자가 예상한 것과 다른 모듈 검색 경로로 인해 모듈 이름의 충돌이나 잘못된 가져오기를 방지합니다.  
모듈을 더 쉽게 찾을 수 있습니다.

<a id="s2.3.2-cons"></a>
<a id="232-cons"></a>

<a id="packages-cons"></a>

#### 2.3.2 Cons

패키지 계층 구조를 복제해야 하므로 코드 배포가 더 어려워집니다. 최신 배포 메커니즘에는 실제로 문제가 없습니다.

<a id="s2.3.3-decision"></a>
<a id="233-decision"></a>

<a id="packages-decision"></a>

#### 2.3.3 Decision

모든 새 코드는 전체 패키지 이름으로 각 모듈을 가져와야 합니다.  
`import`는 다음과 같아야 합니다.

```python
# Yes:
# Reference absl.flags in code with the complete name (verbose).
import absl.flags
from doctor.who import jodie

_FOO = absl.flags.DEFINE_string(...)
```

```python
# Yes:
# Reference flags in code with just the module name (common).
from absl import flags
from doctor.who import jodie

_FOO = flags.DEFINE_string(...)
```

*(assume this file lives in `doctor/who/` where `jodie.py` also exists)*

```python
# No:
# Unclear what module the author wanted and what will be imported.  The actual
# import behavior depends on external factors controlling sys.path.
# Which possible jodie module did the author intend to import?
import jodie
```

기본 바이너리가 있는 디렉토리는 일부 환경에서 발생하더라도 `sys.path`에 있다고 가정하면 안 됩니다.  
이 경우 코드는 `import jodie`가 로컬 `jodie.py`가 아니라 `jodie`라는 이름의 타사 또는 최상위 패키지를 참조한다고 가정해야 합니다.

<a id="s2.4-exceptions"></a>
<a id="24-exceptions"></a>

<a id="exceptions"></a>


### 2.4 Exceptions

예외가 허용되지만 신중하게 사용해야 합니다.

<a id="s2.4.1-definition"></a>
<a id="241-definition"></a>

<a id="exceptions-definition"></a>

#### 2.4.1 Definition

예외는 오류 또는 기타 예외 조건을 처리하기 위해 정상적인 제어 흐름을 깨는 수단입니다.

<a id="s2.4.2-pros"></a>
<a id="242-pros"></a>

<a id="exceptions-pros"></a>

#### 2.4.2 Pros

정상적인 작업 코드의 제어 흐름은 오류 처리 코드로 인해 복잡해지지 않습니다.  
또한 특정 조건이 발생할 때 제어 흐름이 여러 프레임을 건너뛸 수 있습니다.  

<a id="s2.4.3-cons"></a>
<a id="243-cons"></a>

<a id="exceptions-cons"></a>

#### 2.4.3 Cons

제어 흐름이 혼동될 수 있습니다.  
라이브러리 호출 시 오류 사례를 놓치기 쉽습니다.

<a id="s2.4.4-decision"></a>
<a id="244-decision"></a>

<a id="exceptions-decision"></a>

#### 2.4.4 Decision

예외는 특정 조건을 따라야 합니다.

- 타당할 때 내장된 예외 클래스를 사용하십시오. 
  예를 들어, 위반된 전제 조건과 같은 프로그래밍 실수를 나타내기 위해 `ValueError`를 발생시킵니다
  (예: 음수가 전달되었지만 양수가 필요한 경우).
  공개 API의 인수 값을 검증하기 위해 `assert` 문을 사용하지 마십시오. 
  'assert'는 내부 정확성을 보장하는 데 사용되며 올바른 사용을 강요하거나 예기치 않은 이벤트가 발생했음을 나타내기 위한 것이 아닙니다.   
  예시 :
  ```python
    # Yes:
    def connect_to_next_port(self, minimum: int) -> int:
      """Connects to the next available port.
    
      Args:
        minimum: A port value greater or equal to 1024.
    
      Returns:
        The new minimum port.
    
      Raises:
        ConnectionError: If no available port is found.
      """
      if minimum < 1024:
        # Note that this raising of ValueError is not mentioned in the doc
        # string's "Raises:" section because it is not appropriate to
        # guarantee this specific behavioral reaction to API misuse.
        raise ValueError(f'Min. port must be at least 1024, not {minimum}.')
      port = self._find_next_open_port(minimum)
      if port is None:
        raise ConnectionError(
            f'Could not connect to service on port {minimum} or higher.')
      assert port >= minimum, (
          f'Unexpected port {port} when minimum was {minimum}.')
      return port
  ```

  ```python
    # No:
    def connect_to_next_port(self, minimum: int) -> int:
      """Connects to the next available port.

      Args:
        minimum: A port value greater or equal to 1024.

      Returns:
        The new minimum port.
      """
      assert minimum >= 1024, 'Minimum port must be at least 1024.'
      port = self._find_next_open_port(minimum)
      assert port is not None
      return port
  ```


- 라이브러리 또는 패키지는 자체 예외를 정의할 수 있습니다. 
  그렇게 할 때 기존 예외 클래스에서 상속해야 합니다. 
  예외 이름은 `Error`로 끝나야 하며 반복(`foo.FooError`)을 도입하지 않아야 합니다.

- 포괄적인 `except:` 문을 사용하거나 `Exception` 또는 `StandardError`를 포착하지 마십시오.
    - 예외를 다시 발생시키거나
    - 예외가 전파되지 않고 대신 기록되고 억제되는 프로그램에서 격리 지점을 생성합니다.
      예를 들어 가장 바깥쪽 블록을 보호하여 스레드 충돌을 방지합니다.

  Python은 이에 대해 매우 관대해서 
  `except:`는 철자가 틀린 이름, sys.exit() 호출, Ctrl+C 인터럽트, 
  단위 테스트 실패 및 단순히 포착하고 싶지 않은 모든 종류의 예외를 포함한 모든 것을 실제로 포착합니다.

- `try`/`except` 블록의 코드 양을 최소화합니다.
  `try`의 본문이 클수록 예외가 발생할 것으로 예상하지 않은 코드 행에서 예외가 발생할 가능성이 높아집니다. 
  이러한 경우 `try`/`except` 블록은 실제 오류를 숨깁니다.

- `try` 블록에서 예외가 발생했는지 여부에 관계없이 `finally` 절을 사용하여 코드를 실행합니다.
  이는 종종 정리, 즉 파일 닫기에 유용합니다.

<a id="s2.5-global-variables"></a>
<a id="25-global-variables"></a>
<a id="s2.5-global-state"></a>
<a id="25-global-state"></a>

<a id="global-variables"></a>

### 2.5 Mutable Global State

변경 가능한 전역 상태를 피하십시오.

<a id="s2.5.1-definition"></a>
<a id="251-definition"></a>

<a id="global-variables-definition"></a>

#### 2.5.1 Definition

프로그램 실행 중에 변경될 수 있는 모듈 수준 값 또는 클래스 특성입니다.

<a id="s2.5.2-pros"></a>
<a id="252-pros"></a>

<a id="global-variables-pros"></a>

#### 2.5.2 Pros

때때로 유용합니다.

<a id="s2.5.3-cons"></a>
<a id="253-cons"></a>

<a id="global-variables-cons"></a>

#### 2.5.3 Cons

* 캡슐화 중단: 이러한 디자인은 유효한 목표를 달성하기 어렵게 만들 수 있습니다.
  예를 들어 전역 상태를 사용하여 데이터베이스 연결을 관리하는 경우, 
  마이그레이션 중 차이점 계산과 같이 동시에 두 개의 서로 다른 데이터베이스에 연결하는 것이 어려워집니다.
  글로벌 레지스트리에서도 유사한 문제가 쉽게 발생합니다. 
* 모듈을 처음 가져올 때 전역 변수에 대한 할당이 완료되기 때문에 가져오는 동안 모듈 동작을 변경할 가능성이 있습니다.

<a id="s2.5.4-decision"></a>
<a id="254-decision"></a>

<a id="global-variables-decision"></a>

#### 2.5.4 Decision

변경 가능한 전역 상태를 피하십시오.

전역 상태를 사용해야 하는 경우, 변경 가능한 전역 엔터티는 모듈 또는 클래스 특성으로 선언하고 
이름 앞에 `_`를 추가하여 내부로 만들어야 합니다. 전역 상태에 대한 외부 액세스가 필요하다면 공용 함수 또는 클래스 메서드를 통해 수행되어야 합니다.   
아래의 [Naming](#s3.16-naming)을 참조하세요. 


<a id="s2.6-nested"></a>
<a id="26-nested"></a>

<a id="nested-classes-functions"></a>


### 2.6 Nested/Local/Inner Classes and Functions

중첩된 로컬 함수 또는 클래스는 로컬 변수를 닫는 데 사용할 때 좋습니다. 내부 클래스는 괜찮습니다.

<a id="s2.6.1-definition"></a>
<a id="261-definition"></a>

<a id="nested-classes-functions-definition"></a>

#### 2.6.1 Definition

클래스는 메서드, 함수 또는 클래스 내에서 정의할 수 있습니다. 
함수는 메서드나 함수 안에 정의할 수 있습니다. 
중첩 함수는 바깥쪽 범위에 정의된 변수에 대한 읽기 전용 액세스 권한이 있습니다.

<a id="s2.6.2-pros"></a>
<a id="262-pros"></a>

<a id="nested-classes-functions-pros"></a>

#### 2.6.2 Pros

매우 제한된 범위 내에서만 사용되는 유틸리티 클래스 및 함수의 정의를 허용합니다.  
[Abstract data type](https://en.wikipedia.org/wiki/Abstract_data_type)를 구현하는 데 일반적으로 사용됩니다.

<a id="s2.6.3-cons"></a>
<a id="263-cons"></a>

<a id="nested-classes-functions-cons"></a>

#### 2.6.3 Cons

중첩 함수 및 클래스는 직접 테스트할 수 없습니다. 
중첩은 외부 함수를 더 길고 읽기 어렵게 만들 수 있습니다.

<a id="s2.6.4-decision"></a>
<a id="264-decision"></a>

<a id="nested-classes-functions-decision"></a>

#### 2.6.4 Decision

몇 가지주의 사항이 있습니다. 
`self` 또는 `cls` 이외의 로컬 값을 닫을 때를 제외하고 중첩 함수 또는 클래스를 사용하지 마십시오.  
모듈 사용자에게 숨기기 위해 함수를 중첩하지 마십시오. 대신 테스트에서 계속 액세스할 수 있도록 모듈 수준에서 이름에 \_ 접두사를 붙입니다.

<a id="s2.7-comprehensions"></a>
<a id="s2.7-list_comprehensions"></a>
<a id="27-list_comprehensions"></a>
<a id="list_comprehensions"></a>
<a id="list-comprehensions"></a>

<a id="comprehensions"></a>


### 2.7 Comprehensions & Generator Expressions

간단한 경우에 사용하기 좋습니다.

<a id="s2.7.1-definition"></a>
<a id="271-definition"></a>

<a id="comprehensions-definition"></a>

#### 2.7.1 Definition

List, Dict 및 Set 제너레이터 표현식은 
기존의 루프인 `map()`, `filter()` 또는 `lambda`를 사용하지 않고도 컨테이너 유형과 반복자를 만드는 
간결하고 효율적인 방법을 제공합니다.

<a id="s2.7.2-pros"></a>
<a id="272-pros"></a>

<a id="comprehensions-pros"></a>

#### 2.7.2 Pros

다른 dict, list 또는 set 생성 기술보다 더 명확하고 간단할 수 있습니다. 
제너레이터 표현식은 목록을 완전히 생성하지 않기 때문에 매우 효율적일 수 있습니다.


<a id="s2.7.3-cons"></a>
<a id="273-cons"></a>

<a id="comprehensions-cons"></a>

#### 2.7.3 Cons

복잡한 캄프리헨션이나 제너레이터 표현식은 읽기 어려울 수 있습니다.

<a id="s2.7.4-decision"></a>
<a id="274-decision"></a>

<a id="comprehensions-decision"></a>

#### 2.7.4 Decision

간단한 경우에 사용하기 좋습니다. 
상황이 더 복잡해지면 대신 루프를 사용하십시오.

```python
# Yes:
result = [mapping_expr for value in iterable if filter_expr]

result = [{'key': value} for value in iterable
          if a_long_filter_expression(value)]

result = [complicated_transform(x)
          for x in iterable if predicate(x)]

descriptive_name = [
    transform({'key': key, 'value': value}, color='black')
    for key, value in generate_iterable(some_input)
    if complicated_condition_is_met(key, value)
]

result = []
for x in range(10):
    for y in range(5):
        if x * y > 10:
            result.append((x, y))

return {x: complicated_transform(x)
        for x in long_generator_function(parameter)
        if x is not None}

squares_generator = (x ** 2 for x in range(10))

unique_names = {user.name for user in users if user is not None}

eat(jelly_bean for jelly_bean in jelly_beans
    if jelly_bean.color == 'black')
```

```python
# No:
result = [complicated_transform(
    x, some_argument=x + 1)
    for x in iterable if predicate(x)]

result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]

return ((x, y, z)
        for x in range(5)
        for y in range(5)
        if x != y
        for z in range(5)
        if y != z)
```

<a id="s2.8-default-iterators-and-operators"></a>
<a id="default-iterators-operators"></a>


### 2.8 Default Iterators and Operators

list, dictionaries, file과 같이 기본 반복자와 연산자를 지원하는 유형은 이를 사용 하십시오

<a id="s2.8.1-definition"></a>
<a id="281-definition"></a>

<a id="default-iterators-operators-definition"></a>

#### 2.8.1 Definition

사전 및 목록과 같은 컨테이너 유형은 기본 반복자와 멤버십 테스트 연산자("in" 및 "not in")를 정의합니다.


<a id="s2.8.2-pros"></a>
<a id="282-pros"></a>

<a id="default-iterators-operators-pros"></a>

#### 2.8.2 Pros

기본 반복자와 연산자는 간단하고 효율적입니다. 
추가 메서드 호출 없이 작업을 직접 표현합니다. 
기본 연산자를 사용하는 함수는 일반적입니다. 
작업을 지원하는 모든 유형과 함께 사용할 수 있습니다.

<a id="s2.8.3-cons"></a>
<a id="283-cons"></a>

<a id="default-iterators-operators-cons"></a>

#### 2.8.3 Cons

메서드 이름으로 객체의 유형을 알 수 없습니다(변수에 유형 주석이 없는 경우).  
이것은 장점입니다.


<a id="s2.8.4-decision"></a>
<a id="284-decision"></a>

<a id="default-iterators-operators-decision"></a>

#### 2.8.4 Decision

목록, 사전 및 파일과 같이 이를 지원하는 유형에 대해 기본 반복자와 연산자를 사용하십시오. 
내장 유형은 반복자 메소드도 정의합니다. 목록을 반환하는 메서드보다 이러한 메서드를 선호합니다. 
단, 컨테이너를 반복하는 동안 컨테이너를 변경해서는 안 됩니다.

```python
# Yes:
for key in adict: ...
if obj in alist: ...
for line in afile: ...
for k, v in adict.items(): ...
```

```python
# No:
for key in adict.keys(): ...
for line in afile.readlines(): ...
```

<a id="s2.9-generators"></a>
<a id="29-generators"></a>

<a id="generators"></a>
