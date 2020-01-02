---
title: Glide Error - "You cannot start a load for a destroyed activity"
tags:
  - android
  - error-log
---

Glide 관련 된 처음보는 오류가 발생했다.

`You cannot start a load for a destroyed activity`

다행히(?) 예전에 이슈가 된 에러였다.([https://github.com/bumptech/glide/issues/803](https://github.com/bumptech/glide/issues/803))

이런 에러가 발생한 이유는 `with()` 함수가 lifecycle을 따르기 때문이다. 즉 Glide가 이미지가 로드 중 `Glide.with()`의 `with()`에 들어간 인자가 activity 또는 fragment가 destroyed되어 위의 에러가 발생한 것이다.

---

**Reference**

- [https://stackoverflow.com/questions/31964737/glide-image-loading-with-application-context/32887693#32887693](https://stackoverflow.com/questions/31964737/glide-image-loading-with-application-context/32887693#32887693)

- [https://eso0609.tistory.com/72](https://eso0609.tistory.com/72)

- [https://github.com/bumptech/glide/issues/803](https://github.com/bumptech/glide/issues/803)
