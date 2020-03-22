---
layout: post
title:  "2020-03-22-[javascript]-5.function"
subtitle:   "2020-03-22 javascript study function "
categories: devlog
tags: javascript

---


## 함수

<img style="float: left;" src="https://user-images.githubusercontent.com/49095304/77245685-c6238480-6c63-11ea-9637-2652ad5a0857.JPG" width="300"/><br/><br/><br/><br/><br/><br/><br/><br/><br/>


<hr style="height: 1px; background: skyblue; "/>


#### 특정값들의 합을 구하는 함수를 만들어보자!

```

const a = 1;
const b = 2;

const sum =  a + b;

```

#### function으로 만들어보자!

```

function 함수이름 (파라미터) {

	return 결과값;
}

```

- 파라미터 = 넣는 값 <br/>
- return = 반환 = 결과값으로 내주겠다

```

function add(a, b) {
  return a + b;
}

const sum = add(1, 2);
console.log(sum);

```

> 3

```

unction hello(name) {
  console.log("Hello. " + name + "!");
}
hello("function");

```

> Hello. function!


<hr style="height: 1px; background: skyblue; "/>

#### Template literal

- ES6 부터 사용하기 시작하였다!
    - 자바스크립트 버전으로 2015년에 만들어졌다
    - ES2015 라고도 불린다

> ES7 = 2017 <br/>
> ES8 = 2018 <br/>
> ES9 = 2019 <br/>
> ES10 = 현재 여기까지 만들어졌다

- ES6 에서 큰 변화가 있었고 그 이후로는 조금씩의 변화가 있었음

```

function hello(name) {
  console.log(`hello ${name}!`);
} hello('template literal');

```

> hello template literal!

```

` ${parameter}`

```

#### returun 이후 함수 실행이 안된다.

```

function hello(name) {
  return `hello ${name}!`;
  console.log('a');
}

const result = hello('template literal');
console.log(result);

```

> hello template literal!

- a 는 출력되지 않음

<hr style="height: 1px; background: skyblue; "/>

#### function 연습~

```

function getGrade(score) {
  if (score === 100) {
    return "A+";
  } else if (score >= 90) {
    return "A";
  } else if (score === 89) {
    return "B+";
  } else if (score >= 80) {
    return "B";
  } else if (score === 79) {
    return "C+";
  } else if (score >= 70) {
    return "C";
  } else if (score === 69) {
    return "D+";
  } else if (score >= 60) {
    return "D";
  } else {
    return "F";
  }
}

const grade = getGrade(100);
console.log(grade);

```

> A+


<hr style="height: 1px; background: skyblue; "/>

#### 화살표 함수

```

const 함수명 = (파라미터) => {}

```

- es6 이후로 사용되기 시작함


```

const add = (a, b) => {
  return a + b;
};

const hello = name => {
  console.log(`Hello ${name}!`);
};

const sum = add(1, 2);
console.log(sum);

hello("arrow function");

```

> 3 <br/>
> hello arrow function!

#### 함수 내부에서 바로 return 가능!

```

const add = (a, b) => a + b;
const sum = add(1, 2);
console.log(sum);

```

> 3

<hr style="height: 1px; background: skyblue; "/>
