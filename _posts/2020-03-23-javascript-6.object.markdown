---
layout: post
title:  "2020-03-23-[javascript]-6.object"
subtitle:   "2020-03-23 javascript study object "
categories: devlog
tags: javascript

---


## 객체 <br/>

- 우리가 어떤 값을 선언하게 될 때 하나의 이름에 여러 종류의 <br/>
	값을 넣을 수 있게 해준다.

<hr style="height: 1px; background: skyblue; "/>

<br/>

- 예를 들어 강아지의 값을 넣을때

```

const dogName = '멍멍이';
const dogAge = 2;

console.log(dogName);
console.log(dogAge);

```

> 멍멍이 <br/>
> 2

<p>이런식을 넣었다면,</p>

<br/>


```

// const dog = {
//   이름: 값
// }

const dog = {
  name: '멍멍이',
  age: 2,
  cute: true,
  sample: {
    a: 1,
    b: 2,
  }
}

```

- 이렇게 객체 생성 가능하다! <br/>

```

const dog = {
  name: '멍멍이',
  age: 2,
}

console.log(dog);
console.log(dog.name);
console.log(dog.age);

```

> key : value 형식 <br/>
> key에 공백이 있으면 안되지만 "" 감싸서 사용할 수 있다.

```

const dog = {
  name: '멍멍이',
  age: 2,
  'key with space': 'asdf',
}

console.log(dog);
console.log(dog.name);
console.log(dog.age);

```

> Object {name: "멍멍이", age: 2, key with space: "asdf"} <br/>
> 멍멍이 <br/>
> 2

<br/>

<hr style="height: 1px; background: skyblue; "/>


#### 연습 <br/>

```

const ironMan = {
  name: "토니 스타크",
  actor: "로버트 다우니 주니어",
  alias: "아이언맨"
};

const captainAmerica = {
  name: "스티브 로저스",
  actor: "크리스 에반스",
  alias: "캡틴 아메리카"
};

console.log(ironMan);
console.log(captainAmerica);

```

<br/>

> Object {name: "토니 스타크", actor: "로버트 다우니 주니어", alias: "아이언맨"} <br/>
> Object {name: "스티브 로저스", actor: "크리스 에반스", alias: "캡틴 아메리카"}

<br/>

#### print 함수를 만들어서 출력해보자 <br/>

```

const ironMan = {
  name: "토니 스타크",
  actor: "로버트 다우니 주니어",
  alias: "아이언맨"
};

const captainAmerica = {
  name: "스티브 로저스",
  actor: "크리스 에반스",
  alias: "캡틴 아메리카"
};

function print(hero) {
  const text = `${hero.alias}(${hero.name}) 역할을 맡은 배우는 ${
    hero.actor
  } 입니다`;
  console.log(text);
}

print(ironMan);
print(captainAmerica);

```

> 아이언맨(토니 스타크) 역할을 맡은 배우는 로버트 다우니 주니어입니다  <br/>
> 캡틴 아메리카(스티브 로저스) 역할을 맡은 배우는 크리스 에반스입니다

<br/>

<hr style="height: 1px; background: skyblue; "/>

#### 비구조화 할당 <br/>

 - 객체 구조 분해 라고도 한다!

 ```

 function print(hero) {
  const text = `${hero.alias}(${hero.name}) 역할을 맡은 배우는 ${
    hero.actor
  } 입니다`;
  console.log(text);
}

```

<br/>
- 이 부분의 hero.alias 처럼 기입 하는 것을 es6 비구조화 할당으로 편리하게 사용

<br/>

```

const ironMan = {
  name: "토니 스타크",
  actor: "로버트 다우니 주니어",
  alias: "아이언맨"
};

const captainAmerica = {
  name: "스티브 로저스",
  actor: "크리스 에반스",
  alias: "캡틴 아메리카"
};

function print(hero) {
  const { alias, name, actor } = hero;
  const text = `${alias}(${name}) 역할을 맡은 배우는 ${
    actor
  } 입니다`;
  console.log(text);
}

print(ironMan);
print(captainAmerica);

```

> 아이언맨(토니 스타크) 역할을 맡은 배우는 로버트 다우니 주니어입니다  <br/>
> 캡틴 아메리카(스티브 로저스) 역할을 맡은 배우는 크리스 에반스입니다

<br/>

- 비구조화 할당은 특정 값들을 객체에서 빼온다!!
- 더 간결하게 작성 가능

<br/>

```

function print({ alias, name, actor }) {
  const text = `${alias}(${name}) 역할을 맡은 배우는 ${
    actor
  } 입니다`;
  console.log(text);
}


```

<br/>

```

const ironMan = {
  name: "토니 스타크",
  actor: "로버트 다우니 주니어",
  alias: "아이언맨"
};

const { name } = ironMan;
console.log(name);

```

> 토니 스타크

<br/>

- 이렇게도 쓰일 수 있다.

<hr style="height: 1px; background: skyblue; "/>


#### 객체 안에 함수 넣기 <br/>

```

const dog = {
  name: "멍멍이",
  sound: "멍멍!",
  say: function say() {
    console.log(this.sound);
    // this = 함수가 위치한 객체를 가리킴!
  }
};

dog.say();

```

