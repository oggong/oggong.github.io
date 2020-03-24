---
layout: post
title:  "2020-03-24-[javascript]-7.array"
subtitle:   "2020-03-24 javascript study array "
categories: devlog
tags: javascript

---


## 배열 <br/>

- 객체는 한 변수, 한 상수 안에 여러가지 정보를 담기 위함이었다면!! <br/>
- 배열은 여러개의 항목들이 들어있는 리스트다!!

[ 0, 1, 2, 3];

<hr style="height: 1px; background: skyblue; "/>

<br/>


#### 자바스크립트에서는 배열안의 원소들이 모두 같은 형태일 필요가 없다.

<br/>

<hr style="height: 1px; background: skyblue; "/>


#### 사용법


```

const array = [1, 2, 3, 4, 5];
console.log(array);

```

>[1,2,3,4,5]

<br/>

- 이렇게도 가능!! <br/>

```

const array = [1, "blabla", {}];
console.log(array);

```

> [1, "blabla", Object]


<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 항목별 조회

```

const array = [1, "blabla", {}];
console.log(array);

console.log(array[0]);
console.log(array[1]);
console.log(array[2]);
console.log(array[3]);

```

<br/>

> 1 <br/>
> blabla <br/>
> Object {} <br/>
> undefined


<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 객체로 이루어진 배열

<br/>


```

const objects = [{ name: "멍멍이" }, { name: "야옹이" }];

console.log(objects);
console.log(objects[0]);
console.log(objects[1]);

```

> [Object, Object] <br/>
> Object {name: "멍멍이"} <br/>
> Object {name: "야옹이"}

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>


#### 새로운 항목 추가
#### push (자바스크립트 배열 내장 함수)

<br/>

```

const objects = [{ name: "멍멍이" }, { name: "야옹이" }];

objects.push({
  name: "멍뭉이"
});

console.log(objects);


```

> [Object, Object, Object] <br/>
> 0: Object <br/>
> name: "멍멍이" <br/>
> 1: Object <br/>
> name: "야옹이" <br/>
> 2: Object <br/>
> name: "멍뭉이"

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 배열의 크기를 알아보는 법
#### 몇개가 들어 있는지 확인
#### length(배열 내장 함수)

<br/>

```

const objects = [{ name: "멍멍이" }, { name: "야옹이" }];

console.log(objects.length);

objects.push({
  name: "멍뭉이"
});

console.log(objects);

console.log(objects.length);

```

> 2 <br/>
> [Object, Object, Object] <br/>
> 0: Object <br/>
> name: "멍멍이" <br/>
> 1: Object <br/>
> name: "야옹이" <br/>
> 2: Object <br/>
> name: "멍뭉이" <br/>
> 3

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>

#### 연습

```

const array = [1, true, { a: 1 }, [1, 2, 3, 4]];

array.push(6);

console.log(array);
console.log(array.length);

```

> [1, true, Object, Array[4], 6] <br/>
> 0: 1 <br/>
> 1: true <br/>
> 2: Object <br/>
> a: 1 <br/>
> 3: Array[4] <br/>
> 0: 1 <br/>
> 1: 2 <br/>
> 2: 3 <br/>
> 3: 4 <br/>
> 4: 6 <br/>
> 5
