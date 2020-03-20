---
layout: post
title:  "2020-03-20-[javascript]-2. variable"
subtitle:   "2020-03-20 javascript study variable"
categories: devlog
tags: javascript

---

#### 변수

```

let value = 1;

```

- let 이라는 keyword로 변수 선언 <br/>

##### 특정 이름의 특정 값을 담는 것 = 선언
##### 이제부터 value 는 1이야!

```

value = 2;
console.log(value);

```

- 변수 선언 주의점
	- 한번 선언하였으면 똑같은 이름으로 선언 불가능

```

let value = 2;

```

>SyntaxError: /src/index.js:
>Identifier 'value' has already been declared (16:4)

<hr style="height: 1px; background: skyblue; "/>

#### 상수

- const

```
const a = 1;

```

> 한번 설정하면 바꿀 수 없다.

```

a = 2;

```

> Error: "a" is read-only


<br/>

#### var
- variable

```

var d = 1;
var d = 2;

```

- 구형 브라우저에서는 var를 사용
- 그러나 보통 babel을 이용하면 구형 브라우저에서 사용 가능하기에 <br/>
	let, const 사용하여도 상관 없음

<br/>

<hr style="height: 1px; background: skyblue; "/>

#### 문자열 선언

```

let text = 'hello';
console.log(text);

```

> hello

```

let name = "헬로우 자바스크립트";
console.log(name);

```

> 헬로우 자바스크립트

<hr style="height: 1px; background: skyblue; "/>

#### boolean

```

let good = true;
let loading = false;


```

- null 과 undefined 은 다름!
	- 둘 다 없음을 의미하지만

```

let good2 = null;

```

> 진짜 없다

```

let something = undefined;

```

> 아직 정해지지 않았다.


```

let friend = null;
// 난 친구가 없어

let criminal;
console.log(criminal);
// undefined

```