> 멍멍!

<br/>

- 이런 방식으로도 가능하다!

```

const dog = {
  name: "멍멍이",
  sound: "멍멍!",
  say() {
    console.log(this.sound);
    // this = 함수가 위치한 객체를 가리킴!
  }
};

dog.say();

```

> 멍멍!

#### 화살표 함수 불가능!!

```

const dog = {
  name: "멍멍이",
  sound: "멍멍!",
  say: () => {
    console.log(this.sound);
    // this = 함수가 위치한 객체를 가리킴!
  }
};

dog.say();

```

<br/>

```

const dog = {
  name: "멍멍이",
  sound: "멍멍!",
  say: function() {
    console.log(this.sound);
    // this = 함수가 위치한 객체를 가리킴!
  }
};

dog.say();


const cat = {
  name: '야옹이',
  sound: '야옹~',
};

cat.say = dog.say;
dog.say();
cat.say();

const catSay = cat.say;
catSay();

```

> 멍멍! <br/>
> 야옹~ <br/>
> TypeError: Cannot read property 'sound' of undefined

- this는 속해 있는 객체에서만 불려질 수 있음

<br/>

<hr style="height: 1px; background: skyblue; "/>


#### 객체 getter, setter <br/>

```

const numbers = {
  a: 1,
  b: 2,
 }
};

numbers.a = 5;
console.log(numbers);

```

> Object {a: 5, b: 2}

<br/>

#### getter <br/>

```

const numbers = {
  a: 1,
  b: 2,
 // getter
  get sum() {
    console.log('sum 함수가 실행됩니다!');
    return this.a + this.b;
  }
};

console.log(numbers.sum);

```

- 조회만 해도 함수가 실행!!

<br/>

```

numbers.b = 5;
console.log(numbers.sum);


```

- 특정 값을 조회하려고 할때 특정 코드를 실행 시키고, 연산된 값을 받아서 사용할 수 있는 것!

> sum 함수가 실행됩니다! <br/>
> 3 <br/>
> sum 함수가 실행됩니다! <br/>
> 6 <br/>

#### setter <br/>


```

const dog = {
  _name: '멍멍이',
  // setter
  set name(value) {
    console.log('이름이 바뀝니다 ..' + value);
    this._name = value;
  }
};

console.log(dog._name);

```

> 멍멍이

<br/>

```

const dog = {
  _name: '멍멍이',
  // setter
  set name(value) {
    console.log('이름이 바뀝니다 ..' + value);
    this._name = value;
  }
};

console.log(dog._name);
dog.name = '뭉뭉이';
console.log(dog._name);

```

> 멍멍이 <br/>
> 이름이 바뀝니다 .. 뭉뭉이 <br/>
> 뭉뭉이


<br/>

#### getter , setter 둘다 사용 하기 <br/>

```

// getter를 같이 써주면 _name을 하지 않아도 됨

const dog = {
  _name: '멍멍이',
  get name() {
    console.log('_name을 조회합니다..');
    return this._name;
  },
  // setter
  set name(value) {
    console.log('이름이 바뀝니다 ..' + value);
    this._name = value;
  }
};

console.log(dog.name);
dog.name = '뭉뭉이';
console.log(dog.name);

```

> _name 을 조회합니다.. <br/>
> 멍멍이 <br/>
> 이름이 바뀝니다 .. 뭉뭉이 <br/>
> _name 을 조회합니다.. <br/>
> 뭉뭉이


<br/>

```

const numbers = {
  _a: 1,
  _b: 2,
  sum: 3,
  calculate() {
    console.log('calculate');
    this.sum = this._a + this._b;
  },
  get a() {
    return  this._a;
  },
  get b() {
    return  this._b;
  },
  set a(value) {
    this._a = value;
    this.calculate();
  },
  set b(value) {
    this._b = value;
    this.calculate();
  }
};

console.log(numbers.sum);
numbers.a = 5;
numbers.b = 7;
numbers.a = 9;
console.log(numbers.sum);
console.log(numbers.sum);
console.log(numbers.sum);

```

- 값이 바뀔때 마다  계산하는 것!!!

> 3 <br/>
> calculate <br/>
> calculate <br/>
> calculate <br/>
> 16 <br/>
> 16 <br/>
> 16 <br/>

<img style="float: left;" src="https://user-images.githubusercontent.com/49095304/77290485-9e91f200-6d1f-11ea-8b0e-65d01d89cfe5.JPG" width="600"/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>



```

const numbers = {
  a: 1,
  b: 2,
  get sum() {
    console.log("sum");
    return this.a + this.b;
  }
};

console.log(numbers.sum);
numbers.a = 5;
numbers.b = 7;
numbers.a = 9;
console.log(numbers.sum);
console.log(numbers.sum);
console.log(numbers.sum);


```

- 조회 할때마다 계산!!

> sum <br/>
> 3 <br/>
> sum <br/>
> 16 <br/>
> sum <br/>
> 16 <br/>


- 결론!!!

- 조회 할때마다 계산하는 것은 비효율적!!
- 그래서 getter 와 setter 를 적절히 사용하는 게 좋다!!
