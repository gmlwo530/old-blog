---
title: "[GoLang] 크롤링 하다가 알게 된 패키지 알아보기 #2 (io)"
tags:
  - go
  - golang
  - 크롤링
---

이전 글 목록

이전 글에 이어서 [io](https://golang.org/pkg/io/) package에 대해 알아보자.

와 [charset](https://pkg.go.dev/golang.org/x/net/html/charset?tab=doc) package

## io

Go는 byte를 사용하여 작업하기 위해 만들어진 프로그래밍 언어이다.

io package는 바이트 스트림을 다루기 위한 인터페이스와 헬퍼를 제공하는 패키지이다.

먼저 byte을 다루기 때 제일 기본적으로 사용되는 두 가지 함수 Reading & Writing을 알아보자

<br>

### Reading Bytes

```go
type Reader interface {
  Read(p []byte) (n int, err error)
}
```

Reader(io.Reader)는 데이터를 읽고 버퍼로 이전(transfer)해주는 역할을 한다. 그리고 Read 메소드를 이용해서 버퍼를 이용 할 수 있다.
예제 코드를 하나 보자.

```go
package main

import (
	"fmt"
	"io"
	"strings"
	"os"
)

func main() {
	reader := strings.NewReader("Clear is better than clever")
	p := make([]byte, 4)

	for {
		n, err := reader.Read(p)
		if err != nil{
      if err == io.EOF {
        fmt.Println(string(p[:n])) //should handle any remainding bytes.
        break
      }
      fmt.Println(err)
      os.Exit(1)
		}
		fmt.Println(string(p[:n]))
	}
}
```

_출처 : [https://github.com/vladimirvivien/learning-go/blob/master/tutorial/io/simple_reader.go](https://github.com/vladimirvivien/learning-go/blob/master/tutorial/io/simple_reader.go)_

에제 코드를 보면 `"Clear is better than clever"`라는 문자열 데이터를 버퍼로 이전하고 길이 4짜리의 바이트 슬라이스에 버퍼를 전달 해줍니다.
코드 실행 결과는 아래와 같습니다

```plain
Clea
r is
 bet
ter
than
 cle
ver

```

이 인터페이스는 network connection, files, 그리고 wrappers for in-memory slices에 이르기까지 모든 표준 라이브러리를 통해 구현 됩니다.

Reader는 Read() 메소드가 똑같은 바이트들을 재사용 할 수 있게 buffer(위 코드에서 p 인자이다)를 전달함으로써 동작합니다. 만약 Read() 메소드가 하나의 인자를 받는 것 대신에 새로운 byte 슬라이드를 리턴한다면 reader는 Read() 햠수를 실행 할 때마다 새로운 byte 슬라이스를 생성하게 됩니다. 이런 상황은 가비지 콜렉터를 엉망 징창으로 만들 수 있습니다.

Reader 인터페이스가 가지고 있는 하나의 문제점은 미묘한 규칙들과 함께 한다는 것입니다.

1. Reader 인터페이스는 스트림이 끝났을 때 io.EOF error를 정상 동작한 것처럼 반환된다.
2. 버퍼가 채워질 것이라는 보장이 없다. 만약 8 바이트 슬라이스를 인자로 넘기면, 0에서 8바이트 사이중 어떤 바이트든 받게 될 수도 있다는 말이다.

물론 이런 문제점을 해결 할 수 있는 메소드들이 io에 정의되어 있습니다.
더 자세한 내용은 제가 참고한 [블로그](https://medium.com/go-walkthrough/go-walkthrough-io-package-8ac5e95a9fbd)에서 알아보길 바랍니다.

<br>
<br>

### Writing Bytes

```go
type Writer interface {
        Write(p []byte) (n int, err error)
}
```

Writer는 Reader의 반대이다. 바이트 버퍼를 이용해서 스트림에 넣어준다. 바로 예제를 보자

```go
package main

import (
	"bytes"
	"fmt"
	"os"
)

func main() {
	proverbs := []string{
		"Channels orchestrate mutexes serialize",
		"Cgo is not Go",
		"Errors are values",
		"Don't panic",
	}
	var writer bytes.Buffer

	for _, p := range proverbs {
		n, err := writer.Write([]byte(p))
		if err != nil {
			fmt.Println(err)
			os.Exit(1)
		}
		if n != len(p) {
			fmt.Println("failed to write data")
			os.Exit(1)
		}
	}

	fmt.Println(writer.String())
}
```

출처 : [https://github.com/vladimirvivien/learning-go/blob/master/tutorial/io/using_writer.go](https://github.com/vladimirvivien/learning-go/blob/master/tutorial/io/using_writer.go)

결과 값은 아래와 같다

```plain
Channels orchestrate mutexes serializeCgo is not GoErrors are valuesDon't panic
```

쓰기는 읽기보다 간단한 것을 알 수 있다.

<br><br>

바이트 스트림은 Go 프로그래밍에서 굉장히 많이 다루게 된다. io 패키지는 바이트 스트림을 다루는 기초를 제공 해준다.
io 패키지가 제공 해주는 다양한 메소드와 io 잘 다루기 위한 방법은 참고한 블로그에 나와 있으니, 꼭 시간을 내서 확인 해보길 바란다.

---

**Reference**

- [https://medium.com/go-walkthrough/go-walkthrough-io-package-8ac5e95a9fbd](https://medium.com/go-walkthrough/go-walkthrough-io-package-8ac5e95a9fbd)
- [https://mingrammer.com/translation-go-walkthrough-io-package/](https://mingrammer.com/translation-go-walkthrough-io-package/)
- [https://medium.com/learning-the-go-programming-language/streaming-io-in-go-d93507931185](https://medium.com/learning-the-go-programming-language/streaming-io-in-go-d93507931185)
