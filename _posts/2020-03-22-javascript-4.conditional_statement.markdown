---
layout: post
title:  "2020-03-22-[javascript]-4.conditional statement"
subtitle:   "2020-03-20 javascript study conditional statement "
categories: devlog
tags: javascript

---


## 조건문

- 특수한 상황에 특정 작업문 실행 가능


<hr style="height: 1px; background: skyblue; "/>

#### if문

```

const a = 0;
if (a + 1 === 2) {
  console.log("a + 1 이 2입니다.");
}

```

> Console was cleared

```

const a = 1;
if (a + 1 === 2) {
  console.log("a + 1 이 2입니다.");
}

```

> a + 1 은 2입니다.

<br/>

#### 다른 블록 범위에서는 똑같은 이름으로 변수 선언 가능하다!

```

const a = 1;
if (a + 1 === 2) {
  const a = 2;
  console.log("if문 안의 a 값은 " + a);
}

console.log("if문 밖의 a 값은" + a);

```

> if문 안의 a 값은 2 <br/>
> if문 밖의 a 값은 1

#### var를 추천하지 않는 이유!

```

var a = 1;
if (a + 1 === 2) {
  var a = 2;
  console.log("if문 안의 a 값은 " + a);
}

console.log("if문 밖의 a 값은 " + a);

```

> if문 안의 a 값은 2 <br/>
> if문 밖의 a 값은 2

<hr style="height: 1px; background: skyblue; "/>

#### if ~ else

```

const a = 10;

if (a > 15) {
  console.log("a 가 15보다 큽니다");
} else {
  console.log("a 가 15보다 크지 않습니다.");
}

```

> a가 15보다 크지 않습니다.

<hr style="height: 1px; background: skyblue; "/>

#### if ~ else if

```

const a = 7;

if(a === 5) {
  console.log('5 입니다');
} else if (a === 10) {
  console.log('10 입니다.');
} else {
  console.log('5도 아니고 10도 아닙니다');
}

```

> 5도 아니고 10도 아닙니다.

- 첫 번째 두 번째 도 비교해서 아니었기 때문에 세 번째 출력


```

const a = 7;

if (a === 5) {
  console.log("5 입니다");
} else if (a === 10) {
  console.log("10 입니다.");
} else if (a === 7) {
  console.log("7 입니다.");
} else {
  console.log("5도 아니고 10 도 아닙니다. 7도 아니네요");
}

```

 <hr style="height: 1px; background: skyblue; "/>

#### switch~ case

- 특정 값이 무엇이냐에 따라 작업문을 실행

```

const device = "iphone";

switch (device) {
  case "iphone":
    console.log("iphone");
    break;
  case "ipad":
    console.log("ipad");
    break;
  case "galaxy note":
    console.log("galaxy note");
    break;
  default:
    console.log("모르겠네요...");
}

```

> iphone

#### break가 빠지면

```

const device = "iphone";

switch (device) {
  case "iphone":
    console.log("iphone");

  case "ipad":
    console.log("ipad");

  case "galaxy note":
    console.log("galaxy note");

  default:
    console.log("모르겠네요...");
}

```

> iphone <br/>
> ipad <br/>
> galaxy note <br/>
> 모르겠네요...
