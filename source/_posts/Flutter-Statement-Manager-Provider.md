---
title: Flutter State Management - Provider
date: 2020-01-12 17:33:13
tags:
  - Flutter
---

Flutter에는 State가 있다. 사용자에 의해 이벤트가 발생 했을 때 state를 이용하여 UI를 업데이트 해준다.

예를 들자면, 우리가 Flutter Project를 처음 생성 했을 때 기본으로 있는 count 앱을 들 수 있다.
사용자가 Floating Button인 + 버튼을 누르면 화면 중앙에 있는 숫자가 1씩 증가한다.
아래 코드와 같이 state를 이용하여 `_counter` 변수를 업데이트하고 UI를 업데이틑 하는 것을 확인 할 수 있다.

```dart
int _counter = 0;

void _increment(){
  setState( () {
    _counter++;
  });
}
```
