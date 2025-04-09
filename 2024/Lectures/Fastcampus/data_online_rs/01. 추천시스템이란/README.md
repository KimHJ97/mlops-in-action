# 추천 시스템이란

추천 시스템은 아이템 또는 사용자를 추천한다.  
아이템과 사용자 프로필은 추천 알고리즘을 위한 feature가 된다.  
추천 알고리즘은 아이템 또는 사용자를 점수화하는 것이다.  

 - __추천시스템의 등장__
    - 인터넷은 폭발적인 성장과 수많은 정보가 쏟아지는 공간
    - 인터넷 관련 비즈니스 활성화
        - e-Business, e-Commerce 등
    - 수많은 정보(+데이터)로 사용자가 적절한 결정을 내리기 어려움
 - __추천시스템의 정의__
    - 사용자로부터 선호도 여부를 데이터화
        - Explicit Feedback (평점)
        - Implicit Feedback (사용자의 행동 패턴)
    - 사용자의 선호도와 제한사항을 바탕으로 가장 적절한 아이템 점수 계산
    - 사용자에게 가장 관련 있는 아이템 순서대로 리스트 형태로 제시
 - __추천시스템 사용 사례__
    - 넷플릭스 콘텐츠 추천: 좋아하는 컨텐츠를 기반으로 콘텐츠 추천
    - 인스타그램 팔로우 추천: 팔로잉하고 있는 계쩡 유형과 피드에서 자주 클릭한 계정을 분석해 피드에 광고 노출
    - 쿠팡 상품 추천: 구매 목록, 상품 키워드, 클릭 상품을 기반으로 다양한 상품 추천

<br/>

### 추천시스템 알고리즘 종류

 - __Contents-based Recommender System(컨텐츠 기반 추천시스템)__
    - 사용자가 과거에 좋아했던 아이템을 파악하고, 그 아이템과 비슷한 아이템을 추천
    - ex) 스파이더맨에 4.5점 평점을 부여한 유저는 타이타닉보다 캡틴 마블을 더 좋아할 것이다.
 - __Collaborative Filtering(협업 필터링)__
    - 비슷한 성향 또는 취향을 갖는 다른 유저가 좋아한 아이템을 현재 유저에게 추천
    - 간단하면서 수준 높은 정확도를 나타냄
    - ex) 스파이더맨에 4.5점을 준 2명의 유저 -> 유저 A가 과거 좋아했떤 캡틴 마블을 유저 B에게 추천
 - __Hybrid Recommender System__
    - Content-based와 Collaborative Filtering의 장단점을 상호보완
    - Collaborative Filtering은 새로운 아이템에 대한 추천 부족
    - 이에, content-based 기법이 cold-start 문제에 도움을 줄 수 있음
 - __Other Recommendation Algorithms__
    - Context-based Recommendation
        - Context-aware Recommendation System
        - Location-based Recommendation System
        - Real-time or Time-Sensitive Recommendation System
    - Community-based Recommendation
        - 사용자의 친구 또는 속한 커뮤니티의 선호도를 바탕으로 추천
        - SNS 등의 뉴스피드 또는 SNS 네트워크 데이터 등 활용
    - Knowledge-based Recommendation
        - 특정 도메인 지식을 바탕으로 아이템의 features를 활용한 추천
        - Case-based Recommendation
            - 사용자의 니트와 해결책 중 가장 적합한 것을 골라서 추천
        - Constraint-based Recommendation
            - 사용자에게 추천할 때, 정해진 규칙을 바탕으로 추천

<br/>

### 추천시스템 한계

 - Scalability
    - 실제 서비스 상황은 다양한 종류의 데이터
    - 학습 또는 분석에 사용한 데이터와는 전혀 다른 실전 데이터
 - Proactive Recommender System
    - 특별한 요청이 없어도 사전에 먼저 제공하는 추천서비스
    - 모바일, 인터넷 등 어디서는 유저에게 끊임없이 좋은 정보를 추천할 수 있는 서비스
 - Cold-Start Problem
    - 추천서비스를 위한 데이터 부족
    - 기본적인 성능을 보장하는  협업필터링 모델 구축이 쉽지 않은 것이 일반적
    - 컨텐츠 기반 또는 지식 기반의 방법 역시 서비스로 적용하기 어려움
 - Privacy preserving Recommender System
    - 개인정보 등 유저 정보가 가장 중요하지만, 직접적으로 사용하기 어려움
 - Mobile devices and Usage Contexts
    - 개별 상황 또는 환경 등에 따라 다른 컨텍스트를 사용
 - Long-term and Short-term user preference
    - 개인 또는 그룹의 단기/장기 관심사항
    - 추천받고 싶은 아이템이 현재 또는 과거 중 어느 시기와 관련 있는지 파악하기 어려움
 - Generic User models and Cross Domain Recommender System
    - 하나의 모델을 여러가지 데이터에 적용하기 어려움
    - 비슷한 도메인의 데이터를 활용해도 동일한 성능의 추천시스템을 기대하기 어려움
 - Starvation and Diversity
    - Starvation: 필요한 컴퓨터 자원을 끊임없이 가져오지 못하는 상황
    - 유저/아이템이 다양하고, 모든 유저/아이템에 더 많은 관심을 부여해야 함
