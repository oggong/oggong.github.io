---
layout: post
title:  "0531-[Web]-bootstrap(4)"
subtitle:   "0531-bootstrap(4)"
categories: devlog
tags: web

---

## bootstrap (4)

<hr style="height: 1px; background: skyblue; "/>

#### toggletab

~~~

<!doctype html>
<html lang="ko-kr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>부트스트랩</title>
    <link href="./css/bootstrap.min.css" rel="stylesheet">

    <style>
    h2 { margin: 20px 0}
    .tab-content {padding: 10px 0;}
    </style>

  </head>
<body>
 <div class="container">  
    <h2>토글되는 탭 </h2>

    <ul class='nav nav-tabs'>
      <li><a href="#home" data-toggle="tab">독도</a></li>
      <li><a href="#tab1" data-toggle="tab">독도이름</a></li>
      <li><a href="#tab2" data-toggle="tab">독도의 지형</a></li>
      <li><a href="#tab3" data-toggle="tab">독도의 우편</a></li>
    </ul>

  <!-- 중요: 위의 a href에서 연결되는 이름과 보여줄 id값이 동일해야 한다.  -->
  <div class='tab-content'>
    <div class='tab-pane active' id="home">
      <h3>독도 이야기 1</h3>
			울릉도 동남쪽 87.4㎞[4] 바다 위에 있는 대한민국 영토를 총칭한다. 날씨가 좋을 때 울릉도의 고지대에서 맨눈으로 볼 수 있다. 대한민국 정부의 실효지배 지역 중 한반도 본토에서 가장 멀리 떨어져 있다.[5]
			일본에서는 이 섬이 한국 영토가 아니라 시마네 현 오키 군 오키노시마 정(오키 제도)에 딸린 섬 '다케시마(竹島)'며 대한민국이 강제 점령하고 있으니 돌려받아야 한다고 억지스러운 주장을 한다. 이로 말미암아 벌어지는 외교 분쟁이 유명하다.[6] 반면 대한민국은 독도에 대해서 애초에 영토 분쟁은 없으며, 따라서 분쟁조차 되지 않는다는 입장을 명백히 하고 있으며 실효지배 또한 줄곧 대한민국이 하고 있다.
			북한 역시 한국이 불법 점거하고 있다고 하는데 일본과는 성격이 아주 다르다. 단지 휴전선 남쪽에 있어서 불법 점거 지역에 쏙 들어가버린 것. 즉, 조국이 남북으로 갈라져서 불법 점거 영토가 된 것이지, 근본적으로는 한민족 고유 영토라는 입장은 한국과 같다. 이 때문에 일본 주장에는 남북 모두 고유 영토인데 일본은 먹으려 들지 말라며 한 목소리를 내고 있다.   
    </div>
    <div class='tab-pane' id="tab1">
      <h3>독도 이야기 2</h3>
			한자로는 홀로 독(獨)자를 쓴다. 하지만 독도의 한자표기는 이런 한자 뜻과는 상관없이 그저 한자의 소리를 빌려 쓴 음차로, 진짜 뜻은 돌(石)의 서남 방언인 '독'이다[7]. '돌로 된 섬'이란 소리.[8] 독도는 동도(東島)와 서도(西島)라는 큰 두 암초와 크고 작은 89개 부속도서로 나뉜다. 실제로는 암초 하나로 이루어진 것이 아니라는 소리. 따지고 보면 노래 독도는 우리땅의 첫 소절인 '외로운 섬 하나'는 잘못된 셈이다. 물론 절해고도(絶海孤島)란 점에서 보면 '외로운 섬'이라는 이름도 어울리기는 하다.
  	</div>
	 <div class='tab-pane' id="tab2">
      <h3>독도 이야기 3</h3>
			많은 사람들이 잘 모르는 사실이지만 화산 분화로 형성되었고 지질학적 높이가 2,000m에 이른다. 수백만 년 전 신생대에 동해에서 분출한 화산이 오랜 세월이 지나면서 풍화되어 화산의 모습이 거의 다 사라지고, 나머지 부분은 평균 수심이 깊은 동해에 가려 잘 보이지 않는 것. 마찬가지로 화산섬인 울릉도는 여전히 화산의 모습이 희미하게나마 있다.[11] 독도의 해저 지형
	 </div>
    <div class='tab-pane' id="tab3">
      <h3>독도 이야기 4</h3>
	      독도경비대 및 1가구가 거주하며, 일대에 천연가스, 메탄 하이드레이트 등 자원이 풍부한 것으로 알려져 있다. 행정구역상 주소는 대한민국 경상북도 울릉군 울릉읍 독도리. 시설물로는 RKDD라는 ICAO 코드를 받은 헬리콥터 포트와 # 노무현 정부 시기 만들어진 접안시설, 어민숙소 등이 있다. 접안시설은 확장될 예정이다. RK**는 대한민국의 공항을 뜻하는 국가 코드이다. 일본은 RJ**.
		 독도에도 우체통이 있다. 이 우체통에 투함된 우편물은 2개월에 한 번 독도경비대함이 들어올 때 집배원이 수거한다. 서울 영등포구 기준으로 독도에서 투함한 우편물이 오는 경로는 독도⇨울릉우체국⇨포항우편집중국⇨대전교환센터⇨서서울우편집중국⇨영등포우체국⇨배달이다. 우편번호는 개정 전 6자리 번호가 799-805, 2015년 개정 후 5자리 번호는 40240이다.
      </div>
