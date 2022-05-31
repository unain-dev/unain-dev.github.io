---
layout: post
title: "[Next.js] Next.js에서 이미지 import 하기"
categories: React.js
---
## Next.js에서 이미지 import 하는 방법
```
import Image from "next/image";
```

## img 태그를 사용하지 않고 Image를 사용하는 이유
1. Next.js의 Image 태그는 최신 웹용으로 확장된 next/imageHTML img요소이다.

2. 브라우저에서 지원하는 경우 JPEG보다 약 30 % 작은 WebP와 같은 최신 이미지 형식으로 이미지를 자동으로 제공한다.
(필요에 따라 이미지 최적화)

3. 뷰포트를 스크롤하는 동안 특정 임계 값에 도달 한 경우에만 페이지 내부의 이미지를 지연로드한다.

4. 동적으로 사용할 다양한 및 사용자 정의 해상도에 대해 다른 이미지 크기를 지정할 수 있다.

5. 사진의 품질을 75 %로 설정된 낮은 임계 값으로 자동 변경한다
(각 호출에 대해 변경 가능)



## 참고자료 출처
- [[React] NextJS 에서 이미지 import 하기](https://velog.io/@pyo-sh/React-NextJS-%EC%97%90%EC%84%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-import-%ED%95%98%EA%B8%B0){:target="\_blank"}
