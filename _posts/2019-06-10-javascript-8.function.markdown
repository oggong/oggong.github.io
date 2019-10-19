---
layout: post
title:  "06-10-[javascript]-8.function"
subtitle:   "0610-js-function"
categories: devlog
tags: javascript

---

## function

<hr style="height: 1px; background: skyblue; "/>

#### kinds_of_func (1)

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title>자바스크립트 함수 3가지</title>
	<script>

	// 1. function 명령
	function triangle(base,height){
		return base * height /2;

	}
	document.write('삼각형의 넓이:' + triangle(3,4)+"<br/>");


	// 2. Function 생성자 이용
	var triangle2 = new Function('base','height','return base * height / 2');

	document.write('삼각형의 넓이2:' + triangle2(3,4)+"<br/>");

	// 3. 함수 리터럴 (*리터럴 : 변수의 값)
	var triangle3 = function(base,height){
		return base * height / 2;

	}
	document.write('삼각형의 넓이3:' + triangle3(3,4)+'<br/>');

	</script>
</head>

<body>


 </body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### kinds_of_func (2)

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title>자바스크립트 함수 만들기</title>
	<script>
	//1. function 명령어 - first() 완성
		function first(){
		var txt = document.getElementById('first');
		txt.style.backgroundColor=('red');
		txt.style.color='yellow';
	}
	//2. function 생성자 - second() 완성
		var second = new Function("var txt = document.getElementById('second');txt.style.backgroundColor=('red');txt.style.color='yellow';");

	//3. 함수 리터럴 - third() 완성
	var third = function(){
			var txt = document.getElementById('third');
			txt.style.backgroundColor=('red');
			txt.style.color='yellow';
	}

	</script>
</head>

<body>
	<p> <span id="first"> function 명령 </span>
		<input type="button" value="확인" onclick="javascript:first()"/>
	</p>
	<p> <span id="second"> Function 생성자 </span>
		<input type="button" value="확인" onclick="javascript:second()"/>
	</p>
	<p> <span id="third"> 함수 리터럴 </span>
		<input type="button" value="확인" onclick="javascript:third()"/>
	</p>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### function

~~~

<!DOCTYPE HTML>
<html>
<head>
<meta charset="UTF-8">
<title>리터럴 함수</title>
</head>
<body>
	<script>
		/* 		###1. function 명령은 정적인 구조
		 // function 생성자와 함수 리터럴은 실행시 판단한다.
		 // 반드시 선언을 먼저 해야 한다

		 // 1. function 명령
		 document.write('삼각형의 넓이:' + triangle(3, 4) + "<br/>");
		 function triangle(base, height) {
		 return base * height / 2;

		 }

		 // 2. Function 생성자 이용

		 var triangle2 = new Function('base', 'height',
		 'return base * height / 2');
		 document.write('삼각형의 넓이2:' + triangle2(3, 4) + "<br/>");
		 // 3. 함수 리터럴 (*리터럴 : 변수의 값)
		 var triangle3 = function(base, height) {
		 return base * height / 2;
		 document.write('삼각형의 넓이3:' + triangle3(3, 4) + '<br/>');
		 */

		/* '####[2] 함수도 데이타 타입(자료형)이다' */

		var triangle3 = function(base, height) {
			return base * height / 2;
		}
		document.write('삼각형의 넓이3:' + triangle3(3, 4) + '<br/>');
		document.write('함수:' + triangle3 + "<br/>");
		triangle3 = 10000;
		document.write('변수:' + triangle3 + "<br/>");
		/* '####[3] 함수도 배열에 저장'  */
		function doA() {
			document.write('함수 A <br/>');
		}
		function doB() {
			document.write('함수 B <br/>');
		}
		var arr = [ doA, doB ];
		document.write('함수 배열:' +arr+'<br/>');

		// 호출 ???
		arr[0]();
		arr[1]();



	</script>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>


#### argument

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>함수의 인자</title>
</head>
<script type="text/javascript">
		/*#### 1. 함수의 인자는 개수를 체크하지 않는다  */
	function multiple(first,second){
			return first*second;

		}
	document.write('곱 1:' +multiple(2,4)+"<br/>");
	document.write('곱 2:' +multiple(2,3,4)+"<br/>");
	document.write('곱 3:' +multiple(2)+"<br/>");
		//multiple(2) 2 X undefined 로 되어 Not A Number 출력

	/* ### 2. 여러개의 인자(파라미터)를 익명의 객체로 받음  */

	function mul(args){
			return args.first * args.second;
		}
		document.write('곱 :' +mul({first:3,second:4})+'<br/>');

	/* ### 3. arguments 특별한 객체  */
	function func(){
		//document.write(arguments + '<br/>');
		console.log(arguments);
	}
	func(1);
	func(2,3);
	</script>
<body>

</body>
</html>



~~~

<hr style="height: 1px; background: skyblue"/>

#### valuable

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title>자바스크립트 변수와 범위</title>
	<script>

	/* ### 1. 글로벌변수와 지역변수  */
/* 	var scope = '글로벌변수';

	function getValue(){
		var scope='지역변수';
		return scope;
	}
	document.write('1>' +getValue()); // 지역 변수(함수 안에 선언)
	document.write('2>'+scope); // 글로벌 변수  */

	/* ### 2. var 생략 가능 : 지역변수가 글로벌 변수가 된다 '지역변수 '출력 */