</div>

</div>
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="./js/bootstrap.min.js"></script>


</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### carousel

~~~

<!doctype html>
<html lang="ko-kr">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>부트스트랩</title>
    <link href="./css/bootstrap.min.css" rel="stylesheet">
    <style>
    h2 { margin: 20px 0}
    </style>

  </head>
<body>
 <div class="container">

    <h2>캐러셀 슬라이드 효과  </h2>
        <div id="carousel-example-generic" class='carousel slide' >
            <!-- Indicators -->
            <ol class='carousel-indicators '>
              <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
              <li data-target="#carousel-example-generic" data-slide-to="1"></li>
              <li data-target="#carousel-example-generic" data-slide-to="2"></li>
            </ol>

             <!-- Carousel items -->
             <div class='item carousel-inner'>
                <div class="item active">
                   <img src="./images/slide1.jpg" alt="First slide">
                </div>
                <div class="item">
                   <img src="./images/slide2.jpg" alt="Second slide">               
                </div>
                <div class="item">
                   <img src="./images/slide3.jpg" alt="Third slide">                 
                </div>
             </div>

            <!-- Controls -->
              <a class="left carousel-control" href="#carousel-example-generic" data-slide="prev">
                <span class="icon-prev"></span>
              </a>
              <a class="right carousel-control" href="#carousel-example-generic" data-slide="next">
                <span class="icon-next"></span>
              </a>
          </div>
  </div>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="./js/bootstrap.min.js"></script>
    <script>
      $('.carousel').carousel({
    	  interval:3000
      })
    </script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### component

~~~

<!--
이 페이지는  http://bootstrapk.com/components/ 에 있는 내용을 여기에 복사해서 확인하세요.
 -->


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



	<!--  ............................................................................  -->

    <!-- jQuery (부트스트랩의 자바스크립트 플러그인을 위해 필요합니다) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
    <!-- 모든 컴파일된 플러그인을 포함합니다 (아래), 원하지 않는다면 필요한 각각의 파일을 포함하세요 -->
    <script src="js/bootstrap.min.js"></script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### dropdown

~~~

<!doctype html>
<html lang="ko-kr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>부트스트랩</title>
    <link href="./css/bootstrap.min.css" rel="stylesheet">
  </head>
