---
layout: post
title:  "2020-03-24-[javascript]-8.repetitive_statement(1)"
subtitle:   "2020-03-24 javascript study repetitive_statement(1) "
categories: devlog
tags: javascript

---


## 반복문(1) <br/>

- 이름에서도 유추가 가능하듯
- 특정 작업을 반복적으로 사용할 때!!

<img style="float: left;" src="https://user-images.githubusercontent.com/49095304/77399248-5ee50c00-6dec-11ea-970e-c33bc444f0b3.jpg" width="500"/><br/><br/><br/><br/><br/><br/><br/>
<br/>

#### 반복문은 특정 조건이 만족하는 동안 계속 반복하다가 조건이 만족되지 않으면 끝낸다!

- but 상황에 따라 끝나지 않는 반복문도 있음

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>


### for

<br/>

```

for (let i = 0; i < 10; i++) {
  console.log(i);
}

```
> 0 <br/>
1 <br/>
2 <br/>
3 <br/>
4 <br/>
5 <br/>
6 <br/>
7 <br/>
8 <br/>
9

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 반대로도 가능

<br/>

```

for (let i = 10; i > 0; i--){
  console.log(i);
}

```

> 10 <br/>
9 <br/>
8 <br/>
7 <br/>
6 <br/>
5 <br/>
4 <br/>
3 <br/>
2 <br/>
1

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 2씩 줄이기

```

for (let i = 10; i >= 0; i-=2){
  console.log(i);
}

```

>10 <br/>
8 <br/>
6 <br/>
4 <br/>
2 <br/>
0


<br/>

- 그러나 보통 0부터 시작하는 반복문이 대부분이다!!

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 연습

#### for 문과 배열 같이 쓰기

```

//배열 선언
const names =['멍멍이','야옹이','멍뭉이'];

// names의 사이즈를 알아야 전부 출력

for (let i = 0; i < names.length; i++ ) {
  console.log(names[i]);
}

```

> 멍멍이  <br/>
야옹이  <br/>
멍뭉이 
