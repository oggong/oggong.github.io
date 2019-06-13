---
layout: post
title:  "06-05-[javascript]-5.window(2)"
subtitle:   "0605-js-window(2)"
categories: devlog
tags: javascript

---

## window (2)

<hr style="height: 1px; background: skyblue; "/>

#### iframe_practice(1)

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>4_iframe_연습.html</title>

<script type="text/javascript">
		function changeSite() {
			var siteCheck = document.frm.site.value;		
			var ifrm = document.getElementById('ifrm');

			switch (siteCheck) {
			case '다음':
				ifrm.src = 'http://www.daum.net';
				break;
			case '다나와':
				ifrm.src = 'http://www.danawa.com';
				break;
			case '네이트':
				ifrm.src = 'http://www.nate.com';
				break;
			}
		}

	//http://postcode.map.daum.net/guide
</script>
</head>
<body>

	<form name="frm">
		<input type="radio" name="site" onclick="changeSite()" value='다음'> 다음
		<input type="radio" name="site" onclick="changeSite()" value='다나와'> 다나와
		<input type="radio"	name="site" onclick="changeSite()" value='네이트'> 네이트 <br /> <br />

	</form>
	<iframe name='ifrm' id='ifrm' width="800" height="800" src = ""> </iframe>

</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### sub

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script type="text/javascript">
	function sel() {
		parent.frm.result.value = document.fm.gender.value;
	}
</script>
<title></title>
</head>
<body>

	<form name='fm'>
		받은 결과 : <input type='text' name='result' size='20' />
		<hr />
		<input type='radio' name='gender' value='남자' onclick='sel()'>남자
		<input type='radio' name='gender' value='여자' onclick='sel()'>여자
	</form>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
