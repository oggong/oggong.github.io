---
layout: post
title:  "2020-03-24-[javascript]-8.repetitive_statement(3)"
subtitle:   "2020-03-24 javascript study repetitive_statement(3) "
categories: devlog
tags: javascript

---


## 반복문(3) <br/>


#### for of, for in

#### 배열을 다루게 될때 주로 사용
#### 배열 안에 있는 것들을 사용해서 어떠한 작업들을 할때 이용!

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

```

const numbers = [10,20,30,40,50];

for (let number of numbers) {
  console.log(number);
}

```

> 10 <br/>
20 <br/>
30 <br/>
40 <br/>
50

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### for of 가 헷갈릴 수 있는 이유는 for in 이 있기 때문!!

#### for in 은 객체에 대한 반복작업을 해야할 경우에 사용!!

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

- 먼저 객체의 정보를 배열 형태로 받아오는 방법을 알아보자!


```

const numbers = [10, 20, 30, 40, 50];

const doggy = {
  name: "멍멍이",
  sound: "멍멍",
  age: 2
};

// key값 보여지기
console.log(Object.keys(doggy));

// values 값 보여지기
console.log(Object.values(doggy));

// entries // key와 values 값을 같이 보여지기
console.log(Object.entries(doggy));

```

> ["name", "sound", "age"] <br/>
0: "name" <br/>
1: "sound" <br/>
2: "age" <br/>
["멍멍이", "멍멍", 2] <br/>
[Array[2], Array[2], Array[2]] <br/>
0: Array[2] <br/>
0: "name" <br/>
1: "멍멍이" <br/>
1: Array[2] <br/>
0: "sound" <br/>
1: "멍멍" <br/>
2: Array[2] <br/>
0: "age" <br/>
1: 2 <br/>

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### for in

```

const doggy = {
  name: "멍멍이",
  sound: "멍멍",
  age: 2
};


for (let key in doggy) {
  console.log(key);
}


```

> name <br/>
sound <br/>
age


#### key value 모두 출력

```

const doggy = {
  name: "멍멍이",
  sound: "멍멍",
  age: 2
};

for (let key in doggy) {
  console.log(`${key} : ${doggy[key]}`);
}


```

#### template literal 사용!!

> name : 멍멍이  <br/>
sound : 멍멍  <br/>
age : 2 
