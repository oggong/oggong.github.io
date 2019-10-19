---
layout: post
title:  "0531-[Web]-bootstrap(2)"
subtitle:   "0531-bootstrap(2)"
categories: devlog
tags: web

---

## bootstrap (2)

<hr style="height: 1px; background: skyblue; "/>

#### grid(1)

~~~

<!-- (3) 화면을 작게 하여 반응형을 웹을 확인  -->

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title> 기본 샘플 확인 </title>

    <!-- 부트스트랩 -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    	<!-- (2) 선을 그려 확인  -->
        <style>
				.col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6,
				.col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11,  .col-md-12 {
				  border: 1px solid red;
				  padding: 10px;
				}
				.row{
				  margin-bottom: 4px;
				  margin-top: 4px;

				  }
		</style>
</head>
<body>
	<!--  ............................................................................  -->   

  <div class="container">
    <div class="row">
      <!--  (1) 8칸 을 가정하고  -->
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
      <div class="col-md-1"> 1칸 </div>
    </div>

	<div class='row'>
		<div class='col-md-4'>4칸</div>
		<div class='col-md-4'>4칸</div>
	</div>

	<div class='row'>
		<div class='col-md-2'>2칸</div>
		<div class='col-md-2'>2칸</div>
		<div class='col-md-2'>2칸</div>
		<div class='col-md-2'>2칸</div>
		<div class='col-md-2'>2칸</div>

	</div>

  </div>

	<!--  ............................................................................  -->

    <!-- jQuery (부트스트랩의 자바스크립트 플러그인을 위해 필요합니다) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
    <!-- 모든 컴파일된 플러그인을 포함합니다 (아래), 원하지 않는다면 필요한 각각의 파일을 포함하세요 -->
    <script src="js/bootstrap.min.js"></script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### grid(2)

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>기본 샘플 확인</title>

<!-- 부트스트랩 -->
<link href="css/bootstrap.min.css" rel="stylesheet">

<style>
/* 나늠고딕체 가져오기 항상 저작권 조심!!!  */
@import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);

header {
	height: 100px;
	background-color: rgba(125, 211, 242, 0.5);
	border-radius: 15px;
	padding: 10px;
	margin: 10px;
	font-family: 'Nanum Gothic', sans-serif;
	text-align: center;
}

footer {
	text-align: center;
}

ul.nav {
	background-color: rgba(201, 201, 201, .5);
	padding: 10px;
	border-radius: 10px;
}
</style>
</head>
<body>
	<!--  ............................................................................  -->

	<div class="container">
		<header>
			<h2>우리들의 사이트</h2>
		</header>

		<div class="row">
			<div class='col-md-2 col-md-push-10'>
				<ul class="nav">
					<li>주제 1</li>
					<li>주제 2</li>
					<li>주제 3</li>
					<li>주제 4</li>
				</ul>
			</div>

			<div class='col-md-10 col-md-pull-2'>
				<h3>1696년의 죽도(울릉도／다케시마) 도해금지령</h3>
				<p>1696년에 일본 막부는 어민들에게 울릉도에 건너가지 못하도록 명을 내렸습니다. 이를 죽도(울릉도／다케시마)
					도해금지령이라고 하는데, 여기에는 독도도 포함됩니다. 안용복이 1693년 일본에 끌려가 울릉도와 독도를 우리나라 땅이라고
					주장하고부터 일본은 울릉도를 빼앗아 가기 위해 여러 가지 방법을 썼습니다. 당시 막부는 최종 결정을 내리기에 앞서
					돗토리번의 영주에게 두 섬이 어느 나라에 속하는지를 물었습니다(1695년 12월). 돗토리번의 영주는 조사해 본 결과,
					조선에서 마쓰시마(독도)까지는 80~90해리, 마쓰시마(독도)에서 죽도(울릉도／다케시마)까지는 40해리, 그리고 일본
					오키섬에서 마쓰시마(독도)까지는 80해리라는 사실을 알아냈습니다. 그래서 돗토리번 영주는 울릉도와 독도, 두 섬이 일본에
					속한 섬이 아니라고 막부에 보고하였는데, 이러한 사실이 일본의 여러 기록에 남아 있습니다.</p>

				<h3>1870년 일본 외무성의 보고서「조선국 교제시말 내탐서」</h3>
				<p>1869년 12월 일본은 외무성 관리 3인을 조선에 보냈습니다. 이는 새로 들어선 일본 메이지 정부가 조선과
					새로운 관계를 맺기 위해 조선에 관한 조사를 새로 할 필요를 느꼈기 때문입니다. 이때 관리들은 보고서에서
					‘죽도(울릉도／다케시마)와 마쓰시마(독도)가 조선 부속이 된 경위’를 적었습니다. 이 보고서로도 일본이 두 섬을 조선
					영토로 인정하고 있었다는 것이 드러납니다.</p>
			</div>

		</div>
		<hr>
		<footer> 여기는 우리 사이트 기본 정보 </footer>
	</div>
	<!--  ............................................................................  -->

	<!-- jQuery (부트스트랩의 자바스크립트 플러그인을 위해 필요합니다) -->
	<script
		src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
	<!-- 모든 컴파일된 플러그인을 포함합니다 (아래), 원하지 않는다면 필요한 각각의 파일을 포함하세요 -->
	<script src="js/bootstrap.min.js"></script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### form

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>기본 샘플 확인</title>

