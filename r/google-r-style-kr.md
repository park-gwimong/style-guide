# Google R Style Guide

> 이 문서는 Google의 R Style Guide를 번역하며 정리한 문서입니다. 약간의 의역이 섞여 있을 수 있지만 본 의도는 해치지 않습니다.

원문 주소 : https://google.github.io/styleguide/Rguide.html

---

<details markdown="1">
  <summary>Table of Contents</summary>

- [1 개요](#s1-syntax)
    * [1.1 명명 규칙](#s1-1-naming-conventions)
    * [1.2 attach를 사용하지 마세요](#s1-2-do-not-use-attach)
- [2 파이프](#s2-pipes)
    * [2.1 오른쪽 할당](#s2-1-right-hand-assignment)
    * [2.2 명시적 반환 사용](#s2-2-use-explicit-returns)
    * [2.3 한정 네임스페이스](#s2-3-qualifying-namespaces)
- [3 문서화](#s3-documentation)
    * [3.1 Packeg-level 문서](#s3-1-package-level-documentation)

</details>

R은 주로 통계 컴퓨팅에 사용되는 고급 프로그래밍 언어입니다.
그리고 그래픽. R 프로그래밍 스타일 가이드의 목표는 R 코드를 만드는 것입니다.
더 쉽게 읽고, 공유하고, 확인할 수 있습니다.

Google R 스타일 가이드는 Hadley Wickham의 [Tidyverse 스타일 가이드](https://style.tidyverse.org/)의 포크입니다.
[라이선스](https://creativecommons.org/licenses/by-sa/2.0/). Google 수정은 내부 R 사용자 커뮤니티와 공동으로 개발되었습니다. 이 문서의 나머지 부분에서는
Tidyverse 가이드와 Google의 주요 차이점과 이러한 차이점이 존재하는 이유를 설명합니다.

<a id="s1-syntax"></a>

## 1 Syntax

<a id="s1-1-naming-conventions"></a>

### 1.1 명명 규칙

Google은 다른 개체와 명확하게 구별하기 위해 'BigCamelCase'로 기능을 식별하는 것을 선호합니다.

```
# Good
DoNothing <- function() {
  return(invisible(NULL))
}
```

개인 함수의 이름은 점으로 시작해야 합니다. 이는 기능의 출처와 용도를 모두 전달하는 데 도움이 됩니다.

```
# Good
.DoNothingPrivately <- function() {
  return(invisible(NULL))
}
```

이전에는 `dot.case`로 개체 이름을 지정하는 것이 좋습니다. S3 방법과 혼동을 일으키기 때문에 우리는 여기서 멀어지고 있습니다.

<a id="s1-2-do-not-use-attach"></a>

### 1.2 attach()를 사용하지 마세요

`attach()`를 사용할 때 오류가 발생할 가능성은 많습니다.

<a id="s2-pipes"></a>

## 2 파이프

<a id="s2-1-right-hand-assignment"></a>

### 2.1 오른쪽 할당

오른손 할당을 사용하는 것을 지원하지 않습니다.

```
# Bad
iris %>%
  dplyr::summarize(max_petal = max(Petal.Width)) -> results
```

이 규칙은 다른 언어의 관행과 상당히 다르며 개체가 정의된 코드에서 보기가 더 어렵습니다.
예를 들어 `foo <-`를 검색하는 것이 `foo <-` 및 `-> foo`를 검색하는 것보다 쉽습니다.

<a id="s2-2-use-explicit-returns"></a>

### 2.2 명시적 반환 사용

R의 암시적 반환 기능에 의존하지 마십시오.
개체 `return()`에 대한 의도를 명확히 하는 것이 좋습니다

```
# Good
AddValues <- function(x, y) {
  return(x + y)
}

# Bad
AddValues <- function(x, y) {
  x + y
}
```

<a id="s2-3-qualifying-namespaces"></a>

### 2.3 한정 네임스페이스

사용자는 모든 외부 기능에 대한 네임스페이스를 명시적으로 한정해야 합니다.

```
# Good
purrr::map()
```

모든 기능을 NAMESPACE로 가져오기 위해 `@import` Roxygen 태그를 사용하지 않는 것이 좋습니다.
Google은 매우 큰 R 코드베이스를 보유하고 있으며 모든 기능을 가져오면 이름이 충돌할 위험이
너무 큽니다.

`::`을 사용하면 약간의 성능 저하가 발생하지만 코드의 종속성을 더 쉽게 이해할 수 있습니다.
이 규칙에는 몇 가지 예외가 있습니다.

* 중위 함수(`%name%`)는 항상 가져와야 합니다.
* 특정 `rlang` 대명사, 특히 `.data`는 가져와야 합니다.
* `datasets`, `utils`, `grDevices`, `graphics`, `stats` and `methods`.  
  필요한 경우 전체 패키지를 `@import`할 수 있습니다.

함수를 가져올 때 외부 종속성이 사용되는 함수 위의 Roxygen 헤더에 `@importFrom` 태그를 배치합니다.

<a id="s3-documentation"></a>

## 3 문서화

<a id="s3-1-package-level-documentation"></a>

### 3.1 Package-level 문서

모든 패키지에는 `packagename-package.R` 파일에 패키지 문서 파일이 있어야 합니다.
