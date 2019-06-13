---
layout: post
title:  "06-10-[javascript]-7.dom"
subtitle:   "0610-js-dom"
categories: devlog
tags: javascript

---

## dom

<hr style="height: 1px; background: skyblue; "/>

#### sample

~~~

<!DOCTYPE HTML>
<html>
<head>
<meta charset="UTF-8">
<title> DOM 기초 </title>
<script type="text/javascript">


</script>

</head>
<body>
	<p>DOM으로 특정 <strong>노드</strong> 얻어와서 처리한다 </p>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>

#### debug

~~~

<!-- 크롬에서 F12 > 개발자 모드

개발자 모드 오른쪽 상단 > 점세개 모양 > Dock slide
		각자의 취향대로 개발자 모드를 위치 설정

F9 :  next step
F10 : step over (함수를 호출하면 결과만 받고 현재 위치에서 다음 라인 실행 )
F11 : step into (함수 안에 들어가기 )

for문을 선택하여 breakpont 설정
for문 안에 선택하면 for문의 조건문과 증가치를 모두 매번 단계로 확인한다

watch 탭에서 +를 누르고 result 변수를 지정하면 매단계 result 변수를 볼 수 있다.

 			   # DOM Breakpoints  #
			 	- 엘리먼트의 속성이 변경되는 것을 감시하시 위해
				- 소스 탭에서는 DOM 브렉포인트를 잡을 수 없고 엘리먼트 탭에서 잡아줘야 한다.
				- 엘리먼트 탭에서 요소를 선택 > 오른마우스 > Break On > Attributes Modificattion > DOM Breakpoints에 추가됨
						Subtree Modifications: 해당 노드의 자식노드의 변화, 예를들면 자식노드의 추가나 삭제를 하는 자바스크립트 코드에 브렉포인트를 잡아준다.
						Attributes Modificattion: 해당 노드의 어트리뷰트를 변경하는 자바스크립트 코드에 브렉포인트를 잡아준다.
						Node Removal: 해당노드를 삭제하는 자바스크립트 코드에 브렉포인트를 잡아준다.


  				 # XHR/fetch breakpoints
  				 - ajax 통신시 url을 설정하면
  				 - any XHR이라고 추가하면 모든 ajax통신에 대해 설정
   -->

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> 크롬 디버그</title>
<script>

	var result = 0;
	// 디버깅 모드에서 Scope > Global에서는 result 변수 외에 많은 기존 변수가 다 나온다
	// watch 탭에서 +를 누르고 result 변수를 지정하면 매단계 result 변수를 볼 수 있다

	window.onload = function(){
		var btn = document.getElementById('btn');
		btn.onclick = function(){
			for( var i = 10; i >=0 ; i-=2){
				result += i;
			}

			result += func1();			//re.innerHTML = result  ;
			result += func2();		//re.innerHTML = result  ;
			alert('결과:' + result );
			// alert()이 나중에 있어도 먼저 실행하고 나서 화면 결과에 출력된다???
			// 각 줄에 alert()를 여러개 지정해도 alert()만 먼저 다 실행된다.

			//-----------------------------------  2 DOM Breakpoints
			var re = document.getElementById('re');
			re.value = result  ;

		}
	}

	function func1(){
		var temp1 = 100;
		return temp1;
	}

	function func2(){
		var temp1 = 1000;
		return temp1;
	}
</script>
</head>
<body>

<input type='button' value='시작' id='btn'>
<input type='text' id='re'>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### sample_1

~~~

<!DOCTYPE HTML>
<html>
<head>
<meta charset="UTF-8">
<title>DOM에서 노드 검색 방법</title>
<script type="text/javascript">

	window.onload = function(){

		document.getElementById('btn').onclick = function(){
			//alert('버튼!');

			var result = document.getElementById('result');

			// 1. id 로 얻어오기
			//var name = document.querySelector('#name');
			//result.innerHTML = name.value + "님 반갑습니다.2";


			//var name = document.getElementById('name');
			// id 가 name 인 이름의 값을 name에 넣기

			//result.innerHTML = name.value + "님 반갑습니다.";
			// innerHTML

		//2. Class 로 얻어오기

			var name = document.querySelectorAll('.cname');
			result.innerHTML = name[0].value + "님 반갑습니다.2";

			//var name = document.getElementsByClassName('cname');
			//result.innerHTML = name[0].value + "님 반갑습니다.";

		//3. tagName 으로 얻어오기

			//var name = document.getElementsByTagName('input');
			//result.innerHTML = name[0].value + "님 반갑습니다.";

		//4. 폼으로 얻어오기
			//var name = document.fm.name;
			//result.innerHTML = name.value+ " 님 즐거운 주말";


		}
	}

  </script>
