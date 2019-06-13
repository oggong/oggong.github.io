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

#### button

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title> 기본 샘플 확인 </title>

    <!-- 부트스트랩 -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

</head>
<body>
	<!--  ............................................................................  -->   
 <div class="container">  

    <h4 class="text-primary"> 버튼 </h4>
      <button type="button" >클래스 선택자 적용하지 않는 경우  </button>
      <button type="button" class="btn">class="btn" 만 적용한 경우 </button>
    <hr>

    <h4 class="text-primary"> button 태그 사용 </h4>    
      <button type="button" class="btn btn-default">기본 버튼 모양 </button>
      <button type="button" class="btn btn-primary">중요한 버튼</button>       
      <button type="button" class="btn btn-success">긍정적 의미의 버튼</button>       
      <button type="button" class="btn btn-info">정보제공 버튼</button>       
      <button type="button" class="btn btn-warning">주의를 알리는 버튼 </button>       
      <button type="button" class="btn btn-danger">위험을 나타내는 버튼</button>       
      <button type="button" class="btn btn-link">단순 링크로 처리하는 버튼</button>      
      <hr>

    <h4 class="text-primary"> input 태그 사용 </h4>
      <input type="button" class="btn btn-default" value="기본 모양 버튼 ">
      <input type="button" class="btn btn-primary" value="중요한 버튼 ">
      <input type="button" class="btn btn-success" value="긍정적 의미의 버튼">
      <input type="button" class="btn btn-info" value="정보제공 버튼">      
      <input type="button" class="btn btn-warning" value="주의를 알리는 버튼  ">
      <input type="button" class="btn btn-danger" value="위험을 나타내는 버튼 ">
      <input type="button" class="btn btn-link" value="단순 링크로 처리하는 버튼 ">
      <hr>

    <h4 class="text-primary"> a 태그 사용 </h4>    
      <a href="#" class="btn btn-default" role="button">기본 모양 버튼 </a>
      <a href="#" class="btn btn-primary" role="button">중요한 버튼 </a>
      <a href="#" class="btn btn-success" role="button">긍정적 의미의 버튼 </a>
      <a href="#" class="btn btn-info" role="button">정보제공 버튼 </a>
      <a href="#" class="btn btn-warning" role="button">주의를 알리는 버튼</a>
      <a href="#" class="btn btn-danger" role="button">위험을 나타내는 버튼  </a>
      <a href="#" class="btn btn-link" role="button">단순 링크로 처리하는 버튼 </a>
      <hr>      

      <p>
        <button type="button" class="btn btn-primary">기본 버튼 </button>
        <button type="button" class="btn btn-info">기본 버튼 </button>
      </p>
      <p>
        <button type="button" class="btn btn-info btn-lg">큰 버튼</button>
        <button type="button" class="btn btn-success btn-lg">큰 버튼</button>
      </p>
      <p>
        <button type="button" class="btn btn-info btn-sm">작은 버튼</button>
        <button type="button" class="btn btn-primary btn-sm">작은 버튼</button>
      </p>
      <p>
        <button type="button" class="btn btn-info btn-xs">아주 작은 버튼</button>
        <button type="button" class="btn btn-warning btn-xs">아주 작은 버튼</button>
      </p>

      <hr>

      <div>
        <button type="button" class="btn-block btn btn-info">화면 전체 버튼</button>
        <button type="button" class="btn-block btn btn-warning">화면 전체 버튼</button>
      </div>

	<hr>
	<!-- label은 클릭시 출력되는 조그마한 알림 같은 것   -->
	<div class='label label-primary'>위 예문은 부트스트랩 사이트과 양용석 저자의 '부트스트랩으로 디자인하라'에 정리된 내용입니다.</div>
	<div class='label label-info'>위 예문은 부트스트랩 사이트과 양용석 저자의 '부트스트랩으로 디자인하라'에 정리된 내용입니다.</div>

	<!-- 우리가 생각하는 라벨 -->
	<div class='alert alert-info'>위 예문은 부트스트랩 사이트과 양용석 저자의 '부트스트랩으로 디자인하라'에 정리된 내용입니다.</div>
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

#### table

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>기본 샘플 확인</title>

<!-- 부트스트랩 -->
<!-- 외부 css 먼저 -->
<link href="css/bootstrap.min.css" rel="stylesheet">

<!-- 내부 css 나중 -->
<style type="text/css">
/*  hover 로 색 변경 */
.table tr:nth-child(even) {
	background: #86E57F;
}
.table tr:hover{
	background:#B7F0B1;
}
</style>

</head>
<body>
	<!--  ............................................................................  -->

	<div>
		<h2 class="text-success">우리 스타 보기</h2>
		<!-- <table class='table table-bordered table-striped table-hover' >  -->
		<table class='table'>
			<thead>
				<tr>
					<th>ID</th>
					<th>이름</th>
					<th>직업</th>
					<th>특징</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td>203A</td>
					<td>샤이니</td>
					<td>가수</td>
					<td>[소속]SM엔터테인먼트 [멤버]온유, 종현, 키, 최민호, 태민 [데뷔]2008년 싱글 앨범 '누난 너무
						예뻐 (Replay)'</td>
				</tr>
				<tr>
					<td>141B</td>
					<td>소녀시대</td>
					<td>가수</td>
					<td>[멤버] 태연, 윤아, 수영, 효연, 유리, 티파니 영, 써니, 서현 [소속사] SM엔터테인먼트
						[데뷔]2007년 싱글 앨범 '다시 만난 세계'</td>
				</tr>
				<tr>
					<td>2031</td>
					<td>김수현</td>
					<td>배우</td>
					<td>탤런트, 영화배우 출생 1988년 2월 16일 (만 30세) 신체 180cm, 65kg | AB형</td>
				</tr>
				<tr>
					<td>007F</td>
					<td>국카스텐</td>
					<td>가수</td>
					<td>[멤버] 하현우(보컬, 기타), 전규호(기타), 김기범(베이스), 이정길(드럼) [소속사] 인터파크
						엔터테인먼트 [데뷔]2008년 싱글 앨범 'Guckkasten'</td>
				</tr>
			</tbody>
		</table>


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