<body>
 <div class="container">  
<h1> 드롭다운 </h1>

<hr>
<h4> 네비게이션 바 드롭다운 </h4>
    <nav role="navigation" class='navbar navbar-default'>
      <!-- Brand and toggle get grouped for better mobile display -->
      <div class='navbar-header'>
        <button class='navbar-toggle' type="button" data-toggle="collapse" data-target=".navbar-ex1-collapse">
          <span class="sr-only">Toggle navigation</span> <!-- sr-xxx : 라벨숨기는 것인데 시각장애인을 위한 screen reader에서 사용하도록  -->
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class='navbar-brand' href="#">로고 </a>
      </div>

      <!-- Collect the nav links, forms, and other content for toggling -->
      <div class="collapse navbar-collapse navbar-ex1-collapse">
        <ul class='nav navbar-nav'>
          <li class='dropdown'>
            <a class='dropdown-toggle' href="#" data-toggle="dropdown">메뉴 1 <b class="caret"></b></a>
            <ul class='dropdown-menu'>
              <li><a href="#">서브메뉴 1</a></li>
              <li><a href="#">서브메뉴 2</a></li>
              <li><a href="#">서브메뉴 3</a></li>
            </ul>
          </li>
          <li>
            <a class='dropdown-togle' href="#"  data-toggle="dropdown">메뉴 2 <b class="caret"></b></a>
            <ul class='dropdown-menu'>
              <li><a href="#">서브메뉴 1</a></li>
              <li><a href="#">서브메뉴 2</a></li>
              <li><a href="#">서브메뉴 3</a></li>
            </ul>
		</li>
          <li>
            <a class='dropdown-toggle' href="#" data-toggle="dropdown">메뉴 3 <b class="caret"></b></a>
            <ul class='dropdown-menu'>
              <li><a href="#">서브메뉴 1</a></li>
              <li><a href="#">서브메뉴 2</a></li>
              <li><a href="#">서브메뉴 3</a></li>
            </ul>
          </li>
        </ul>


      </div><!-- /.navbar-collapse -->
    </nav>



</div>
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="./js/bootstrap.min.js"></script>

</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### nav_sample

~~~

<!doctype html>
<html lang="ko-kr">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title> 우리 가게  </title>
    <link href="./css/bootstrap.min.css" rel="stylesheet">

  <!-- 부트스트랩을 이용하여 만들고 나서도 화면을 수정하고자 css를 추가해야 한다  -->

    <style>
    @import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);
    .navbar{ background-color: #fff; border: none; padding-bottom: 10px;  font-family: 'Nanum Gothic', sans-serif; font-weight: 300; font-size: 18px;height: 90px; text-transform: capitalize; border-bottom: 1px solid #AAAAAA}
    .navbar-toggle {position: relative;margin-top: 40px;top: 2px;}
    .navbar-nav { padding-right: 10px;margin-top: 20px; background-color: #fff}
    .navbar-nav li { margin:0 20px; }

   #carousel-example-generic {
   	margin-top: 50px;
   	width: 100%;
   	height: 450px;
   }

   #carousel-example-generic img {
   	margin-left: 300px;
   	width:600px;
   	height: 400px;
   }
    </style>


  </head>
