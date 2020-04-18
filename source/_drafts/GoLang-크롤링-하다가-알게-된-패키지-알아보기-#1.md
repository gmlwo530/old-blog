---
title: "[GoLang] 크롤링 하다가 알게 된 패키지 알아보기 #1"
tags:
  - go
  - golang
  - 크롤링
---

Go를 이용해 크롤링을 하면서 두 가지 문제가 생겼다.

1. 한국 웹 사이트는 Content Type이 EUC-KR로 세팅되어 있어서, 크롤링을 해왔을 때 한글이 깨진다.
2. [goquery](https://github.com/PuerkitoBio/goquery)라는 HTML의 DOM을 CSS selector로 가져 올 수 있게 해주는 라이브러리를 사용하는데, DOM을 console에 프린터 해줄 수 있는 기능이 없다.

결국 답은 StackOverFlow에 있었다. 먼저 해결법을 보자.

#### _한국 웹 사이트는 Content Type이 EUC-KR로 세팅되어 있어서, 크롤링을 해왔을 때 한글이 깨진다._ ([출처](https://stackoverflow.com/a/31661586))

```go
res, err := http.Get(url)

contentType := res.Header.Get("Content-Type")
utf8reader, err := charset.NewReader(res.Body, contentType) // NewReader 함수는 io.Reader를 반환한다.

doc, err := goquery.NewDocumentFromReader(utf8reader)
...
```

(편의를 위해 err 체크하는 코드는 생략)

위 코드는 html의 Content-Type에 정의 된 인코딩 타입으로부터 utf-8 형식으로 인코딩 해주는 코드이다.

참고로, `NewDocumentFromReader` 함수는 dom을 css selector로 읽을 수 있는 타입으로 변환 해주는 함수이다.

#### _DOM을 console에 프린터 해줄 수 있는 기능이 없다._ ([출처](https://stackoverflow.com/a/38855264))

```go
for _, n := range dom.Nodes {
    var buf bytes.Buffer
    w := io.Writer(&buf)
    html.Render(w, n)

    fmt.Println(buf.String())
}
```

여기서 dom 변수는 `goquery` 라이브러리에서 정의한 구조체 타입을 가지고 있는 변수인데, 이 변수에서 [Node](https://godoc.org/golang.org/x/net/html#Node)타입의 구조체들을 슬라이스로 뽑을 수 있다.

이 Node를 가지고 콘솔에 dom이 어떻게 생겼는지 찍어 볼 수 있다.

문제 해결은 됐지만, 코드에 대한 이해도 정확히 하지 않은채 넘어가면 나에게 남는 것이 없다.

그렇기 때문에 첫 번째 문제 해결법에서 등장하는 `charset`과 `io` 패키지는 어떤 것인지 알아보고, 두 번째 문제 해결법에서 등장하는
`bytes`와 `html` 패키지는 어떤 것인지 알아보자.

다음 글에서 계속 알아보도록 하겠다.

---

**Reference**

- [https://stackoverflow.com/a/31661586](https://stackoverflow.com/a/31661586)
- [https://stackoverflow.com/a/38855264](https://stackoverflow.com/a/38855264)