<!-- 부트스트랩 -->
<link href="css/bootstrap.min.css" rel="stylesheet">

</head>
<body>
	<!--  ............................................................................  -->

	<div class="container">

		<h4 class="text-primary">기본적인 HTML5의 폼</h4>
		<form>
			<label for="name">이름</label> <input type="text" id='name'
				placeholder="이름"> <label for="email">이메일</label> <input
				type="email" id='email' placeholder="이메일">
			<button type="submit">확인</button>
		</form>
		<hr>
		<h4 class="text-primary">부트스트랩의 폼</h4>
		<form role='form' class='form-inline'>
			<div class='form-group'>
				<label for="name">이름</label>
				<input class='form-control' type="text" id='name' placeholder="이름">
			</div>
			<div class='form-group'>
				<label for="email">이메일</label>
				<input class='form-control' type="email" id='email'	placeholder="이메일">
			</div>
			<div class='form-group'>
			<button type="submit">확인</button>
			</div>
		</form>



	</div>

	<!--  ............................................................................  -->

	<!-- jQuery (부트스트랩의 자바스크립트 플러그인을 위해 필요합니다) -->
	<script
		src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
	<!-- 모든 컴파일된 플러그인을 포함합니다 (아래), 원하지 않는다면 필요한 각각의 파일을 포함하세요 -->
	<script src="js/bootstrap.min.js"></script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### formSample

~~~

<!doctype html>
<html lang="ko-kr">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>부트스트랩   </title>

    <!-- Bootstrap -->
    <link href="./css/bootstrap.min.css" rel="stylesheet">

  </head>
