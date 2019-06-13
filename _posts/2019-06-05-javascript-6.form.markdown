---
layout: post
title:  "06-05-[javascript]-6.form"
subtitle:   "0605-js-form"
categories: devlog
tags: javascript

---

## form

<hr style="height: 1px; background: skyblue; "/>

#### form_check

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title> 폼 예제 1 </title>
<script type="text/javascript" src = './js/formCheck.js'></script>

</head>
<body>
아래의 폼을 완성하시렵니까<br><br>
<form name="frm" id='frm' method="get" action="something.jsp">


	<!-- 이름 입력 텍스트필드 추가(한글만 가능 2~5 사이) -->
	<label for="name">이름</label>
		<input id="name" name = 'name'pattern="[ㄱ-힣]{2,5}" placeholder='한글 2-5자 입력 하세요'maxlength="5" required	><br>
	<label for="nickname">별명</label>
		<input id="nickname" name = 'nickname' pattern="[A-Za-z]{3,}" maxlength="10" value="">
		<br>
		<label for="myemail">이메일</label>
		<input type="email" id="myemail" required>
		<br>
		<label for="myage">나이</label>
		<input type="number" id="myage" min="0" max="100" step="20" value="23">
		<br>
		<label for="agree">약관</label>
		<input type="checkbox" id="agree" value=''/>네 확인하였습니다.
		<br>
	<input type="button" value="눌려봐">
</form>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### form_var

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title></title>
<script type="text/javascript">

	window.onload = function(){

		// 첫번째 방식
		document.myForm.txt0.value = '하하';
		// 두번째 방식
		document.myForm['txt1'].value = '호호';


		document.getElementById('btn').onclick = function(){
			// 네 곳의 input 태그에 '데이타' 글씨를 지정

			for(var i = 0; i < 4; i++){
				document.myForm['txt'+i].value ='데이타';				
			}
		}
	}

</script>
</head>
<body>
	<form name='myForm'>
		첫번째 :  <input type='text' name='txt0'><br/>
		두번째 :  <input type='text' name='txt1'><br/>
		세번째 :  <input type='text' name='txt2'><br/>
		네번째 :  <input type='text' name='txt3'><br/>
		<input type='button' value='값지정'  id='btn'>
	</form>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### select_1

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>이벤트 예제 2</title>
<script type="text/javascript">
	window.onload = function() {

		//
		var mango = document.frm.mango; // id로 있으면 getElementById ,
		//name 이면 form 태그 안에 있는지 확인 후 document 로 찾기
		// value를 써주면 태그 사이 값을 value 로 가져옴
		var avocado = document.frm.avocado;

		mango.onchange = cal;
		avocado.onchange = cal;

		function cal() {
			document.frm.total.value = mango.value * 4000
			+ avocado.value* 5000; // 화면에 뜨자마자 total 값에 넣어줌
		}

	//	mango.onchange = function(){
		//	document.frm.total.value = mango.value * 4000
		//	+ avocado.value* 5000; // 화면에 뜨자마자 total 값에 넣어줌
		//} ---------------------------------------------------------> 한번 쓸때 축약 사용 가능!

	}
</script>

</head>
<body>
	주문서
	<hr>

	<form name="frm">
		<table border='1'>
			<tr>
				<th>상품</th>
				<th>단가</th>
				<th>주문수량</th>
			</tr>
			<tr>
				<td>망고</td>
				<td>4000원</td>
				<td><select name="mango">
						<option>0</option>
						<option>1</option>
						<option>2</option>
						<option>3</option>
				</select> 뭉치</td>
			</tr>
			<tr>
				<td>아보카도</td>
				<td>5000원</td>
				<td><select name="avocado">
						<option>0</option>
						<option>1</option>
						<option>2</option>
						<option>3</option>
				</select> 봉다리</td>
			</tr>
			<tr>
				<td colspan=2>함계</td>
				<td><input type="text" name="total" size=6>원</td>
			</tr>
			<tr>

			</tr>
		</table>
	</form>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>


#### select_2

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title> 폼 예제 2</title>
</head>
<script type="text/javascript">

		window.onload = function(){

			var upBtn = document.getElementById('up');
			upBtn.onclick = function(){
				//alert('up');
				var idx = document.frm.play.selectedIndex; // 선택한 인덱스를 얻어오기
				var optSel = document.frm.play.options; // options 는 배열로 넘어간다. -s-
				var str = optSel[idx].text; //text 인지 value 인지 잘 확인

				if(idx>0){

				optSel[idx].text = optSel[idx-1].text;
				optSel[idx-1].text =str;
				optSel[idx-1].selected = true;

				//alert(str);
				}
			}

			var downBtn = document.getElementById('down');
			downBtn.onclick = function(){
				//alert('down');
				var idx = document.frm.play.selectedIndex;
				var optSel = document.frm.play.options;
				var str = optSel[idx].text;

				if(idx< optSel.length -1){
					optSel[idx].text =optSel[idx+1].text;
					optSel[idx+1].text =str;
					optSel[idx+1].selected = true;
				}
			}

			//document.getElementById('down').onclick = function(){
			// alert('down');
			//}
		}