/* 	 scope = '글로벌변수';

	function getValue(){
		document.write('0>'+scope+'<br/>');//
		var scope='지역변수';
		return scope;
	}
	document.write('1>' +getValue()); // 지역 변수(함수 안에 선언)
	document.write('2>'+scope); // 지역 변수
*/
	/* ### 3. 지역변수 범위  */
	if(true){
		var i = 100;
	}

	document.write('i='+ i+ '<br/>');

	function test(){
		var j = 1000;
	}
	test();
// 	document.write('j='+ j+ '<br/>'); // ?

	for(var k=0; k<3; k++){}
	for(var k=0; k<3; k++){}

	var k=10;
	var k=100;
	document.write('k=' + k);

	/* 호이스팅(hoisting) */
		// 변수가 자신이 속한 블록 안에 있지 않고 밖으로 끌어올려지는 현상
	function doA(num){
		document.write('before'+value+'<br/>');

		if(num%10 === 0){
			var value = true;
		}
		document.write('after:'+value+'<br/>');
	}
	doA(10);
	</script>

	<!-- ECMA Script 6 (ES6)
		 var 사용 자제 -> let 사용 권장
	 -->
</head>

<body>


 </body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### parameter

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title> 파라메터 인자</title>
	<script>
	// 1. 기본형 인자 (call by value)

	var pri = 10;
	function preParam(pri){ // 인자로 받기 때문에 함수 안에서만 사용 ,반환
		pri--;
		return pri;
	}
	document.write('1>' + preParam(pri) +'<br/>');
	document.write('2>' + pri+'<br/>');

	// 2. 참조형 인자 (call by reference)
	var ref = [1,2,3,4,5];
	function refParam( ref){
		ref.pop(); // 스택 pop, push 는 원본 값을 건드리므로 1,2,3,4 출력
		return ref;
	}
	document.write('1>' + refParam(ref) +'<br/>');
	document.write('2>' + ref+'<br/>');



	</script>
</head>

<body>


 </body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### function_arg

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title>고급 함수 </title>
	<script type="text/javascript" src="js/arg_func.js"></script> <!-- <script/>은 버그인가 -->
	<script type="text/javascript">

	/* 자바스크립트는 함수이름도 인자가 될 수 있다. sum,square 라는 함수 이름 !  */

	function testFunc(arg){
		var data = document.frm.num;
		if(arg=='sum'){
			arrayProcess(data,sum);
			alert('합계:' + sumResult);
		}else if(arg=='square'){
			arrayProcess(data,square);
			alert('제곱:'+ squareResult);
		}
	}

	</script>
</head>
<body>

	<!-- 2 -->
	<form name="frm">
		<label> 숫자를 입력하세요
		<input type="text" name="num" size="3" value="1"/>
		<input type="text" name="num" size="3" value="2"/>
		<input type="text" name="num" size="3" value="3"/>
		<input type="text" name="num" size="3" value="4"/>
		<input type="text" name="num" size="3" value="5"/>
		</label>

		<input type="button" value="총합" onclick="javascript:testFunc('sum')"/>
		<input type="button" value="제곱" onclick="javascript:testFunc('square')"/>
	</form>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### function_arg2

~~~

<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title>06_function_arg2.html </title>
	<script type="text/javascript">

	/* ## 1. 함수이름이 다른 함수의 인자가 될 수 있다.  */
	/* ## 2. 함수가 다른 함수의 인자 될 수 있다.  */
	function prt(key,value){
		document.write(key+':'+value+'<br/>');
	}
	function arrayWalk(data, f){
		for (var key in data){
			f(key, data[key]);
		}
	}
	var ary =  ['ㅁ','ㄴ','ㅇ','ㄹ','ㅎ'];
	//arrayWalk(ary,prt);
	arrayWalk(ary,function(key,value){
		document.write(key+':'+value+'<br/>');
	});
	</script>


</head>
<body>



</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### progress

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>progress</title>
<style>
</style>
</head>
<body>
	<p>다운로드 중</p>
	<progress max="100" id="progress"></progress>
</body>
<script>
	var progress = document.getElementById("progress");
	var current = 0;


	/*
	- setTimeout(func,time): time 지난 후에 한 번 func 함수 실행
	- setInterval(func,time): 매 time 마다 func 함수 실행
	*/

	var intervalId = setInterval(function updateProgress(){
		progress.value = current++;		
		if(current==100){
			clearInterval(intervalId);
		}, 100);
	// 함수 안에 함수 들어가진다! 잘 익혀두기


	/* function updateProgress(){
		progress.value = current++;		
		if(current==100){
			clearInterval(intervalId);
		} */
	}


</script>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

## js/ arg_func.js

~~~

// 함수의 인자로 들어오는 함수처리
function arrayProcess( data, f ) {
	for( key=0; key < data.length; key++ ){
	//for(var key in data ){
		f( key, data[key].value );
	}
}

// 함수명 도 함수의 인자로 들어와서  불려질수 있다.

// 각각의 데이터를 더하는 함수
var sumResult = 0;
function sum( key, data ){
	sumResult += parseInt(data);
}

// 각각의 데이터의 곱을 구하는 함수
var squareResult = new Array();
function square( key, data ){			
	squareResult.push( data * data );
}



~~~

<hr style="height: 1px; background: skyblue"/>
