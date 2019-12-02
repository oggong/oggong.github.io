---
layout: post
title:  "06-03-[javascript]-2.eventHandler"
subtitle:   "0603-js-eventHandler"
categories: devlog
tags: javascript

---

## eventHandler

<hr style="height: 1px; background: skyblue; "/>

#### event_called

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> 이벤트 핸들러 연결 </title>

	<script type="text/javascript">
	//function btn_click(){
	//	alert('이벤트 발생');
	//}

	//자바 스크립트는  함수도 자료형이다.
	// 변수 선언 가능


	var btn_click = function(){alert('이벤트확인');}
	</script>

</head>

<body>
	<input type='button' value='눌려' onclick='btn_click()' />
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### evnet_handler

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>이벤트 핸들러 연결</title>
<script type="text/javascript">
	window.onload = init;
	function init() {
		var btn = document.getElementById('btn');
		btn.onclick = btn_click;

		function btn_click(e) {
			alert('이벤트방식2 : ' + e);
		}
	}

	/* 	window.onload = function() {
	 var btn = document.getElementById('btn');
	 btn.onclick = function() {
	 alert('이벤트방식2');

	 }
	 } */

	/* 	window.onload = function() {
	 document.getElementById('btn').onclick = function() {
	 alert('이벤트방식2-z');
	 }
	 } */
</script>

</head>
<body>
	<input type='button' value='눌러' id='btn' />
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### event_listner

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>이벤트 리스너 연결</title>

<script type="text/javascript">
	/* window.onload = function(){

		var btn = document.getElementById('btn');
		btn.addEventListener('click', btn_click);

		function btn_click(){
			alert('이벤트방식-3');
		}
	} */

	window.onload = function() {
		document.getElementById('btn').addEventListener('click', function() {
			alert('이벤트 방식-3');
		});
	}
</script>
</head>
<body>
	<input type='button' value='눌러' id='btn' />
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### eventTest

~~~

<!--
	1. 페이지 이벤트
		onload 		: 페이지를 불러오기 할 때
		onunload 	: 다른 페이지로 이동할 때 ( 브라우저를 끝때가 아님 )

	2. 마우스 이벤트
		onmouseover	: 마우스 커서를 대면
		onmouseout	: 마우스 커서가 떠나면
		onclick		: 마우스 클릭시
		onmousedown	: 마우스 버튼을 눌였을 때
		onmouseup	: 마우스 버튼을 떼었을 때
 -->

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title> 이벤트 </title>
</head>
<body onload="alert('무척이나 반갑습니다')" onunload="alert('가긴어딜가..가지맛!! 돌아와줘!')">

	<input type="button" value="눌려~~~~" onclick="alert('누르라고 누르긴')"><br><br><br>
	<b onmouseover="alert('마우스 치워랏')">이 글씨에 마우스를 대면.....</b><br><br><br><br><br>
	<b onmouseover="this.style.background='red'" onmouseout="this.style.background='white'">
	다시 한번만 더 마우스를 대주세요
	</b><br>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
