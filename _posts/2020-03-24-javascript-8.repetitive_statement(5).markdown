---
layout: post
title:  "2020-03-24-[javascript]-8.repetitive_statement(5)"
subtitle:   "2020-03-24 javascript study repetitive_statement(5) "
categories: devlog
tags: javascript

---


## 반복문(5) <br/>


#### 연습



<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>


#### 반복문 연습과 퀴즈

#### 함수를 만들어보자!


- 파라미터로 숫자로 이루어진 배열을 가지고 올것!
- 배열을 넣어주면은 배열의 값을 모두 합하는 함수를 실행!
- 결과는 result라는 값에다가 함수의 결과물을 넣어줄것!


```
function sumOf(numbers) {


  let sum = 0;
  for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
  }
  return sum;
}

const result = sumOf([1, 2, 3, 4, 5]);
console.log(result);

```

<img style="float: left;" src="https://user-images.githubusercontent.com/49095304/77408635-5f38d380-6dfb-11ea-9b2c-4d7602a2aecb.JPG" width="500"/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/>

<br/>

<hr style="height: 1px; background: skyblue; "/>

<br/>


#### 퀴즈

- 숫자로 이루어진 배열이 주어졌을 때, 해당 숫자 배열안에 들어있는 숫자 중 <br/>
3보다 큰 숫자로만 이루어진 배열을 새로 만들어서 반환해보세요.

```

function biggerThanThree(numbers) {
  /* 구현해보세요 */
}

const numbers = [1, 2, 3, 4, 5, 6, 7];
console.log(biggerThanThree(numbers)); // [4, 5, 6, 7]

```

#### 답!!

```

function biggerThanThree(numbers) {
  const array = [];

  for (let i = 0; i < numbers.length; i++){
    if(numbers[i] > 3) {
      array.push(numbers[i]);
    }
  }
  return array;
}

const numbers = [1, 2, 3, 4, 5, 6, 7];
console.log(biggerThanThree(numbers)); // [4, 5, 6, 7]

```



<img style="float: left;" src="https://user-images.githubusercontent.com/49095304/77408839-aaeb7d00-6dfb-11ea-8d2b-6fff0762c673.jpg" width="1000"/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/>