</script>
<body>

내가 제일 좋아하는 놀이 순서대로 한다면 <br>

<form name="frm">
<select name="play" size="8"> <!-- 사이즈 지정 -->
	<option selected> 숨쉬기 </option>
	<option> 밥먹기 </option>
	<option> 그냥있기 </option>
	<option> 잠자기 </option>
	<option> 술먹기 </option>
	<option> 멍때리기 </option>
</select> <br>

<input type="button" id='up'	value="▲"><br><br>
<input type="button" id='down'	value="▼"><br><br>
</form>

</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>


#### cal_select

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>날짜 선택</title>

<!--  1. 자바스크립트에서 select 태그에 option 값들을 추가하고 오늘 날짜로 지정한다.
			1) 년도는 올해년도를 기준으로 -5 ~ +5 으로 option 값을 지정한다.
			2) 월은 1~12월 지정한다.
			3) 일을 해당 달에 맞는 1일부터 마지막날까지 지정한다.
				[hint] Option 클래스 이용

		2. 년과 월을 변경할 때마다 해당되는 일이 마지막날이 변경되어야 한다.

		3. 오늘 날짜로 선택되어 있어야 한다.
-->



<script type="text/javascript">
//오늘 날짜 구하기
var today = new Date();
var year = today.getFullYear();
var month = today.getMonth();
var date = today.getDate();

var lastDays = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
var weeks = ['일','월','화','수','목','금','토'];


window.onload = function(){

	var frm = document.frm;

	// 년 구하기
	for( var j=year-5;  j<= year+5; j++){
		frm.y.add( new Option(j, j));				
	// 만들고 브라우저 F12에서 Elements로 확인 : Option(j)와 Option(j,j) 차이
	}

	// 월 구하기
	for(var j=1; j<=12; j++){
		frm.m.add(new Option(j,j));
	}

	// 일 구하기
	for(var j =1; j<=lastDays[month]; j++){
		frm.d.add(new Option(j,j));
	}
	// 오늘을 날짜로 화면을 지정
	frm.y.value = year;
	frm.m.value = month+1;
	frm.d.value = date;

	frm.w.value = weeks[today.getDay()];


	frm.m.onchange = function() {

		frm.d.value.empty;

		for(var j =1; j<=lastDays[frm.m.selectedIndex]; j++){
			frm.d.add(new Option(j,j));
		}
	}

	frm.d.onchange = function() {

	//지정 날자로 화면을 지정

	today.setYear(frm.y.value);
	today.setMonth(frm.m.value-1);
	today.setDate(frm.d.value);

	//alert(today);


	frm.w.value = weeks[today.getDay()];
	}

}
</script>

</head>
<body>
<form name='frm'>
	<select name='y'></select> 년
	<select name='m'></select>월
	<select name='d'></select>일
	<input type='text' name='w' size='4'>요일
</form>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>


#### day

~~~

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title> 폼 예제 3 </title>
<script type="text/javascript">

	window.onload =  function(){




		document.getElementById('btn').onclick = function(){

			var myDate = new Date();

			//사용자 입력 값으로 년,월,일 을 지정(변경)
		/* 	myDate.setFullYear(document.frm1.y.value);
			myDate.setMonth(document.frm1.m.value -1);
			// 0 부터 시작하므로 -1 해줘야 알맞은 값이 나옴
			myDate.setDate(document.frm1.d.value);

			alert(myDate); */

			var y = frm1.y.value;

			var m = frm1.m.value;

			var d = frm1.d.value;

			var myDate = new Date(y+'/'+m+'/'+d);


			//var weeks = [];   
			var weeks = new Array('일','월','화','수','목','금','토');

			document.frm1.w.value = weeks[myDate.getDay()];


		}

	}


</script>
</head>
<body>

<hr><hr>

요일을 알아봅시다. <br>

<form name="frm1">
	<input type="text" name="y" size=4>년
	<input type="text" name="m" size=2>월
	<input type="text" name="d" size=2>일
	<input type="button" id='btn' value="☞" >
	<input type="text" name="w" size=4>요일입니다.
</form>

<hr><hr>


</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
