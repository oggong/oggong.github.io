---
layout: post
title:  "06-04-[javascript]-4.dialog"
subtitle:   "0604-js-dialog"
categories: devlog
tags: javascript

---

## dialog

<hr style="height: 1px; background: skyblue; "/>

#### event_called

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>Alert Test</title>
<script type="text/javascript">
	//1. HTML에서 함수 호출 방식

	function show_dialog() {
		alert('확인');
	}
	//2. JS에서 요소 찾아서 이벤트함수 연결

	window.onload = function() {
		//alert -> confirm
		var result = confirm('이 페이지는 http://playdata.io로 이사하였습니다.\n 이동하시겠습니까?');
		//window.location.href = 'http://playdata.io';
		//location.href = 'http://playdata.io';
		//window.location = 'http://playdata.io';
		//location = 'http://playdata.io';
		if (result) {
			location = 'http://playdata.io';
		}
	}
</script>
</head>
<!-- <body onload="show_dialog()"> -->
<body>이 사이트는 조만간 운영하지 않습니다.
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>
