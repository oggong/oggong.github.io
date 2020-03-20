---
layout: post
title:  "2020-03-20-[javascript]-3.operator"
subtitle:   "2020-03-20 javascript study operator"
categories: devlog
tags: javascript

---


## 연산자

<hr style="height: 1px; background: skyblue; "/>

- 프로그래밍 언어에서 특정 연산을 할 때 사용하는 문자

```

let value = 1;


```

- = 이것은 대입 연산자
- value에 1을 넣겠다

<hr style="height: 1px; background: skyblue; "/>

#### 산술 연산자
- 사칙 연산을 하는 연산자

```

let a = 1 + 2;
console.log(a);

```

> 3

```

let b = 1 + 2 - (3 * 4) / 4;
console.log(b);

```

> 0

#### ++

```

let a = 1;

console.log(a++);
console.log(a);
console.log(++a);

```

> 1
> 2
> 3

- a++ 과 ++a 의 차이

```

let a = 1;
console.log(a--);
console.log(a);

```

- -- 도 가능

<hr style="height: 1px; background: skyblue; "/>

#### 대입 연산자

```

let a = 1;
a += 3;
a -= 3;
a *= 3;
a /= 3;
console.log(a);

```

> 1

<hr style="height: 1px; background: skyblue; "/>

#### 논리 연산자

##### NOT = !

```

const a = !true;
console.log(a);

```

> false

##### AND &&

```

const b = true && true;
console.log(b);

```

> true

```

const c = true && false;
console.log(c);

```

> false

##### OR ||

```

const d = true || true;
console.log(d);

```

> true

```

const e = false || true;
console.log(e);

```

> true

- 사칙 연산처럼 NOT-AND-OR 부터 연산한다.

```

const value = !(true && false || true && false || ! false);

```

> NOT - AND - OR
> !(true && false || true && false || true)
> !(false || false || true)
> !(false || true)
> !(true)
> false

- 코드 샌드박스에서는 ctrl + s 로 저장하면서 동시에 코드가 정리 된다

> ex) const value = !((true && false) || (true && false) || !false);

<hr style="height: 1px; background: skyblue; "/>

#### 비교 연산자

```

const a = 1;
const b = 1;
const equals = a === b;
console.log(equals);

```

> true

- == 와 === 의 차이
	- == 는 type 구별을 하지 않음
	- === 는 type 까지 구별해줌


```

const a = true;
const b = 1;
const equals = a == b;
console.log(equals);

```

> true

```

const a = true;
const b = 1;
const equals = a === b;
console.log(equals);

```

> false

```

const a = null;
const b = undefined;
const equals = a === b;
console.log(equals);

```

> false

- 결론은 === 을 주로 쓰는 게 좋다는 강사의 조언!
	- 더 유용


```

const a = 'a';
const b = 'b';
const notEquals = a !== b;
console.log(notEquals);

```

> true

<hr style="height: 1px; background: skyblue; "/>

#### 대소 비교

```

const a = 10;
const b = 15;
const c = 15;

console.log(a < b);

console.log(b < a);

console.log(b >= a);

console.log(a <= c);

console.log(b < c);


```

> true
> false
> true
> true
> false

<hr style="height: 1px; background: skyblue; "/>

#### 문자열 붙이기

```

const a = '안녕';
const b = '하세요';
console.log(a + b);

```

> 안녕하세요
