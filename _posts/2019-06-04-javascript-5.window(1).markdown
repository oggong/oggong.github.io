---
layout: post
title:  "06-04-[javascript]-5.window(1)"
subtitle:   "0604-js-window(1)"
categories: devlog
tags: javascript

---

## window (1)

<hr style="height: 1px; background: skyblue; "/>

#### location_href

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="euc-kr">
<title>window 예제</title>
<script type="text/javascript">
	window.onload = function() {
		//축약
		var sel = document.frm.chooseSite;
		sel.onchange = function() {

			//setTimeout(test, 2000);

			setTimeout(function() {
				//1. 선택한 옵션의 값(url)을 얻어온다.
				var nextPage = sel.value;
				//2. location 객체의 href 프로퍼티에 url을 지정
				//window.location.href = nextPage;

				//loaction 의 replace 이용
				location.replace(nextPage);
				//href와의 차이점은 뒤로가기 버튼이 비활성화 -- 기록에 남기지 않음
			}, 2000); // 축약형
		}

		/* var sel = document.frm.chooseSite;
		sel.onchange = showSite; // 이벤트 연결

		function showSite() {
			alert('이벤트 확인2');
		 */
	}
</script>
</head>
<body>
	<form name="frm">
		<h1>이동하길 원하는 페이지를 선택하세요</h1>
		<!-- <select name="chooseSite" onchange='showSite()'> -->
		<select name="chooseSite">
			<option>골라 골라</option>
			<option value="http://www.daum.net">다음네</option>
			<option value="http://www.naver.com">네이바</option>
			<option value="http://www.nate.com">네이또</option>
		</select>
	</form>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### window_location

~~~

<!--
	1. 새로운 창을 연다
		창변수 = window.open ( "URL", "창이름", "옵션지정" )

			* 옵션
			direction='yes/no'	: 디렉토리바 표시 여부
			location='yes/no'	: 로케이션바 표시 여부
			menubar='yes/no'	: 메뉴바 표시 여부
			scrollbars='yes/no'	: 스크롤바 표시 여부
			status='yes/no'		: 상태바 표시 여부
			toolbar='yes/no'	: 툴바 표시 여부
			resizable='yes/no'	: 창 크기 변경가능 여부
			width=숫자(픽셀단위)	: 창의 폭
			height=숫자(픽셀단위)	: 창의 높이

	2. 창을 닫는다
		창변수.close()

	3. 창이 열려있는지 확인
		창변수.closed()

 -->

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>window 예제</title>
<script type="text/javascript">
	window.onload = function() {

		var sel = document.frm.chooseSite;

		sel.onchange = showSite;

		function showSite() {

			var winObj = window.open('', 'window-name',
					'width=480 ,height = 400');

			var idx = sel.selectedIndex;
			switch(idx)
			{
				case 1:winObj.location.href = 'http://www.daum.net'; break;
				case 2:winObj.location.href = 'http://www.naver.com'; break;
				case 3:winObj.location.href = 'http://www.nate.com'; break;
			}

			/*
			1. 선택한 값의 인덱스를 얻어온다.
			2. 각각의 인덱스에 맞는 새로운 창을 연다
			[예] 인덱스 값이 1이라면 http://www.daum.net으로 창을 연다
			 */

		}

	}
</script>
</head>
<body>
	<form name="frm">
		<h1>이동하길 원하는 페이지를 선택하세요</h1>
		<select name="chooseSite">
			<option>골라 골라</option>
			<option>다음네</option>
			<option>네이바</option>
			<option>네이또</option>
		</select>
	</form>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### window_opener

~~~

<!--
	자기를 열어준 창을 제어할려면? opener
 -->

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>여기가 원래 창</title>
</head>
<body bgcolor="#ddddff">
	원하는 사이트를 선택하여 주시면 넘어갈걸요?

	<script type="text/javascript">
		//3_2_window_opened.html 창을 열기

		//창변수 = window.open ( "URL", "창이름", "옵션지정" )
		var winObj = window.open('3_2_window_opened.html', '',
				'width=400, height=380');
	</script>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### window_opened

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>새로 열려진 창</title>
<script type="text/javascript">
	window.onload = function() {
		var rds = document.frm.site;

		for (var i = 0; i < rds.length; i++) {
			rds[i].onclick = changeSite;
		}
		function changeSite() {

			switch (rds.value) {
			case '0':
				opener.location.href = 'http://www.daum.net';
				break;
			case '1':
				opener.location.href = 'http://www.naver.com';
				break;
			case '2':
				opener.location.href = 'http://www.nate.com';
				break;

			}
			window.close();

		}

	}
</script>
</head>
<body>
	<form name="frm">
		<input type="radio" name="site" value='0'> 다음 <br> <input
			type="radio" name="site" value='1'> 네이버 <br> <input
			type="radio" name="site" value='2'> 네이트 <br>
	</form>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### iframe

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>부분독립페이지</title>
<script type="text/javascript">
	window.onload = function() {
	}
	function changeSite() {
		ifrm.fm.result.value = document.frm.site.value;

	}
</script>
</head>
<body>

	<form name="frm">
		<input type="radio" name="site" onclick="changeSite()" value='다음'>
		다음 <br> <input type="radio" name="site" onclick="changeSite()"
			value='네이버'> 네이버 <br> <input type="radio" name="site"
			onclick="changeSite()" value='네이트'> 네이트 <br> 결과받기 : <input
			type='text' name='result' size='20' /> <br /> <br />
	</form>

	<iframe name='ifrm' width="420" height="315" src="4_sub.html">
	</iframe>

</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>
