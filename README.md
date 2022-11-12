<div align=center>
    <h1>Zazinmori</h1>
</div>

>취업준비생 대상 자기소개서 분석 및 구직 관련 정보 제공 서비스
> 

Zazinmori는 자소서를 작성해보면서 겪었던 Pain point에서 아이디어를 얻어 개발했습니다. 취업준비생을 타겟으로 하여 합격 자기소개서 키워드 빈도 및 기업의 최신 토픽을 분석하고, 사용자에게 자기자소서 작성 관련 가이드 라인 및 구인 중인 기업 정보를 종합적으로 제공하여 취업을 종합적으로 지원하는 서비스입니다.


<div align=left>
    <br>
    <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white">
    <img src="https://img.shields.io/badge/Apache Hadoop-66CCEE?style=for-the-badge&logo=Apache Hadoop&logoColor=white">
    <img src="https://img.shields.io/badge/Apache Spark-E25A1C?style=for-the-badge&logo=Apache Spark&logoColor=white">
    <img src="https://img.shields.io/badge/Apache Airflow-017CEE?style=for-the-badge&logo=Apache Airflow&logoColor=white">
    <img src="https://img.shields.io/badge/Apache Kafka-231F20?style=for-the-badge&logo=Apache Kafka&logoColor=white">  
    <img src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=Elasticsearch&logoColor=white">
    <img src="https://img.shields.io/badge/Logstash-005571?style=for-the-badge&logo=Logstash&logoColor=white">
    <img src="https://img.shields.io/badge/Kibana-005571?style=for-the-badge&logo=Kibana&logoColor=white">
    <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white">
    <img src="https://img.shields.io/badge/Amazon EC2-FF9900?style=for-the-badge&logo=Amazon EC2&logoColor=white">
    <img src="https://img.shields.io/badge/django-092E20?style=for-the-badge&logo=django&logoColor=white">
    <img src="https://img.shields.io/badge/Fastapi-009688?style=for-the-badge&logo=Fastapi&logoColor=white">
    <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white">  
    <img src="https://img.shields.io/badge/NGINX-009639?style=for-the-badge&logo=NGINX&logoColor=white">     
    <img src="https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=Jenkins&logoColor=white">  
    <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=Git&logoColor=white">  
    <img src="https://img.shields.io/badge/Github-181717?style=for-the-badge&logo=Github&logoColor=white">  
</div>
<br>

프로젝트 기간 : 2022.08.18 ~ 2022.09.30

# 프로젝트 배경
- 취준생으로서 자소서를 쓰면서 가졌던 pain point들에서 아이디어 도출
  - 기업을 둘러 싼 최신 토픽들이 무엇인지 매번 찾아보기 힘듦
  - 일일이 합격자소서들을 찾아보는 것이 힘듦
  - 기업의 기본 정보들을 각 기업별로 찾아보는 것 힘듦
- 이러한 정보들을 제공해주는 서비스들이 있긴하지만, 하나에 특화되어있거나 부분적으로 제공하고있는 상황
- 이를 종합하여 하나의 서비스로 만들어 낸다면, 자소서를 작성하는 시간이 크게 절약될 뿐만아니라 자소서의 질도 향상될수 있다고 판단
- 따라서 하나의 웹서비스로 기업의 모든 정보를 찾아볼 수 있고 구직자들은 하나의 웹페이지에서 자소서를 작성하기만 되는 종합 자소서 플랫폼을 기획

# 주요 기능
- 기업별 세부 정보 검색 기능
- 채용공고 스크랩 및 자소서 작성 기능
- 기업별, 자소서 항목별 추천 키워드 제공 기능
- 사용자 활동 기반의 유저 맞춤형 기업 추천 기능
- 커뮤니티 및 기타 유저 편의 기능

# 아키텍쳐
![pjt3-arch](/images/pjt3-arch.png)

# 클러스터
![pjt3-cluster](/images/pjt3-cluster.png)

# 세부 구현 내용
자진모리는 확장성, 성능, 안정성이라는 세가지 요소에 초점을 맞추어 개발 했습니다.

