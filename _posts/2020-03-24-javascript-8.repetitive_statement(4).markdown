---
layout: post
title:  "2020-03-24-[javascript]-8.repetitive_statement(4)"
subtitle:   "2020-03-24 javascript study repetitive_statement(4) "
categories: devlog
tags: javascript

---


## 반복문(4) <br/>


#### break continue

#### 반복문에서 벗어나거나 그 다음 루프를 돌게 할 수 있다.

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

```

for (let i = 0; i< 10; i++){

  if(i === 2) continue;
  // continue 특정 조건이 만족되었을때 그 다음 루프를 해라!
  // 2가 skip이되고 다음이 출력
  console.log(i);

  if(i === 5) break;
  // break 가 나타나면 반복문이 끝남
}

// if 문 내부에서 실행할때 한줄짜리면 코드를 중괄호 안해도됨!

// continue 그 다음 루프를 돌게하고
// break는 끝낸다

```

#### for 문 이외의 다른곳도 사용 가능!!
