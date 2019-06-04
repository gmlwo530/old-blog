---
title: '[Flutter] 토이 프로젝트 후기 - (2)'
tags:
  - Flutter
  - 이야기
---

1편에서 이어서 2편은 프로젝트를 진행 과정을 소개하고 후기를 마무리 하겠습니다.

## 🗂 Flutter

1. **Widget**

  Flutter에서 대부분의 UI들은 Widget Class에 속해 있습니다.
  예를 들어, [AlertDialog](https://api.flutter.dev/flutter/material/AlertDialog-class.html) 문서를 보면 

  (사진)

  임을 확인 할 수 있습니다.

2. **StatelessWidget & StatefulWidget**

  React를 사용해보신 개발자 분들에게는 친숙한 개념일 수도 있습니다. Flutter의 모든 UI 즉 Widget은 상태(state)를 가집니다. 

  Widget이 StatelessWidget을 상속 할 때는 상태가 변하지 않아도 되는 UI로 그려집니다. 

  Widget이 StatefullWidget을 상속 할 때는 상태가 변하는 UI로 그려집니다. Flutter에서 제공하는 `setState` 함수를 통해서 widget의 상태를 변화 시킬 수 있습니다. (최근에 알게 되었는데 setState 말고도 widget의 상태를 관리해주는 방법들이 제공된다고 합니다. 특히 [provider](https://github.com/google/flutter-provide)라는 프레임워크가 2019 Google I/O에서 언급이 되었는데, 굉장히 잘 만들었으니 꼭 사용하라고 언급 되었습니다.)

  이전에 react 개발 경험이 있어 state가 낯설지 않았습니다. react 개발을 했을 때 또 느꼈지만, ui의 state를 관리해줄 수 있다는 점은 굉장히 좋은 방법인거 같습니다.

<br>

## 🗄 Save Data
  
  앱을 간단하게 하기 위해서 데이터 저장은 sqlite를 이용해서 디바이스 내부에 저장히기로 결정했습니다. Flutter에서 sqlite를 이용하는 방법을 찾아보니, package를 이용하는게 제일 편리하다고 판단하여, [sqflite](https://github.com/tekartik/sqflite)라는 package를 추가 했습니다.

  flutter가 입에 오르기 시작한지 얼마되지 않은 만큼, package들도 생겨나기 시작한지 얼마 안된 거 같습니다. star 갯수나 doc의 완성도가 좀 떨어지는 느낌을 받았지만 package 덕분에 쉽게 sqlite를 사용 할 수 있었습니다.

  ```dart
    import 'package:path/path.dart';
    import 'package:path_provider/path_provider.dart';
    import 'package:sqflite/sqflite.dart';

    ...

    initDB() async {
      ...

      return await openDatabase(path, version: 1, onOpen: (db) {
      }, onCreate: (Database db, int version) async {
        await db.execute("CREATE TABLE Line ("
            "id INTEGER PRIMARY KEY,"
            "content TEXT,"
            "created_at INTEGER"
            ")");
      });
    }

    getLine(int id) async {
      final db = await database;
      var res = await db.query("Line", where: "id = ?", whereArgs: [id]);
      return res.isNotEmpty ? Line.fromJson(res.first) : null ;
    }
  ```
  - package를 사용해도 sql 문구를 통해 Database를 만들고, data를 불러와야 했습니다. `,` 같은 사소한 오타가 적지 않게 개발 시간을 많이 잡아 먹었습니다.
  - data를 가지고 와서 json으로 변경을 해주어야 했습니다. 이 과정에 `dynamic`, `factory`라는 개념을 사용 했는데, 정확히 이해를 하지 못하고 구현했습니다. 나중에 기회가 되면 공부를 해봐야겠습니다.


## 🏠 Home

## ️️️️📄 List
## ️️️️⚙️ More
