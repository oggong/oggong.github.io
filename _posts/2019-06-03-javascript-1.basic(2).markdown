---
layout: post
title:  "06-03-[javascript]-1.basic(2)"
subtitle:   "0603-js-basic(2)"
categories: devlog
tags: javascript

---

## basic(2)

<hr style="height: 1px; background: skyblue; "/>

#### string

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>4_string.html</title>
<script type="text/javascript">
	var str = '너의 삶 속에 나의 삶을 넣어 삶을 영위하자';
	document.write(str.indexOf('삶') + "<br/>"); //3
	document.write(str.lastIndexOf('삶') + "<br/>"); // 17
	document.write(str.indexOf('삶을') + "<br/>"); // 11
	document.write(str.length + "<br/>"); // 24

	var msg = '자바에서 웹프로젝트까지 열심히 합시다 짝꿍!';
	document.write(msg.charAt(3) + "<br/>"); // 서
	document.write(msg.slice(5, 12) + "<br/>"); // 웹프로젝트까지
	document.write(msg.substring(5, 12) + "<br/>"); // 웹프로젝트까지 5부터 12까지
	document.write(msg.substr(5, 7) + "<br/>");// 웹프로젝트까지 5부터 시작해서 7개
	document.write(msg.split(' ') + "<br/>"); // 자바에서,웹프로젝트까지,열심히,합시다,짝꿍!
	document.write(msg.concat('화이팅') + "<br/>"); // msg+'화이팅'
	document.write(msg + "<br/>"); //자바에서 웹프로젝트까지 열심히 합시다 짝꿍!
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

#### array

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>5_array.html</title>

<script type="text/javascript">
	var arr = ['지민','뷔','정국','랩몬','제이홉'];
	/* document.write(arr +"</br>"); // 지민 뷔 정국 랩몬 제이홉
	document.write(arr.join('/')+"</br>"); // 지민/뷔/정국/랩몬/제이홉
	document.write(arr.slice(3)+"</br>");// 랩몬 , 제이홉
	document.write(arr.slice(1,3)+"</br>"); // 뷔 , 정국

	document.write(arr.pop()+"</br>"); // 제이홉
	document.write(arr +"</br>"); // 지민,뷔,제이홉,랩몬
	document.write(arr.push('방탄')+"</br>"); //5
	document.write(arr +"</br>"); // 지민,뷔,정국,랩몬,방탄
	document.write(arr.shift() +"</br>"); //지민
	document.write(arr +"</br>"); //뷔,정국,랩몬,방탄
	document.write(arr.length +"</br>"); //4 */

	document.write(arr.reverse()+"</br>" );
	document.write(arr.sort() +"</br>");
	document.write(arr+"</br>");


	var temp = ['슈가','아무개'];
	document.write(arr.concat(temp) +"</br>");
	// 추가되서 나오긴 하지만 원본에 붙어서 나오지 않음
	document.write(arr+"</br>");


</script>

</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### date

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>6_date.html</title>

<script type="text/javascript">
	//var d = new Date("2019/06/02");
	var d = new Date();
	d.setFullYear(2019);
	d.setMonth(5); // 달은 0부터 시작 6월이면 5를 넣어주어야한다.
	d.setDate(3);

	document.write(d + '<br/>'); //Mon Jun 03 2019 12:50:32 GMT+0900 (한국 표준시)
	document.write(d.toLocaleString() + '<br/>'); // 2019. 6. 3. 오후 12:50:32
	document.write(d.toString() + '<br/>'); //	Mon Jun 03 2019 12:50:32 GMT+0900 (한국 표준시)
	document.write(d.toDateString() + '<br/>'); // Mon Jun 03 2019
	document.write(typeof (d) + '<br/>');
	document.write(d.getFullYear() + '<br/>'); //  2019
	document.write(d.getMonth() + '<br/>'); //5
	document.write(d.getDate() + '<br/>'); // 2
	document.write(d.getDay() + '<br/>'); // 요일 ->1(월), 0(일)

	d.setDate(d.getDate() - 10);
	document.write(d.toDateString() + '<br/>'); // 10일을 뺌

	d.setMonth(d.getMonth() - 10);
	document.write(d.toDateString() + '<br/>'); // 10달을 뺌


	d.setDate(0);
	document.write(d.toDateString() + '<br/>'); // 전 달의 마지막 일

	document.write(d.getHours() +'<br/>');
	document.write(d.getMinutes() +'<br/>');
	document.write(d.getSeconds() + '<br/>');



	</script>

</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### date_practice

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>6_date_연습.html</title>


<script type="text/javascript">
	window.onload = function() { //이벤트 발생 후 확인
		var btn = document.getElementById('btn');
		btn.onclick = function() {
			//	alert('확인');
			//	var s = document.getElementById('startDate').value;
			//	var e = document.getElementById('endDate').value;
			//	alert(s +"~"+ e);

			// 1. 사용자 입력값을 Date 형 만들기
			// 2. 두 Date 차이 (- 연산자 이용)
			// 3. 2번의 차이값을 alert 으로 출력

			var s = document.getElementById('startDate').value;
			var e = document.getElementById('endDate').value;

			var sdate = new Date(s);
			var edate = new Date(e);

			// var diff = edate.getDate() - sdate.getDate();
			// alert(diff);

			var diff = edate.getTime() - sdate.getTime();
			//alert(diff);

			var diffday = Math.ceil(diff/(24*60*60*1000)); // 1 이 나옴 !!
			alert(diffday);



		}
	}
