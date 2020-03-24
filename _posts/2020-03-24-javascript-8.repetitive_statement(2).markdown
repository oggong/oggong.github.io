---
layout: post
title:  "2020-03-24-[javascript]-8.repetitive_statement(2)"
subtitle:   "2020-03-24 javascript study repetitive_statement(2) "
categories: devlog
tags: javascript

---


## 반복문(2) <br/>


#### while

#### 특정 조건이 만족할때 실행을 멈춤

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

```

let i = 0;

while(i < 10) {
  console.log(i);
  i++;
}

```

- 주의할점
  - 여기의 조건이 언젠가는 false가 되게 해야한다
  - 그렇지 않으면 계속 실행 멈추지 않음

<br/>

#### 단순 숫자 비교가 아닌 특정 조건 비교에 사용하기 적합하다.


```

let i = 0;
let isFun = false;

while(isFun === false) {
  console.log(i);
  i++;
  if (i === 30) {
    isFun = true;
  }
}

```

- isFun 이 false 일때까지 반복해라 !!


```

let i = 0;
let isFun = false;

while(!isFun) {
  console.log(i);
  i++;
  if (i === 30) {
    isFun = true;
  }
}

```

- 이렇게도 가능
