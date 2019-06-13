---
layout: post
title:  "06-03-[javascript]-1.basic(1)"
subtitle:   "0603-js-basic(1)"
categories: devlog
tags: javascript

---

## basic(1)

<hr style="height: 1px; background: skyblue; "/>

#### datatype

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>1_datatype.html</title>

<!-- 주석  -->

<script type="text/javascript">
	//1. 자바 스크립트는 자료형에 관대하다.
	//		변수 선언시 자료형을 기술하지 않는다.

	var byensu = "문자열";
	document.write('변수의값:' + byensu + '<br/>');

	byensu = 1000;
	document.writeln('변수의값:' + byensu + '<br/>');

	// 2. 리터럴 - 자료형(데이타 타입)에 들어가는 값
	var arr = [ '안녕', 'Hello', 'Hola', '곤니치와' ]; // 1차원 배열  
	document.writeln('배열의 요소:' + arr[1] + "<br/>");

	var arr = [ '안녕', [ 'Hello', 'Hola' ], '곤니치와' ]; // 나름 이차원 배열
	document.writeln('배열의 요소:' + arr[1][0] + "<br/>");

	var obj = {
		x : '안녕',
		y : 'Hello',
		z : '곤니치와'
	}; //JSON 구조
	document.writeln('객체의 프로퍼티 :' + obj.x + "<br/>");
	document.writeln('객체의 프로퍼티 :' + obj['x'] + "<br/>");

	var x;
	document.writeln('x=' + x + "<br/>"); 		//error? no
	document.writeln('obj.a =' + obj.a + "<br/>");		//error? no undefined 출력
	// 특수형 -- null 과 undefined


</script>


</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### operator

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>2_operator.html</title>
<script type="text/javascript">
	// 1. == 와 === 차이점

	var num = 10;
	var str = '10';

	if(num == str) alert('같다1'); // 첫번째는 값만 비교 // 자바스크립트의 특성 (자료형을 구분 하지 않는다)
	else alert('다르다1');

	if(num === str) document.write('같다2 <br/>'); // 두번째는 값과 자료형 모두 비교 !!!
	else document.write('다르다2 <br/>');

	if(num !== str) document.write('not 같다  <br/>'); // NOT 연산자
	else document.write('not 다르다  <br/>');


	//2. 실수형 계산시 주의!!!

	document.writeln(0.2*3 == 0.6 +'<br/>'); // true-> false

	document.write(0.2*3); //  0.6000000000000001

	document.write(0.2*10*3 == 0.6*10); // 정수로 만들어 놓고 계산

</script>


</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### for

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>3_for.html</title>
<script type="text/javascript">

	var arr= ['a','b','c'];

	for(var i=0;i<arr.length;i++){
		document.write(arr[i]+"<br/>");
	}// for 문

	for(var i in arr){
		document.write( arr[i] +"<br/>");
	}// 향상된 for문

	var obj = {x:'안녕',y:'hello',z:'Hola'};

	obj.w = '곤니치와';

	for(var i in obj){
		document.write(typeof(i)+":" +obj[i] +"<br/>"); // obj.i 로 하면 undefined 출력
	}

</script>

</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### for_practice

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>3_for연습.html</title>

<script type="text/javascript">
<!-- 5행 5열 테이블을 만드시고 1~ 25 까지 숫자 지정-->
	document.write("<table border='1'>");
	var k = 1;
	for (var i = 0; i < 5; i++) {
		document.write("<tr>");
		for (var j = 0; j < 5; j++, k++) {
			document.write("<td>" + k + "</td>");
		}
		document.write("</tr>");
	}
	document.write("</table>");
</script>

</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
