---
title: "[GoLang] 크롤링 하다가 io package 까보기"
tags:
  - go
  - golang
  - 크롤링
---

io package를 이용해서 아래 코드가 어떤 식으로 되는건지 공부해보기

```go
contentType := res.Header.Get("Content-Type")
utf8reader, err := charset.NewReader(res.Body, contentType)
checkErr(err)

doc, err := goquery.NewDocumentFromReader(utf8reader) // utf8reader is io.Reader
checkErr(err)
```

```go
for _, n := range dom.Nodes {
    var buf bytes.Buffer
    w := io.Writer(&buf)
    html.Render(w, n)

    fmt.Println(buf.String())
}
```

---

**Reference**

- [https://stackoverflow.com/a/31661586](https://stackoverflow.com/a/31661586)
- [https://stackoverflow.com/a/38855264](https://stackoverflow.com/a/38855264)
