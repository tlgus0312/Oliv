# Oliv
4/10 주제 선정
올리브영 감성 분석 
올리브영 스킨 케어 리뷰 감성 분석을 통한 제품 개선 및 마케팅 전략 제안 

1.카테고리별(토너, 에센스,크림) 감정 분포 차이 
2.민감성 피부 관련 부정 키워드 집중 분석 
3.감정 점수 기반 TOP 제품 Vs 부정 키워드 많은 제품 비교

리뷰 속에서 부정 키워드를 분석하고 개선 포인트와 긍정 포인트를 도출하여 
마케팅 문구에 추천 

5/7 크롤링이 안되서, HTML을 분석

*전체 플로우
1.카테고리 진입
스킨케어-> 스킨/토너, 에센스/세럼/앰플, 크림
category ID로 이동
스킨/토너:100000100010013
에센스/세럼/앰플:100000100010014
크림:100000100010015

2.상품 리스트 크롤링 
<ul class="cate_pre_list gtm_cate_list"> 안의 <li> 태그들 전체 수집
각각의 상품 링크 추출 후 진입

3.리뷰 크롤링
상품 상세 페이지에서 리뷰 탭 클릭:<a class="goods_reputation">리뷰</a>
리뷰 영역: <div class="review_list_wrap"> → <ul id="gdasList">
리뷰 텍스트: .review_cont .txt_inner
평점:.review_cont .point
페이지네이션:
<div class="pageing">
각 페이지 순차 클릭 (없으면 종료)

  
홈페이지 이동 https://www.oliveyoung.co.kr/store/main/main.do?oy=0
<a href="#" class="main_menu" data-attr="공통^메인롤링^스킨케어" data-trk="/">스킨케어</a>를 클릭하면

https://www.oliveyoung.co.kr/store/display/getCategoryShop.do?dispCatNo=10000010001&t_page=%EB%93%9C%EB%A1%9C%EC%9A%B0_%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC
&t_click=%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC%ED%83%AD_%EB%8C%80%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC&t_1st_category_type=%EB%8C%80_%EC%8A%A4%ED%82%A8
인 스킨케어로 이동

카테고리 
<div id= "Container"-> div id ="Contnets"-> div class ="ct-main"-> div class ="ct-menu"->p vlass ="ct-heading">스킨케어</p>
<ul class = "list"> -> 리스트를 세개를 moveCategory뒤에 있는것을 가져온다.  
<li>
<a href="javascript:common.link.moveCategory('100000100010013', 'Cat100000100010013_MID','',{ t_page: '카테고리관', t_click: '카테고리상세_중카테고리', t_1st_category_type: '대_스킨케어', t_2nd_category_type: '중_스킨/토너' })" class="100000100010013" onclick="javascript:categoryShop.detail.setBindWlogEvent('mcategory', 1);" data-attr="카테고리관^카테고리리스트^스킨/토너^1" data-trk="/">
<span>스킨/토너</span></a>
</li>

일단 하나 스킨/토너를 누르고 
![캡처333333](https://github.com/user-attachments/assets/3a122c5d-e3e2-43c6-8d4c-89fbb3b533d1)
<ul class="cate_pre_list gtm_cate_list"> 안에 있는  <li criteo-goods="A000000222334001" class="flag" data-index="0" data-number="1"> 이거 전체
<li criteo-goods="A000000222334001" class="flag" data-index="1" data-number="2">
이걸 전체를 가져와야된다. 하나씩 누르면서 리뷰쪽에 있는것을 다 긁어모은다. 상품에 들어간 것에서 리뷰를 클릭한다.
<a href="javascript:;" class="goods_reputation" data-attr="상품상세^상품상세_SortingTab^리뷰">리뷰<span>(18,236)</span></a>
리뷰를 클릭

div vlass ="review_list_wrap">에서 ul class inner_list id = gdasList
<li>
div class="review_cont" -> <div class="txt_inner"></div>->여기에 있는 내용을 가져와야한다. 

<span class="point" style="width:100%">5점만점에 5점</span>->이것도 가져오면 된다. 
<li></li>에 있는것을 전체적으로 계속 가져오게 해야됨
 끝나면 <div class="pageing" style="display: block;"><strong title="현재 페이지">1</strong>
<a href="javascript:void(0);" data-page-no="2">2</a><a href="javascript:void(0);" data-page-no="3">3</a>
<a href="javascript:void(0);" data-page-no="4">4</a><a href="javascript:void(0);" data-page-no="5">5</a><a href="javascript:void(0);" data-page-no="6">6</a>
<a href="javascript:void(0);" data-page-no="7">7</a>

5/8 완성

