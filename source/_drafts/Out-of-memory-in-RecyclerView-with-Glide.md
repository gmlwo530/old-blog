---
title: Out of memory in RecyclerView with Glide
tags:
  - android
---

RecyclerView에서 Out of Memory가 났고, 이유는 Glide에 cache 정책을 제대로 명시하지 않아 발생한 것으로 추측 된다.

그래서 Glide에서 cache 관리는 어떻게 하는지 한 번 정리해보았다.