<body>
 <div class="container">  

    <h4 class="text-primary"> 기본적인 HTML5의 폼 형식</h4>
        <h5> input type="text"</h5>
            <input type="text" class="form-control">
        <h5> input type="password"</h5>  
            <input type="password" class="form-control">         
        <h5> input type="date" </h5>
            <input type="date" class="form-control">
        <h5>input  type="month"</h5>
            <input type="month" class="form-control">
        <h5> type="week"</h5>
            <input type="week" class="form-control">
        <h5> textarea</h5>     
            <textarea  rows="5" class="form-control"></textarea>

        <h5> input type="checkbox"</h5>         
        <div class="checkbox">
          <label>
            <input type="checkbox" value="">
            여기는 체크박스가 적용되는 곳입니다.
          </label>
        </div>
        <div class="checkbox">
          <label>
            <input type="checkbox" value="">
            체크박스는 다중 선택이 가능합니다.
          </label>
        </div>

        <h5> input type="radio"</h5>
        <div class="radio">
          <label>
            <input type="radio" name="optionsRadios" id="optionsRadios1" value="option1" checked>
            여기는 라디오 속성이 적용되는 곳입니다.
          </label>
        </div>
        <div class="radio">
          <label>
            <input type="radio" name="optionsRadios" id="optionsRadios2" value="option2">
            라디오 속성은 여러 개 중 하나를 선택할 경우 사용합니다.
          </label>
        </div>

        <h5> 인라인 체크 박스 label class="checkbox-inline"</h5>  
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox1" value="option1"> 1
        </label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox2" value="option2"> 2
        </label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox3" value="option3"> 3
        </label>

        <h5> 인라인 라디오 label class="radio-inline"</h5>  
            <label class="radio-inline">
               <input type="radio" name="optionsRadios" id="optionsRadios1" value="option1" checked>  r1
            </label>
            <label class="radio-inline">
               <input type="radio" name="optionsRadios" id="optionsRadios1" value="option1" checked>  r2
            </label>
            <label class="radio-inline">
               <input type="radio" name="optionsRadios" id="optionsRadios1" value="option1" checked>  r3
            </label>


        <h5> select는 기본값과 multiple 적용이 가능합니다.</h5>
        <select class="form-control">
          <option>1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
          <option>5</option>
        </select>
         <br>
        <select multiple class="form-control">
          <option>1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
          <option>5</option>
        </select>  
        <h5>폼에 텍스트를 삽입 하기 위해선 p class="form-control-static" 속성을 적용한다. </h5>
        <form class="form-horizontal" role="form">
          <div class="form-group">
            <label class="col-sm-2 col-lg-2 control-label">이메일</label>
            <div class="col-sm-10 col-lg-10">
              <p class="form-control-static">email@example.com</p>
            </div>
          </div>
          <div class="form-group">
            <label for="Password" class="col-sm-2 col-lg-2 control-label">비밀번호</label>
            <div class="col-sm-10 col-lg-10">
              <input type="password" class="form-control" id="inputPassword" placeholder="Password">
            </div>
          </div>
        </form>
        <h5>form-control-static을 적용하지 않을 경우 텍스트가 label 부분과의 정렬이 틀어진다. </h5>
        <form class="form-horizontal" role="form">
          <div class="form-group">
            <label class="col-sm-2 col-lg-2 control-label">이메일</label>
            <div class="col-sm-10 col-lg-10">
              <p>email@example.com</p>
            </div>
          </div>

         <h5> input 부분이 disabled 상태일 때</h5>
        <input type="text" class="form-control" disabled placeholder="이 부분은 disabled 상태입니다.">   

        <hr>
        <form class="form-horizontal" role="form">  
        <fieldset>
          <legend>기본정보 </legend>
        <div class="form-group">   
            <label for="Name" class="col-xs-2 col-lg-2 control-label">이름</label>
            <div class="col-xs-10 col-lg-10">
                <input type="text" class="form-control" placeholder="이름">
            </div>
        </div>
        <div class="form-group">   
            <label for="email" class="col-xs-2 col-lg-2 control-label">이메일</label>
            <div class="col-xs-10 col-lg-10">
                <input type="email" class="form-control" placeholder="이메일">
            </div>
        </div>
        </fieldset>
        <fieldset disabled>
         <legend>부가정보 </legend>      
        <div class="form-group">  
            <label for="address" class="col-xs-2 col-lg-2 control-label">주소</label>
            <div class="col-xs-10 col-lg-10">
                <input type="text" class="form-control" placeholder="주소">
            </div>
          </div>
        </fieldset>         
        </form>

       <hr>
       <h5> input 값에 다양한 메시지를 담을 수 있다.  </h5>
        <div class="form-group has-success">
          <label class="control-label" for="inputSuccess">Input값이 성공적일(문제없을) 경우</label>
          <input type="text" class="form-control" id="inputSuccess">
        </div>
        <div class="form-group has-warning">
          <label class="control-label" for="inputWarning">Input 값에 문제가 있어 경고를 내보낼 경우 </label>
          <input type="text" class="form-control" id="inputWarning">
        </div>
        <div class="form-group has-error">
          <label class="control-label" for="inputError">Input값에 에러가 있을 때 </label>
          <input type="text" class="form-control" id="inputError">
        </div>

        <hr>
        <h5> input-lg, 기본값, input-sm 일 경우 크기 비교  </h5>
          <input type="text" class="form-control input-lg" placeholder="input-lg">  <br>   
          <input type="text" class="form-control" placeholder="기본값">           <br>       
          <input type="text" class="form-control input-sm" placeholder="input-sm">  


        <hr>
        <h5> 그리드 시스템을 이용해서 컬럼 크기 조절 </h5>
        <div class="row">
          <div class="col-sm-2 col-lg-2">
            <input type="text" class="form-control" placeholder="col-sm-2 col-lg-2">
          </div>
          <div class="col-sm-3  col-lg-3">
            <input type="text" class="form-control" placeholder="col-sm-3  col-lg-3">
          </div>
          <div class="col-sm-4  col-lg-4">
            <input type="text" class="form-control" placeholder="col-sm-4  col-lg-4">
          </div>
        </div>  

        <hr>
        <h5> input 부분에 대한 도움말 </h5>
         <input type="text" class="form-control" placeholder="핸드폰 번호">   
         <span class="help-block"> 이 예문은 양용석 저자의 '부트스트랩으로 디자인하라'에서 참고하였습니다.</span>        
     <div style="height:100px"></div>    
 </div>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
