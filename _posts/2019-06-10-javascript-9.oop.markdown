---
layout: post
title:  "06-10-[javascript]-9.oop"
subtitle:   "0610-js-oop"
categories: devlog
tags: javascript

---

## oop

<hr style="height: 1px; background: skyblue; "/>

#### object

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>객체 생성 00_object.html</title>
<script type="text/javascript">

/*
	객체 리터럴

	장점 : 별도의 클래스 선언 같은 구조 없음 -> 구성 자유롭다
	단점 : 구조가 미리 정의가 없으므로 구조 파악이 어렵다
			재사용이 불가능
*/




	// 1- 방식
	var obj = {};

	obj.name= '홍길자'; // 멤버 변수
	obj.age = '23'; // 멤버 변수
	obj.display = function(){ // 멤버 함수
// 		obj.['display'] = function(){
		return this.name +"님은" + this.age+'세입니다.';
	}
	console.log(obj.display())

	// 2- 방식
	var obj2 = {name:'홍길동',age:33};
	obj2.display = function(){
		return this.name +"님은" + this.age+'세입니다.';
	}
	console.log(obj2.display())

	// 3-방식
	var obj3 = new Object();
	obj3.name = '홍길순';
	obj3['age']=44;
	console.log(obj3);

	var out ='';
	out += '이름:' + obj3['name'] + '<br/>';
	out += '나이:' + obj3.age + '<br/>';
	document.write(out);

	var out = '';
	with(obj3){
		out += '이름2:' + name + '<br/>';
		out += '나이2:' + age + '<br/>';
	}
	document.write(out);
	</script>


</head>
<body>

</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### prototype

~~~

<!DOCTYPE HTML>
<html>
<head>
<meta charset="UTF-8">
<title>Javascript 객체지향</title>
<script type="text/javascript">
	// 1. 클래스 선언 - 생성자 함수를 이용
	//		변수명을 첫글자 대문자로 권장

	var Student = function(name, kor, eng, math) {
		this.name = name;
		this.kor = kor;
		this.eng = eng;
		this.math = math;

		/* this.sum = function(){
			return kor+eng+math;} */
	}

	// 동적메소드 추가 -> prototype 선언

	Student.prototype.display = function() {
		return this.name + '님' + this.kor + '/' + this.eng + '/' + this.math;
	}

	/* Student.prototype.sum = function(){
		return this.kor+this.eng+this.math;
	} */
	Student.prototype = {
		sum : function() {
			return this.kor + this.eng + this.math;
		},
		display : function() {
			return this.name + '님' + this.kor + '/' + this.eng + '/'
					+ this.math;
		}
	}

	var s1 = new Student('홍길동', 90, 80, 70);
	document.write(s1.name + '총점:' + s1.sum() + '<br/>');

	//s1.['display'] = function(){
	//	return this.name +'님' + this.kor+'/'+this.eng+'/'+this.math;
	//}
	document.write(s1.display());

	var s2 = new Student("홍길자", 88, 77, 66);
	document.write(s2.name + '총점:' + s2.sum() + '<br/>');
	document.write(s2.display() + '<br/>'); // 동적추가 메소드 호출

	console.log(s1);
	console.log(s2);
</script>


</head>
<body>
	<script>

	</script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### inherit

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title> Javascript 객체지향  - 상속 </title>
</head>
<body>
	<script>
		// 부모클래스
		var Animal = function(){ };
		Animal.prototype = {
			sound : function(){
				document.writeln('울부짖다 <br/>');
			},
			move : function() {
				document.writeln('동물은 움직인다 <br/>');
			}
		};

		// 자식클래스
		var Dog = function(){};
		Dog.prototype = new Animal(); // 상속

		var dog = new Dog(); // 객체 생성
		dog.move();
		Dog.prototype.sound = function(){ // 오버라이딩
			document.writeln('멍멍 짓다<br/>');
		}
		dog.sound(); // 재정의한 것이 불려짐

		Dog.prototype.tail = function(){ // 추가
			document.writeln('꼬리를 흔든다<br/>');
		}
		dog.tail();

	</script>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>