</script>

</head>
<body>

	시작일 :
	<input type='date' id='startDate' /> 종료일 :
	<input type='date' id='endDate' />
	<input type='button' id='btn' value='여행 일정' />

	<!-- <script type="text/javascript">
		var btn = document.getElementById('btn');
		btn.onclick = function() {
			alert('확인');
		}
	</script> -->

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### regexp

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>RegExp 객체</title>
<script type="text/javascript">
	var p = /http(s)?:\/\/([\w-]+\.)+[\w-]+(\/[\w-.\/?%&=]*)?/gi;
	//var p = new RegExp('http(s)?://([\\w-]+\\.)+[\\w-]+(/[\\w-./?%&=]*)?','gi');
	var str = '한 번을 둘러봐야 하는 사이트 http://www.w3schools.com/ 입니다';
	str += ' 또한 집중적으로 봐야하는 사이트 http://jqapi.ru/ 입니다';

	// (1) match() exec 보다 match 메소드 사용 권장

	var result = str.match(p);
	for (var i = 0; i < result.length; i++) {
		document.write(result[i] + "<br/>")
	}

	// (2) exec() - 결과가 이상함
	var result2;
	while ((result2 = p.exec(str)) != null) {
		document.write(result2 + '<br/>');
	}
	// (3) test()
	var one = '한 번을 둘러봐야 하는 사이트 http://www.w3schools.com/ 입니다';
	var two = ' 또한 집중적으로 봐야하는 사이트 http://jqapi.ru/ 입니다';

	document.write(p.test(one) + '<br/>'); // true
	document.write(p.test(two) + '<br/>'); // false
</script>
</head>
<body>

</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### 형변환

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>8_형변환.html</title>

<script type="text/javascript">
	//1. 형변환

	var n = '0770';
	document.write(Number(n) + '<br/>');
	document.write(parseFloat(n) + '<br/>');
	document.write(parseInt(n) + '<br/>');

	var n = '123abc';
	document.write(Number(n) + '<br/>'); // Not a Number
	document.write(parseFloat(n) + '<br/>'); // 123
	document.write(parseInt(n) + '<br/>'); // 123

	//2. 연산 후 형변환
	document.write(123 + "4" + '<br/>'); // 숫자 + 문자열 -> 1234
	document.write(123 - "4" + '<br/>'); // 숫자 - 문자열 -> 119

	document.write(typeof (123 + "4") + '<br/>'); // string
	document.write(typeof (123 - "4") + '<br/>'); // number

	//3. 요긴한 함수 -> 악마함수
	var str = 'alert("안녕하세요")';
	alert(str);
	eval(str);

</script>


</head>
<body>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### homework

~~~

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>99_hw.html</title>
    <!--    달력 만들기-->
    <script type="text/javascript">

        var today = new Date();
        document.write(today + '<br>');
        var year1 = today.getFullYear(); // 2019
        var month1 = today.getMonth() + 1; // 6
        var date1 = today.getDate(); // 3
        var day1 = today.getDay(); // 1 // 오늘의 요일, 월요일
        var startDate = new Date(today.setDate(0)).getDay(); // 5 // 전달의 마지막 요일, 금요일

        document.write(year1, month1, date1, day1 + '<br>');
        document.write(startDate + '<br>');

        var nextMonth = new Date();
        nextMonth.setMonth(month1);
        document.write(nextMonth + '<br>');
        document.write('==============' + '<br>');
        nextMonth.setDate(0);
        document.write(nextMonth.getDate() + '<br>'); // 30, 이번 달의 마지막 요일
        var lastDate = nextMonth.getDate();

        document.write("<table border='3px'>");
        document.write("<tr rowspan='5'>" + month1 + "월 달력</tr>");
        document.write("<tr>");
        document.write("<td>" + "일요일" + "</td>");
        document.write("<td>" + "월요일" + "</td>");
        document.write("<td>" + "화요일" + "</td>");
        document.write("<td>" + "수요일" + "</td>");
        document.write("<td>" + "목요일" + "</td>");
        document.write("<td>" + "금요일" + "</td>");
        document.write("<td>" + "토요일" + "</td>");
        document.write("</tr>");

        var k = 1;
        document.write("<tr>");
        for (var aa = 0; aa < 7; aa++) {
            if (aa > startDate) {
                document.write("<td>" + k + "</td>");
                k = k + 1;
            } else {
                document.write("<td>" + " " + "</td>");
            }
        }
        document.write("<tr>");
        for (var i = 0; i < 5; i++) {
            document.write("<tr>");
            for (var j = 0; j < 7; j++, k++) {
                if (k <= lastDate) {
                document.write("<td>" + k + "</td>");
                }
                else document.write("<td>" + " " + "</td>");
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
