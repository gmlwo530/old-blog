---
title: "[Flutter를 읽다] #1 BoxShadow"
tags:
  - Flutter
---

[BoxShadow Class](https://api.flutter.dev/flutter/painting/BoxShadow-class.html)에 대해서 다뤄 보겠습니다.

Container를 꾸며주는 BoxDecoration을 통해 shadow를 줄 때 사용하는 클래스입니다.

먼저 예제 코드부터 보겠습니다

```dart
Container(
  ...
  width: 100.0,
  height: 100.0,
  decoration: BoxDecoration(
    color: Colors.blue,
    boxShadow: [
      new BoxShadow(
        color: Colors.black,
      )
    ]
  ),
)
```

`BoxDecoration`의 boxShadow 속성은 List를 값으로 받습니다. 즉, 여려 색깔의 shadow를 만들 수 있습니다.