<body>
  <div class="container-fluid">
    <!-- nav bar 부분 -->
    <div class="container">
          <nav class="navbar navbar-default navbar-fixed-top" role="navigation" id="navbar-scroll">
            <div class="container">
            <!-- Brand and toggle get grouped for better mobile display -->
            <div class="navbar-header">
              <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-1-collapse">                
              </button>
              <a class="navbar-brand" href="#"><img src="./images/logo.png" alt="9PixelStudio"> </a>
            </div>

            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse navbar-right navbar-1-collapse">
              <ul class="nav navbar-nav">
                <li><a href="#"> 우리가게 소개 </a></li>  
                <li><a href="#"> 주력상품 </a></li>  
                <li><a href="#"> 소소한 이야기 </a></li>  
                <li><a href="#"> 찾아오시는 길 </a></li>                  
              </ul>
            </div>
            </div><!-- /.navbar-collapse -->
          </nav>
     </div>   
    <!-- // nav bar 부분 끝 -->

    <!-- 케라셀 부분 -->
 <div id="carousel-example-generic" class='carousel slide' >
            <!-- Indicators -->
            <ol class='carousel-indicators '>
              <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
              <li data-target="#carousel-example-generic" data-slide-to="1"></li>
              <li data-target="#carousel-example-generic" data-slide-to="2"></li>
            </ol>

             <!-- Carousel items -->
             <div class='item carousel-inner'>
                <div class="item active">
                   <img src="./images/slide1.jpg" alt="First slide">
                </div>
                <div class="item">
                   <img src="./images/slide2.jpg" alt="Second slide">               
                </div>
                <div class="item">
                   <img src="./images/slide3.jpg" alt="Third slide">                 
                </div>
             </div>
   	<!--케러셀 끝-->

   	<!-- 썸네일 이미지 추가 -->
   	<div class='row'>
   		<div class='col-md-3 col-xs-6'>
   			<a href='#' class='thumbnail'>
   				<img src='./images/slide1.jpg' alt='' class='img-circle'/>
   			</a>
   		</div>
   		<div class='col-md-3 col-xs-6'>
   			<a href='#' class='thumbnail'>
   				<img src='./images/slide2.jpg' alt='' class='img-circle'/>
   			</a>
   		</div>
   		<div class='col-md-3 col-xs-6'>
   			<a href='#' class='thumbnail'>
   				<img src='./images/slide3.jpg' alt='' class='img-circle'/>
   			</a>
   		</div>
   		<div class='col-md-3 col-xs-6'>
   			<a href='#' class='thumbnail'>
   				<img src='./images/slide4.jpg' alt='' class='img-circle'/>
   			</a>
   		</div>
   	</div>

  </div>
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="./js/bootstrap.min.js"></script>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>

#### googlemap

~~~

<!DOCTYPE html>
<html>
<head>
 <meta name="viewport" content="initial-scale=1.0, user-scalable=no">
 <meta charset="euc-kr">
 <title>구글맵 API 활용하기</title>
 <script src="https://maps.googleapis.com/maps/api/js?sensor=false"></script>
 <script>
 function initialize() {

 /*
		구글 지도에서 목적지를 찾고 오른쪽 마우스에서 '이곳이 궁금한가요?'에서 좌표값을 구한다
 */
 var Y_point = 37.486525; // Y 좌표
 var X_point = 127.020683; // X 좌표
 var zoomLevel = 17; // 첫 로딩시 보일 지도의 확대 레벨
 var markerTitle = "목적지"; // 현재 위치 마커에 마우스를 올렸을때 나타나는 이름
 var markerMaxWidth = 300; // 마커를 클릭했을때 나타나는 말풍선의 최대 크기


 var myLatlng = new google.maps.LatLng(Y_point, X_point);
 var mapOptions = {
 zoom: zoomLevel,
 center: myLatlng,
 mapTypeId: google.maps.MapTypeId.ROADMAP
 }
 var map = new google.maps.Map(document.getElementById('map_view'), mapOptions);

 var marker = new google.maps.Marker({
 position: myLatlng,
 map: map,
 title: markerTitle
 });

 var infowindow = new google.maps.InfoWindow(
 {
 content: '여기',
 maxWidth: markerMaxWidth
 }
 );

 google.maps.event.addListener(marker, 'click', function() {
 infowindow.open(map, marker);
 });
 }
 </script>
</head>

<body onload="initialize()">
 <div id="map_view" style="width:500px; height:300px;"></div>
</body>
</html>

~~~

<hr style="height: 1px; background: skyblue"/>
