---
layout: post
title:  "06-12-[jquery]-5.tabs"
subtitle:   "0612-jQuery-tabs"
categories: devlog
tags: jquery

---

## tabs

<hr style="height: 1px; background: skyblue; "/>

#### js/scripts.js

~~~


$(document).ready(function() {
	// var anchors =$('.tabSet a');
	var anchors = $('.tabSet').find('a');
	var panelDivs = $('.tabSet').find('div.panel');

	anchors.show();
	panelDivs.hide();

	var lastAnchor = anchors.filter('.on');
	var lastPanel = $(lastAnchor.attr('href'));
	lastPanel.show();

	anchors.click(function(){
		panelDivs.hide();
		// 모두 안보이게 하고
		anchors.attr('Class','');
		// 모든 클래스에 빈값을 주고
		$(this).attr('Class','on');
		// 클릭한 곳에 class 추가하고
		$($(this).attr('href')).show();
		// 클릭한 곳의 panel을 보여주기
	});

})

~~~

<hr style="height: 1px; background: skyblue"/>

#### css/styles.css

~~~

*{
	margin:0;
	padding:0;
	list-style-type:none;
}
body{
	padding:1.5em 2em;
	line-height:1.4;
	font-family:Arial, Helvetica, sans-serif;
}
.all{
	width:610px;
}
.tabSet{
	padding:0 0 1em;
	border:2px solid #666;
	margin:0 0 20px;
	padding:3px;
	border-radius:4px;
}
ul{
	overflow:hidden;
	padding:12px 12px 0;
	background:#000 url(bg1.png) repeat-x 0 0;
	border-radius:4px;
	*zoom:1; /* ie clear float */
}
	ul li{
		float:left;
		padding:0 4px 0 0;
	}
		ul li a{
			float:left;
			color:#333;
			background:#aaa;
			padding:.45em 1.25em;
			display:none;
			border-radius:4px 4px 0 0;
			text-shadow:0 0 3px #fff;
			font-weight:bold;
			text-decoration:none;
			box-shadow:0 0 5px #444;
		}
		ul li a:hover{
			text-decoration:underline;
		}
		ul li a.on{
			background:#fff;
			color:#333;
			cursor:default;
		}
		ul li a.on:hover{
			text-decoration:none;
		}
.panel{
	background:#fff;
	padding:.75em 15px .4em;
	margin:0 0 .5em;
	width:570px;
}



~~~

<hr style="height: 1px; background: skyblue"/>


#### jquery_test.html

~~~

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8" />
<title>jQuery test</title>
<link rel="stylesheet" type="text/css" href="css/styles.css" />
<script type="text/javascript" src="../lib/jquery-3.4.1.min.js"></script>
<script type="text/javascript" src="/WebUI/5_jquery_class/9_plugin/0_basic/js/jquery.red.js"></script>
</head>
<body>

	<div class="tabSet">
		<ul class="tabs">
			<li><a href="#panel1-1" class="on">첫번째</a></li>
			<li><a href="#panel1-2">두번째</a></li>
			<li><a href="#panel1-3">세번째</a></li>
			<li><a href="#panel1-4">네번째</a></li>
		</ul>
		<div class="panels">
			<div class="panel" id="panel1-1">Like all great travellers, I
				have seen more than I remember,and remember more than I have seen.
				훌륭한 여행가들이 흔히 그렇듯이 나는 내가 기억하는 것보다 많은 것을 보았고 또한 본 것보다 많은 것을 기억한다.
				Benjamin Disraeli(벤자민 디즈렐리)[영국 정치인/작가, 1804-81]</div>
			<div class="panel" id="panel1-2">Anything you're good at
				contributes to happiness. 당신이 잘 하는 일이라면 무엇이나 행복에 도움이 된다. Bertrand
				Russell(버트랜드 러셀)[英 철학자, 1872-1970]</div>
			<div class="panel" id="panel1-3">The computer is only a fast
				idiot; it has no imagination; it cannot originate action. It is, and
				will remain, only a tool of man. 컴퓨터는 민첩한 바보이다, 상상력도 없고 스스로 행동할 수도
				없다. 현재에도 미래에도 컴퓨터는 단지 인간의 도구일 뿐이다. American Library Association's
				1964 statement about the Univac (미국도서관협회의 Univac[전자계산기 상품명]에 관한
				1964년도 성명서)</div>
			<div class="panel" id="panel1-4">Business? It's quite simple.
				It's other people's money. 사업? 그건 아주! 간단하다. 다른 사람들의 돈이다. Alexandre
				Dumas(알렉산드르 듀마)</div>
			<!-- /panels -->
		</div>
		<!-- /tabset -->
	</div>


</body>
</html>



~~~

<hr style="height: 1px; background: skyblue"/>
