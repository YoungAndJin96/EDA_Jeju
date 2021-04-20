Fast Campus Data Science School 17th <EDA project>
## ✨The Analysis of Consumption & Commercial District in Jeju✨

![ppt](https://user-images.githubusercontent.com/71582831/115168106-cc00c900-a0f4-11eb-99c3-aa27a80c96b7.jpg)

## :pencil:개요
### 1️⃣ 주제 선정 목적
    - 제주도 소비/결제 데이터 및 지역별 업종 분석
    - EDA를 통한 요소별 상관관계 분석 및 인사이트 도출
  
### 2️⃣ Reference
    ① 제주도 업종별 매출 데이터
      - 출처: Dacon "공간정보 탐색적 데이터 분석 경진대회" 
        (https://dacon.io/competitions/official/235682/data/)
      - 목적: 지역별/시간대별 상세 업종 결제액 분석
    ② 제주도 금융 생활 데이터 
      - 출처: Dacon "KCB 금융스타일 시각화 경진대회"
        (https://dacon.io/competitions/official/82407/overview/description/) 
      - 목적: 직업, 소득, 연령 등 요소별 상관관계 분석
    ③ 제주도 내국인 관광객 지역, 업종, 성별, 연령대별 카드 이용 데이터 API 
      - 출처: 제주데이터랩 (https://www.jejudatahub.net/data/view/data/597)
    ④ 카카오 지도 API
      - 출처: kakao developers (https://developers.kakao.com/product/map)
      - 목적: pyproj 활용, ITRF2000 기준 좌표계를 경도/위도 기준값으로 변환
    ⑤ 제주도 호텔 데이터 크롤링
      - 출처: 부킹닷컴
      - 목적: 제주도 호텔 실 결제 데이터를 통해 관광객 선호 숙박 입지 분석 

---

## :page_with_curl: 목차

### CHAPTER 1) 제주도 소비생활 분석
  - 제주도는 제주도민과 관광객이 공존하는 지역
  - 고소득/고소비 제주도민과 관광객 공략을 위한 밀집 지역 탐색

#### Hypotheses

     H1: 제주도민과 관광객은 업종별 소비 특성에 차이가 있을 것이다.
     H2: 제주도민의 직업과 소득/소비는 상관관계가 있을 것이다.
     H3: 고소득/고소비층 소비자의 활동 영역은 밀집되어 있을 것이다.
       - H3-1: 고소득/고소비 제주도민의 거주지는 밀집되어 있을 것이다.
       - H3-2: 고소득/고소비 관광객이 묵는 숙박업소는 밀집되어 있을 것이다.
     H4: 특정 업종이 특화된 지역이 있을 것이다.
    
#### 서론 : 제주도민과 관광객의 소비 특성 비교
    - H1 결론: 제주도민과 관광객은 소비 금액 / 횟수 / 객수의 업종별로 비슷한 양상을 보인다.

#### 본론 : 고소득/고소비층 밀집 지역 탐색
    1. 제주도민
     - 소득과 소비력에 직결되는 요소로서 '직업' 선정
     - job points, job level 지표로, 직업과 소득/소비 상관관계 분석
       → med_income(0.6), avg_spend(0.5), avg_debt_credit(0.5),    
         vehicle_own_rat(0.4) 과 양의 상관관계
     - H2 결론: 직업과 소득/소비는 상당한 상관관계가 있다.
     - H3-1 결론: 고소득/고소비 제주도민의 거주지는 밀집되어 있는 경향이 있다.
  
    2. 관광객
     - 고소비층이 묵는 고급 호텔의 밀집지역 탐색
     - 숙박업 결제 데이터 및 부킹닷컴 제주도 호텔 크롤링 데이터 활용
     - H3-2 결론: 고소득/고소비 관광객이 묵는 숙박업소는 밀집되어 있는 경향이 있다.

#### 결론 : 고소득/고소비 소비자의 밀집 지역
    - H3 결론: 타켓 제주도민/관광객 거주지 및 숙박업소는 밀집되어 있는 경향이 있다.
    - CHAPTER 2에서 해당 지역에서 유망한 업종 탐색 지속

### CHAPTER 2) 제주도 유망 사업 업종 분석
  - CHAPTER 1에서 선정한 고소비층 밀집 지역 기준, 유망한 업종 탐색
  - 신규 개인 창업을 가정으로 아래 기준의 데이터 활용하여 분석 진행
  - 영세 상점의 실 결제 데이터 사용 / 제주시 내 10시 ~ 23시 사이 결제 / '소매업', '음식점업' 한정
  - Folium 지도 시각화를 통한 지역별/업종별 비교

#### 서론 : WHERE 어느 지역에서?
    - H3-1과 H3-2의 교집합 상위 8개 지역 선정
      : 성산읍, 남원읍, 애월읍, 연동, 한림읍, 안덕면, 이도이동, 조천읍

#### 본론 : WHAT 어떤 업종을?
    1. 8개 지역 매출 TOP 10 업종
     - 소비횟수 기준, 일반한식(50%), 서양음식(20%), 스넥(6%), 편의점, 농축수산품, 슈퍼마켓, 중국음식, 정장, 기타음료식품, 주점 순
    2. 8개 지역별 TOP 10 업종 분포 비교
     - 지역별 순위 또한 상기 TOP 10 업종 순위와 유사 (일반한식 > 서양음식 > 스넥 > 편의점)
    3. 주요 업종별 8개 지역 매출액 비교 (상위 3개 지역 기재)
      (1) 일반한식: 연동 > 애월읍 > 이도2동
      (2) 서양음식: 애월읍 > 안덕면 > 이도2동
      (3) 편의점: 한림읍 > 애월읍 > 이도2동
      (4) 정장: 이도2동 > 연동 > 한림읍
         ※ 제주도 웨딩 촬영용 맞춤 정장 및 대여 서비스 활성화

#### 결론 : 제주도 사업 인기 업종과 특화 지역
    - 매출액이 높은 업종(일반한식, 서양음식, 편의점, 정장)의 분포 상위 지역은 대체로 제주시에 위치
    - 매출액이 높은 8개 지역 중에서도 고소득/고소비 거주민 밀집도가 높은 지역 (연동, 이도2동)이 상위권을 차지
    - H4: 특정 업종이 특화된 지역이 있을 것이다.
      H4 결론: 
      지역의 특성에 따른 특정 업종 활성화보다는, 상권의 구매력이나 업종 자체의 매출액 규모이 중요한 요인으로 판단된다.
                

### EDA 프로젝트를 마치며...
     1. 한계점 및 아쉬운 점
       - 특정 업종/지역에 매출이 높다는 건 수요와 공급이 모두 많다는 뜻이고 이미 레드 오션일 수도 있으나,
         매출액이 높다는 것이 곧 인기가 많고 기회가 있는 것으로 가정
       - 제주도 업체 및 매출 데이터를 찾지 못하여, 고객 결제 데이터로 갈음
       - 데이터 양이 많아 위도/경도/동 이름 변환 소요 시간이 길어 데이터의 일부만 샘플링하여 진행
     2. 의의 및 느낀 점
       - Pandas DataFrame과 각종 시각화 툴(Matplotlib, Seaborn, Plotly, folium 등) 사용하여 데이터에 맞는 다양한 시각화 시도
       - 여러 개의 데이터 셋을 유기적으로 연계하여 분석 및 인사이트 도출
       - 크롤링 및 API 사용을 통해 필요한 데이터 수급 및 전처리 수행
       - 신혼여행 및 사진 촬영등으로 유명한 제주도의 특성에 따른 특이한 업종(ex 정장)을 발견
