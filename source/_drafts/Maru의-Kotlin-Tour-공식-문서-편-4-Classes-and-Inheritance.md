---
title: [Maru의 Kotlin Tour 공식 문서 편] 4 Classes and Inheritance
tags:
  - Kotlin
---

## Classes

kotlin에서 class는 `class` 키워드로 선언한다. body를 생략 할 수도 있다.

```kotlin
class Invoice { }

class Empty
```

## Constructors

kotlin의 class는 하나의 **primary constructor**와 하나 이상의 **secondary constructor**를 가질 수 있다.