</head>

<body>
	<!-- 1 -->
	<form name="fm">
		<label id="label">
		이름 : <input type="text" id="name"	class="cname" name="name" size="15" />

		<!-- 2 -->
		학과 : <input	type="text" id="dept" name="dept" size="15" />
		학교 : <input	type="text" id="univ" name="univ" size="15" />
		</label>

		 <input id="btn" type="button" value="버튼" />
		<div id="result"></div>
	</form>
</body>
</html>


~~~

<hr style="height: 1px; background: skyblue"/>


#### sample_2

~~~

<!DOCTYPE HTML>
<html>
 <head>
<meta charset="UTF-8">
  <title> DOM에서 노트 추가  </title>
  <script type="text/javascript">
  window.onload = function(){

	  var bInsert = document.getElementById('bInsert');
	  bInsert.onclick = insertCustomer;

  }  

	function insertCustomer(){

		// 1. 입력한 값들을 얻어온다.

		var name = document.getElementById('name').value;
			// var name = document.inForm.name.value;
			// var name = document.querySelector('#name').value;
		var age = document.getElementById('age').value;
		var tel = document.getElementById('tel').value;
		var addr = document.getElementById('addr').value;
		// 2. 테이블요소 얻어온다.

		var tbl = document.getElementById('listTable');

		// 3. tr 요소와 td 요소를 생성한다.
		var tr = document.createElement('tr'); // 반드시 변수로 가지고있어야 제어 하기 좋음
		var tdName = document.createElement('td');
		var tdAge = document.createElement('td');
		var tdTel = document.createElement('td');
		var tdAddr = document.createElement('td');
		// 4. 텍스트노드(1번의 입력값)로 생성한다.

		var txt1 = document.createTextNode(name);
		var txt2 = document.createTextNode(age);
		var txt3 = document.createTextNode(tel);
		var txt4 = document.createTextNode(addr);

		// 5. td 요소에 텍스트노드를 붙인다.

		tdName.appendChild(txt1);
		tdAge.appendChild(txt2);
		tdTel.appendChild(txt3);
		tdAddr.appendChild(txt4);

		// 6. tr 요소에 생성한 td 요소를 붙인다.

		tr.appendChild(tdName);
		tr.appendChild(tdAge);
		tr.appendChild(tdTel);
		tr.appendChild(tdAddr);


		// 7. 테이블요소에 tr요소를 붙인다.
		tbl.appendChild(tr);



	}
</script>
 </head>
<body>

<h2> 고객정보 입력 </h2>

<form name="inForm" method="post">
<table border = 1>
	<tr>
		<td width="80" align="center">Name</td>
		<td width="50" align="center">Age</td>
		<td width="100" align="center">Tel</td>
		<td width="250" align="center">Addr</td>
	</tr>
	<tr>
		<td align="center"><input type="text" size="8" name="name" id="name"></td>
		<td align="center"><input type="text" size="4" name="age" id="age"></td>
		<td align="center"><input type="text" size="12" name="tel" id="tel"></td>
		<td align="center"><input type="text" size="30" name="addr" id="addr"></td>
	</tr>
	<tr>
		<td colspan="4" align="center">
			<input type="button" value="입력" id='bInsert' >
		</td>
	</tr>
</table>

<br>
<hr>

<h2> 고객정보 목록보기  </h2>
<table border = 1 id="listTable">
	<tr>
		<td width="80" align="center">Name</td>
		<td width="50" align="center">Age</td>
		<td width="100" align="center">Tel</td>
		<td width="250" align="center">Addr</td>
	</tr>
</table>

</form>
</body>
</html>



~~~

<hr style="height: 1px; background: skyblue"/>
