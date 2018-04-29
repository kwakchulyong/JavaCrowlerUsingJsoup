# JavaCrowlerUsingJsoup
Java Crowler using jsoup
I called the menu at Kumoh National Institute of Technology's restaurant.
used the JSOUP Java library.

<h1>Before</h1>
<p>
https://jsoup.org/download

jsoup-1.11.2.jar <br/>
jsoup-1.11.2-javadoc.jar<br/>
jsoup-1.11.2-sources.jar<br/>
</p>
<h1>Source code</h1>
<h2>App.java</h2>
sample package>src/main/java/sample.sampe.App.java
<p>
        
    	String menuData = "20180425"; //Date(YYYYMMDD)
    	String menuType = "sikdang.do"; //sikdang.do:Student, sikdang2.do:Teacher
    	String URL = "https://www.kumoh.ac.kr/jsp/common/" + menuType +"?ilja=" + menuData;
        
        Document doc = Jsoup.connect(URL).timeout(3000).get();
        Elements menu = doc.select("div").select(".meal01").select("dl");
        
        ArrayList mealMenu = new ArrayList(); //0: Break Fast, 1:Lunch, 2:Dinner, 3:Sepcial
        if(menu.size() > 0) {
        	for(int i = 0; i< menu.size(); i++) {
        		mealMenu.add(menu.get(i).text());
        	}
        }
        
        System.out.println("==============================");
        System.out.println("조식 : " + mealMenu.get(0));
        System.out.println("중식 : " + mealMenu.get(1));
        System.out.println("석식 : " + mealMenu.get(2));
        if(menu.size() >3) {
        	System.out.println("일품요리 : " + mealMenu.get(3));	
        }
        
        System.out.println("==============================");
        Elements meal_foottime;
        
        if("sikdang.do".equals(menuType)) {
        	meal_foottime = doc.select("div").select(".meal_foottime").select("li");
        } else if("sikdang2.do".equals(menuType)) {
        	meal_foottime = doc.select("div").select(".meal_foottime2").select("li");
        } else {
        	meal_foottime = doc.select("div").select(".meal_foottime").select("li");
        }
        
        ArrayList timeData = new ArrayList(); //Timetable
        
        for(int i = 0; i<meal_foottime.size(); i++) {
        	timeData.add(meal_foottime.get(i).text());
        }
        
        System.out.println(timeData.get(0));
        System.out.println(timeData.get(1));
        
        if(meal_foottime.size() >2) {
        	System.out.println(timeData.get(2));
        }
        
        if(meal_foottime.size() >3) {
        	System.out.println(timeData.get(3));
        }
        System.out.println("==============================");
 </p>
<h2>output</h2>
<p>
        
        ==============================
        조식 : **교직원식당에서 이용가능 합니다(8:20~9:30)** ※ 식사준비인원 :
        중식 : 쌀밥(국내산) 얼큰콩나물국 파돈가스 오징어쫄면무침 맛김치(국내산)/요구르트 ※ 식사준비인원 :
        석식 : 짜장밥(국내산) 짬뽕국 탕수육(국내산) 쥐어채볶음 마카로니후르츠샐러드 단무지무침 ※ 식사준비인원 :
        일품요리 : 고기덮밥/ 된장찌개/ 비빔밥/ 순대국밥/ 김치볶음밥/ 콩나물불고기덮밥/ 된장찌개정식/ 닭갈비볶음밥
        ==============================
        조식 시간 : 08:30 ~ 09:30
        중식 시간 : 11:30 ~ 14:00
        석식 시간 : 17:30 ~ 18:30
        토·일,공휴일 : 09:00 ~ 18:00(학기중)
        ==============================
        
</p>

<h1>Reference site</h1>
<p>
https://www.tutorialspoint.com/jsoup/index.htm
 </p>
