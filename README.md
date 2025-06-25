# Oliv

## 4/10 주제 선정  
**올리브영 스킨케어 리뷰 감성 분석을 통한 제품 개선 및 마케팅 전략 제안**  
1. 카테고리별(토너·에센스·크림) 감정 분포 차이  
2. 민감성 피부 관련 부정 키워드 집중 분석  
3. 감정 점수 기반 TOP 제품 vs. 부정 키워드 많은 제품 비교  

리뷰 속 부정 키워드를 분석하여 개선 포인트와 긍정 포인트를 도출하고,  
이를 바탕으로 마케팅 문구를 추천합니다.

---

## 전체 플로우

1. **카테고리 진입**  
   - 메인 → 스킨케어 클릭  
     ```
     https://www.oliveyoung.co.kr/store/main/main.do?oy=0
     <a class="main_menu" …>스킨케어</a>
     ```
   - 중분류 호출 파라미터
     - 스킨/토너: `dispCatNo=100000100010013`
     - 에센스/세럼/앰플: `dispCatNo=100000100010014`
     - 크림: `dispCatNo=100000100010015`
     ```
     https://www.oliveyoung.co.kr/store/display/getCategoryShop.do?dispCatNo=<ID>
     ```

2. **상품 리스트 크롤링**  
   - HTML 구조:
     ```
     div#Container
       └─ div#Contents
           └─ div.ct-main
               └─ div.ct-menu
                   ├─ p.ct-heading    <!-- “스킨케어” 제목 -->
                   └─ ul.list
                       └─ li > a.moveCategory(…dispCatNo, …)  <!-- 세 개 중분류 링크 -->
     ```
   - 중분류 페이지:
     ```
     ul.cate_pre_list.gtm_cate_list
       └─ li.flag[data-number="1"…]  <!-- 상품 1 -->
       └─ li.flag[data-number="2"…]  <!-- 상품 2 -->
       └─ … 
     ```
   - 각 `<li>`에서 상품 상세 URL 추출 후 진입

3. **리뷰 크롤링**  
   - 리뷰 탭 클릭:
     ```html
     <a class="goods_reputation" …>리뷰<span>(n)</span></a>
     ```
   - 리뷰 영역:
     ```html
     <div class="review_list_wrap">
       <ul id="gdasList" class="inner_list">
         <li>
           <div class="review_cont">
             <div class="txt_inner">…리뷰 텍스트…</div>
             <span class="point" style="width:XX%">…</span>
           </div>
         </li>
         <!-- 반복 -->
       </ul>
     </div>
     ```
   - 평점 계산:  
     ```python
     width = XX  # e.g. “80%”
     rating = (width.strip('%') / 100) * 5
     ```
   - 페이지네이션:
     ```html
     <div class="pageing">
       <strong title="현재 페이지">1</strong>
       <a data-page-no="2">2</a>
       …
       <a class="next" data-page-no="11">다음 10 페이지</a>
     </div>
     ```
   - 모든 페이지 순차 클릭하며 데이터 수집
     ![캡처 5555](https://github.com/user-attachments/assets/a06b1de4-d986-4110-9535-88ec51ac7cc5)
5/8 완성 csv저장

- 스킨/토너 -44144개 저장
- 에센스/세럼/앰플 -46326개저장
- 크림-42560개저장
- 아이크림-32106개저장
- 클렌징폼/젤 리뷰 46568개 저장
- 오일/밤 43564개 저장
- 워터/밀크  42102개 저장


![image](https://github.com/user-attachments/assets/d52aab29-013a-4348-a9cd-4d4c774dd539)
브랜드명/상품명/내용 크롤링 완료 
--
## 라벨링 처리과정
![캡처4444444444444444](https://github.com/user-attachments/assets/dbb79e10-56e6-4b1c-8ae2-5cc5dca9988c)
![캡처22](https://github.com/user-attachments/assets/fad31fb7-05cf-44d5-8deb-ad938a1b8203)

LSTM 감성분석을 하는데 label_studio로 200개 정도 수동으로 라벨작업을 하다가 
이게 맞나라는 생각이 들었다. 교수님이 주신거는 돌아가지 않아서 어떤점이 문제인가 살펴보도록하였다.

###  화장품 데이터의 특징 

![image](https://github.com/user-attachments/assets/5ce5da83-989d-46ed-85a9-5ca2f285098b) 

## 글이 김

![image](https://github.com/user-attachments/assets/1510de13-e794-45fb-90dd-11199f80fde6) 

## 장점, 단점, 후기가 모두 있음

![image](https://github.com/user-attachments/assets/54def414-6faa-4225-8a54-cf8d117346e4) 

## 이모티콘 있음


그리하여 속성기반으로 변경

화장품 리뷰 데이터를 활용하여 **속성 기반 감성 분석(Aspect-Based Sentiment Analysis, ABSA)** 을 수행하고, LSTM 기반 다중 레이블 분류 모델로 **제품별 기능 감성**을 자동 예측하는 파이프라인을 제공

[크롤링을 한거 가지고 학습모델 생성 및 감성분석 웹페이지 구경하기](https://github.com/tlgus0312/OlivFeeling)



