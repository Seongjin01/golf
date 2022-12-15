# 5월 산업기사 기출문제

![image](https://user-images.githubusercontent.com/102296551/207213940-207f4200-7480-488e-ad5a-e89caeaa9f18.png)

골프연습장 회원관리 프로그램 제작

# index.jsp

![image](https://user-images.githubusercontent.com/102296551/207214076-8e071173-6a1a-41a4-bbe4-a3cb042c0e1e.png)

그냥 index.jsp 페이지에 모든걸 만들어도 되지만, 다른 페이지들에도 header, nav, section, footer부분이 나타나야 하므로 <br>
layout으로 분류하여 header, nav, section, footer을 각각 따로 제작 하였다. <BR>

![image](https://user-images.githubusercontent.com/102296551/207214216-582bc721-757f-40f0-ba34-f68783e57755.png)

# css

css는 보기 편하게 위치선정을 하고 색감을 추가하여 직관적으로 보이게 제작하였다.

```css
@charset "UTF-8";
* { margin:0; padding: 0; }
ul, li { list-style: none; }
a { text-decoration: none; color: #fff; }
table, th, td { border: 1px solid #000; text-align: center; }
th, td { padding: 5px; }
body { background: lightgrey; }

#header {
	width: 100%;
	height: 80px;
	line-height: 80px;
	text-align: center;
	color: #fff;
	background: blue;
}

#nav {
	width: 100%;
	height: 40px;
	line-height: 40px;
	background: skyblue;
}
#nav ul li {
	float: left;
	margin: 0 10px;
}

#section {
	width: 100%;
}
#section h2 {
	text-align: center;
	margin: 30px 0 20px 0;
}
#section p {
	margin-left: 5px;
}
#section table {
	margin: 0 auto;
}
#section table.inputTable tr:not(:last-child) td {
	text-align: left;
}

#footer {
	width: 100%;
	height: 30px;
	line-height: 30px;
	text-align: center;
	position: fixed;
	left: 0;
	bottom: 0;
	font-size: 11px;
	background: blue;
	color: #fff;
}
```

# Teacher_list.jsp

강사조회 페이지는 말그대로 강사를 조회하기 위한 페이지로 주어진 조건대로 <br>
table을 작성합니다.

```
String sql ="select teacher_code, teacher_name, class_name,'$'||to_char(class_price, '999,999')class_price,substr(teach_resist_date,1,4)||'년'||substr(teach_resist_date,5,2)||'월'|| substr(teach_resist_date,7,2)||'일' teach_resist_date from tbl_teacher_202201";
```
쿼리문으로 조건을 작성하였습니다.

![image](https://user-images.githubusercontent.com/102296551/207218419-5a6bc01c-b02c-4d4c-afea-755cd4b0a5cb.png)

^- 결과

# class_Reg.jsp

수강신청 페이지는 수강을 신청하기 위한 강사선정, 일자, 회원번호 등을 입력하는 페이지입니다.

![image](https://user-images.githubusercontent.com/102296551/207218824-77d5cdc4-d182-4f58-9d4d-cb7ce8ece309.png)

총 제작 화면

```javascript
function chkVal() {
		var cls = document.classData;
		
		if(!cls.resist_month.value) {
			alert("수강월이 입력되지 않았습니다!");
			cls.resist_month.focus();
			return false;
		}
		if(cls.c_name.value=="none") {
			alert("회원명이 선택되지 않았습니다!");
			cls.c_name.focus();
			return false;
		}
		if(!cls.class_area.value) {
			alert("강의장소가 입력되지 않았습니다!");
			cls.class_area.focus();
			return false;
		}
		if(cls.class_name.value=="none") {
			alert("강의명이 선택되지 않았습니다!");
			cls.class_name.focus();
			return false;
		}
	}
```

javascript를 이용하여 input box가 비어있는지 체크하는 스크립트를 작성하였습니다.

```javascript
function re() {
		alert("정보를 지우고 처음부터 다시 입력 합니다!");
		document.classData.reset();
		document.classData.resist_month.focus();
	}
  ```
  다시쓰기버튼을 누르면 실행되는 결과
  
  ```javascript
  
 	function calTuition(tcode) {
		var mbr = document.classData.c_no.value;
		if(!mbr) {
			alert("회원명을 먼저 선택하세요.");
			document.classData.class_name[0].selected = true;
			document.classData.c_name.focus();
		} else {
			
			var salePrice = 0;
			switch (tcode) {
				case "100":
					salePrice = 100000;
					break;
				case "200":
					salePrice = 200000;
					break;
				case "300":
					salePrice = 300000;
					break;
				case "400":
					salePrice = 400000;
					break;
			}
			
			if(mbr.charAt(0)=='2') {
				alert("수강료가 50% 할인 되었습니다.");
				salePrice = salePrice / 2;
			}
			
			document.classData.tuition.value = salePrice;
		}
	}
  ```
  
  회원명이 선택되어있지 않으면 선택하라는 alert창을 띄워주고 <br>
  강의명에 따라 100, 200, 300, 400이 선택되고 알맞는 수강료가 바로 채워집니다. <br>
  만약 mbr.charAt(0)=='2' 라면 수강료가 50% 할인된다는 alert창이 띄워지고 가격도 (가격)/2로 50% 할인됩니다.
  
  ```javascript
  function vDisplay(code) {
		document.classData.c_no.value = code;
		document.classData.class_name.value = "none";
		document.classData.tuition.value = "";
	}
```
회원명 드롭다운 메뉴에서 이름마다 있는 벨류값을 받아와 값을 입력하는 함수인데, <br>
드롭다운에서 회원명은 그 메뉴를 뜻하기 때문에 따로 벨류값이 없으므로 none을 입력한다.
  
  