## 확장성
>서비스 성장에 따른 서버 규모 확장 용이
>
- H-S Clustering : 하둡-스파크 클러스터를 구축하여 추후 서비스 성장 시 scale out 가능
- Nginx Upstream : Upstream으로 추가 WAS 지정하여 서버 확장 가능
- 로그 모니터링 : elasticsearch, kibana 등을 통해 로그 데이터 분석 환경 구축
- 용도에 따른 서버 구분 : 추후 서버 확장 시, 용도에 맞는 서버에서 기능 확장 시도 가능

## 성능
>구축한 데이터 파이프 라인에 대한 가동 속도 향상
>
- 멀티프로세싱 : Airflow에서 30만 건 이상의 데이터 크롤링 단시간 내 가능토록 멀티프로세싱을 통한 성능 향상
- Spark Cluster : yarn을 클러스터 매니저로 지정하여 리소스 관리, 각 executor에 2core씩 할당
- FastAPI : 메인 서비스 및 모델 서빙 역할에 따라 WAS 구분, FastAPI 이용하여 모델 서빙
- Logstash : Django에서 실시간으로 로그 확보 및 ES 적재

## 안정성
>서비스 규모, 트래픽 증가되는 경우에도 감당 가능토록 인프라 구축
>
- Hadoop Cluster : 3개 서버를 NameNode, SecondaryNamenode, DataNode로 활용
- Airflow : 지속적인 업데이트가 필요한 ETL [데이터 수집 -> 하둡 적재 -> 스파크 처리 -> MySQL 적재] 스케줄링하여 자동화
- NGINX : 정적인 파일에 대한 요청을 담당하여 서비스 중에 WAS에 대한 부하 절감 및 WAS 간 Load balancing
- 로그 수집 : 로그 데이터 유실 방지 위해 2개의 logstash를 각각 로그 수집기와 메세지 처리기로 구분, 그 사이에 중간 저장소로 kafka 사용

## 기타
- Jenkins-GitLab : 배포과정을 자동화하여 개발 속도 향상
- Cold Data의 MongoDB 적재 : 추후 분석을 위해 과거 로그 데이터 적재
- HTTPS : 서비스 보안 향상

# 활용 데이터

|  no  |       내용        |       출처        |    형식/방식     |
|:----:|:---------------:|:---------------:|:------------:|
|  1   |  금융위원회 기업기본정보   |     공공데이터포털     |   JSON/API   |
|  2   |  금융위원회 기업재무정보   |     공공데이터포털     |   JSON/API   |
|  3   |  금융위원회 지배구조정보   |     공공데이터포털     |   JSON/API   |
|  4   | 금융감독원 단일회사 주요계정 |    OPEN DART    |   XML/API    |
|  5   |   금융감독원 기업개황    |    OPEN DART    |   XML/API    |
|  6   |  금융감독원 기업고유번호   |    OPEN DART    |   XML/API    |
|  7   |   잡코리아 합격자소서    |      잡코리아       | CSV/CRAWLING |
|  8   |   인크루트 합격자소서    |      인크루트       | CSV/CRAWLING |
|  9   |   링커리어 합격자소서    |      링커리어       | CSV/CRAWLING |
|  10  |    독취사 합격자소서    |   독취사(네이버 카페)   | CSV/CRAWLING |
|  11  | 자소설 채용공고/자소서 항목 |       자소설       | CSV/CRAWLING |
|  12  | 빅카인즈 기업별 주요 뉴스  |      빅카인즈       | CSV/CRAWLING |

# ERD
![pjt3-erd](/images/pjt3-erd.png)

# 서비스 화면
- 메인 페이지
![pjt3-cluster](/images/main.png)

- 검색 페이지
![pjt3-search1](/images/search1.png)
![pjt3-search2](/images/search2.png)
![pjt3-search3](/images/search3.png)
![pjt3-search4](/images/search4.png)
![pjt3-search5](/images/search5.png)
![pjt3-search6](/images/search6.png)
![pjt3-search7](/images/search7.png)

- 자소서 작성 페이지
![pjt3-resume1](/images/resume1.png)
![pjt3-resume2](/images/resume2.png)
![pjt3-resume3](/images/resume3.png)

- 커뮤니티 페이지
![pjt3-comm1](/images/comm1.png)
![pjt3-comm2](/images/comm2.png)

- 마이 페이지
![pjt3-my](/images/my.png)
