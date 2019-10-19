---
layout: post
title:  "06-03-[javascript]-document"
subtitle:   "0603-js-document"
categories: devlog
tags: javascript

---

## document

<hr style="height: 1px; background: skyblue; "/>

#### documentopen

~~~

<!DOCTYPE html>
<html>
<head>
<title>Document 예제</title>
<meta charset="UTF-8">
<style type="text/css">
</style>

<script type="text/Javascript">
	function show_document() {
		//var irum = document.frm.userName.value;

		//var irum = document.forms[0].userName.value;

		var irum = document.getElementById('userName').value;

		//alert(irum);

		var result = document.getElementById('result');
		result.innerHTML = irum + '님 반갑습니다.';
	}
</script>
</head>

<body>
	<form name="frm">
		당신의 이름은? <input type="text" id='userName' name="userName" size="20">
		<input type="button" value="눌려봐" onclick="JavaScript:show_document()">
	</form>
	<div id='result'></div>
</body>
</html>



~~~

<hr style="height: 1px; background: skyblue"/>

#### document_color

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> 화면 색 바꾸기 </title>
</head>
<body>
	<form name="frm">
		<input type="button" value="스타일 A" onclick="JavaScript:changeColor('A')">
		<input type="button" value="스타일 B" onclick="JavaScript:changeColor('B')">
		<input type="button" value="스타일 C" onclick="JavaScript:changeColor('C')">
	</form>
	여기는 한국입니다.
	<ul>
		<li><a href="http://www.cnn.com"> 여기는 미쿡 </a></li>
		<li><a href="http://news.bbc.co.uk"> 여기는 영쿡 </a></li>
	</ul>

	<!--
			일반적으로 JavaScript는 < head > 안에 기술하는  방법을 많이 씁니다.
			그러나 필요에 따라 < body > 태그 안에 사용도 합니다.
			물론, 지금은 그럴 필요가 없지만 < body > 태그 안에 넣어봤음.

			인자있는 자바스크립스 함수 호출
	 -->
	<script type="text/javascript">

	</script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
