---
title: "[GoLang] 크롤링 하다가 알게 된 패키지 알아보기 #2 (charset, io)"
tags:
  - go
  - golang
  - 크롤링
---

[io](https://golang.org/pkg/io/) package이다.

아래 코드를 보면 `io.Reader`를 사용하는 것을 볼 수 있다.

이쯤되면 `io` 패키지가 궁금해진다.

## io

Go는 byte를 사용하여 작업하기 위해 만들어진 프로그래밍 언어이다.

io package는 바이트 스트림을 다루기 위한 인터페이스와 헬퍼를 제공한다.

먼저 byte을 다루기 때 제일 기본적으로 사용되는 두 가지 함수 Reading & Writing을 알아보자

### Reading Bytes

```go
type Reader interface {
  Read(p []byte) (n int, err error)
}
```

이 인터페이스는 network connection, files, 그리고 wrappers for in-memory slices에 이르기까지 모든 표준 라이브러리를 통해 구현 된다.

Reader는 Read() 메소드가 똑같은 바이트들을 재사용 할 수 있게 buffer(위 코드에서 p 인자이다)를 전달함으로써 동작한다. 만약 Read() 메소드가 하나의 인자를 받는 것 대신에 새로운 byte 슬라이드를 리턴한다면 reader는 Read() 햠수를 실행 할 때마다 새로운 byte 슬라이스를 생성하게 된다. 이런 상황은 가비지 콜렉터를 엉망 징창으로 만들 수 있다.

Reader 인터페이스가 가지고 있는 하나의 문제점은 미묘한 규칙들과 함께 한다는 것이다.

1. Reader 인터페이스는 스트림이 끝났을 때 io.EOF error를 정상 동작한 것처럼 반환한다.
2. 버퍼가 채워질 것이라는 보장이 없다. 만약 8 바이트 슬라이스를 인자로 넘기면, 0에서 8바이트 사이중 어떤 바이트든 받게 될 수도 있다는 말이다.

### Writing Bytes

```go
type Writer interface {
        Write(p []byte) (n int, err error)
}
```

---

**Reference**

- [https://medium.com/go-walkthrough/go-walkthrough-io-package-8ac5e95a9fbd](https://medium.com/go-walkthrough/go-walkthrough-io-package-8ac5e95a9fbd)
- [https://mingrammer.com/translation-go-walkthrough-io-package/](https://mingrammer.com/translation-go-walkthrough-io-package/)
