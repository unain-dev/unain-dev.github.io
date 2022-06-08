---
layout: post
title: "[Web] strict mode란?"
categories: Web
---
## strict mode란?
strict 모드는 ES5(ECMA Script 5)에 추가된 키워드입니다.strict 모드는 자바스크립트가 묵인했던 에러들의 에러 메시지를 발생시킵니다. 엄격하게 문법 검사를 하겠다.. 로 이해하면 될 것 같습니다.

strict 모드는 문법과 런타임 동작을 모두 검사하여, 실수를 에러로 변환하고, 변수 사용을 단순화(Simplifying) 시켜줍니다.

### strict mode 선언(설정)
스크립트의 시작 혹은 함수의 시작 부분에 "use strict"(또는 'use strict')를 선언하면 strict 모드로 코드를 작성 할 수 있습니다.

```javascript
"use strict";
var v = "Hi!  I'm a strict mode script!";
```

```javascript
function strict(){
  // Function-level strict mode syntax
  'use strict';
  function nested() { return "And so am I!"; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
function notStrict() { return "I'm not strict."; }
```

## strict mode 특징
### 실수를 에러로 변환(Converting mistakes into errors)
자바스크립트는 오류를 어느정도 무시하고 넘어갈 수 있습니다. 이것이 편하게 코딩을 할 수 있게 하지만, 때로는 심각한 버그를 만들게 됩니다. strict 모드는 이러한 실수를 에러로 변환하여 즉시 수정할 수 있게 합니다.
![image](https://user-images.githubusercontent.com/28949166/172599605-e99fdf9d-f7ad-423d-85cd-c56338becf1d.png)
> 선언하지 않고 전역 변수를 만들 수 없습니다.

![image](https://user-images.githubusercontent.com/28949166/172599707-e376116d-cb99-4449-80bf-7f0b0600f03f.png)
> writable이 false로, 읽기 전용 객체에 쓰는 것이 불가능 합니다. (read only 객체 수정 불가능)

![image](https://user-images.githubusercontent.com/28949166/172599728-653a7218-34a0-4d92-90e6-65c6df84c9ee.png)
> get으로 선언된 객체는 수정할 수 없습니다. (getter-only property 수정 불가능)

![image](https://user-images.githubusercontent.com/28949166/172599784-ad9a188b-c27d-4a4f-ad2d-9dacb0d3e74e.png)
> extensible 특성이 false로 설정된 객체에 속성을 확장 할 수 없습니다. (확장 불가 객체 확장 불가능)

![image](https://user-images.githubusercontent.com/28949166/172599808-866a5cbb-6102-4051-b188-eba6d2c495a9.png)
> delete를 호출 할 수 없습니다.

![image](https://user-images.githubusercontent.com/28949166/172599875-34a96394-e1c9-4eae-95c8-4d1beb94f931.png)
> 함수의 동일한 매개 변수 이름을 선언하는 것이 불가능 합니다.

### 변수 사용의 명료화(Simplify variable uses)
strict 모드는 변수 이름의 맵핑을 단순화 합니다.대부분의 컴파일러의 최적화는 변수의 매핑에 달려 있습니다. 자바스크립트 또한 변수의 매핑이 최적화의 크리티컬 이슈입니다. strict 모드를 사용하여 자바스크립트를 최적화 할 수 있습니다.

![image](https://user-images.githubusercontent.com/28949166/172600125-83d5f3b1-2203-45db-88fb-e05660cebaed.png)
? with 블록 안에 name은 전역 변수의 name인지 foo의 name인지 모호합니다. 그렇기 때문에 strict 모드에서는 with를 사용하는 것이 불가능합니다.

### eval과 arguments 명료화(Making eval and arguments simpler)
strict 모드는 eval과 arguments 사용을 더욱 명료하게 사용 할 수 있게 합니다.

![image](https://user-images.githubusercontent.com/28949166/172600210-dee3d6c1-36ff-4690-a683-112b3e94f6c7.png)
> eval을 변수 또는 함수, 매개 변수의 이름으로 사용할 수 없습니다.

![image](https://user-images.githubusercontent.com/28949166/172600304-7bece3d2-c6b8-48a8-81f9-156edfd68cbc.png)
> arguments를 변수 또는 함수, 매개 변수의 이름으로 사용할 수 없습니다


### 안전한 자바스크립트("Securing" JavaScript)
strict 모드를 사용하면 보안에 강한 자바스크립트를 작성할 수 있습니다. 일부 웹 사이트에서 사용자에게 자바스크립트를 작성할 수 있는 기능을 제공합니다. 이 때 사용자가 작성한 자바스크립트는 부분적으로 접근을 금지해야 합니다. 접근을 막기 위하여 런타임에 체크를 한다면 비효율적인 코드가 됩니다. 이러한 문제를 strict 모드를 사용하여 해결 할 수 있습니다.

![image](https://user-images.githubusercontent.com/28949166/172600378-6243fd5c-3c3b-4da8-80a9-3408e7d8aa1e.png)
> this의 값이 null 또는 undefined인 경우 전역 객체로 변환하지 않습니다.


### 미래의 자바스트립트 준비(Paving the way for future ECMAScript versions)
strict 모드는 미래의 자바스크립트 버전 도입을 위하여 몇가지 제한 사항을 적용합니다. strict 모드로 몇가지를 제한 하기 때문에, 추후의 자바스크립트 버전에 적용하기 쉽습니다. 즉 향후 업데이트 될 자바스크립트 버전 대응이 용이합니다.

![image](https://user-images.githubusercontent.com/28949166/172599943-c748a952-f32b-4c13-90f2-6ceb5cb28424.png)
> 예약된 키워드의 이름으로 변수 또한 함수를 생성할 수 없습니다.



## 참고자료 출처
- [[자바스크립트] 엄격 모드(strict mode)](https://velog.io/@wiostz98kr/HTTP1.1%EA%B3%BC-HTTP2.0%EC%9D%98-%EC%B0%A8%EC%9D%B4-e2v4x4t1](https://beomy.tistory.com/13){:target="\_blank"}
