# MOONG! 번개모임 SNS
- 사용자가 즉시 모임을 생성하고 참여할 수 있는 ‘벙개 만남 중심 플랫폼’
- 단순한 인스타그램 클론 코딩에서 벗어난, SNS 플랫폼 프로젝트 수행.
[프로젝트 발표자료](https://docs.google.com/presentation/d/13RiIDvLdFT1VZj0Q3EYMLUbsCBPHW3Pq-bJ6WHqiBQ8/edit?usp=sharing)

## 스크린샷 및 데모 실행 화면
### 메인화면
![메인화면](docs/images/main.PNG)

### 모임생성
![모임생성](docs/images/new_moim.gif)

### 모임마감
![모임마감](docs/images/moim_close.gif)

### 댓글
![댓글](docs/images/comment.gif)

### 마이페이지-또뭉(좋아요)
![마이페이지-또뭉(좋아요)](docs/images/mypage_ddomoong.gif)

-----

## 초기 실행 방법(필수)
회원가입 화면의 '활동 지역' 목록은 초기 데이터 적재 후 정상 노출됩니다.

### 1) 패키지 설치 or uv sync 수행(uv 사용 시)
- 1안 : 패키지 설치 pip install -r requirements.txt
- 2안 : uv sync(pyproject.toml 이용)

#### 1-1) 주요 설치 라이브러리 내용 기재 
1. django
2. openai : 게시글 작성 후 ai 해시테그 생성 시 사용
3. python-dotenv : apikey 별도 관리를 위해 추가(.env파일은 .gitignore에 포함)
4. apscheduler : django 스케줄러 사용을 위함.
    - 매일 00:05 만료된 모임 게시글을 scheduler.py ->  expire_posts.py 처리를 통해 완료 혹은 취소 처리를 수행. 
5. pillow : 이미지 표기 시 사용

#### 1-2) API KEY 입력하기 : .env파일 생성 후 api key 입력
- 클론 받은 경로에 .env 파일을 생성합니다 (moong dir 바로 아래)
- 파일 내용 설정 : 
- OPENAI_API_KEY="자신의 api key 입력"
- KAKAO_APP_KEY="자신의 카카오 map api key 입력"

##### KAKAO_APP_KEY 생성하여 얻어오기 (없다면..)
1. https://developers.kakao.com/console/app 접속
2. + 앱생성 이후 생성한 앱 클릭(추가 설정을 해주기 위해 앱 설정으로 진입)
3. 왼쪽 메뉴 앱 > 플랫폼 키 > JavaScript 키 > Default JS Key 키 클릭 > JavaScript SDK 도메인 설정 
- http://127.0.0.1:8000 추가 
    (python manage.py runserver했을 때 사용되는 url 기재)
    (특이사항 : 주의 localhost와 127.0.0.1 을 카카오에서 구별하기 때문에 유의 필요)
4. 왼쪽 메뉴 제품 설정 > 카카오맵 > 사용 설정 > 상태 off에서 on으로 변경

### 2) 마이그레이션
python manage.py migrate

### 3) 지역 데이터 적재 (생략 가능)
python manage.py import_locations 
runserver 시 자동으로 실행되어 생략 가능 (처리 내용 : apps.py)
- 실행 시마다 수행되지만, 이미 저장되어있는 경우에는 skip되므로 중복저장되지않음.

### 4) 관리자 계정 생성
python manage.py createsuperuser

### 5) 실행
python manage.py runserver

<br>

---

## 📌 프로젝트 개요

* **개발 기간**: 2026.01.19 ~ 2026.02.03
* **팀 구성**: 5명
<br>

| 이름 | 역할 |
|------|--------|
| [나솔림](https://github.com/solrimna) | ‘벙개’ 모임 모집글 작성 기능 |
| [이영진](https://github.com/ilove0628yj-w) | ‘벙개’ 모임 참여 관리 |
| [서호근](https://github.com/azure5finger-cmyk) | 회원 관리 기능 / 피드 하단 댓글 기능 |
| [유민지](https://github.com/kittyjoa) | 마이페이지 조회/수정 및 활동이력 생성 |
| [박지영](https://github.com/battlegroundcallofduty) | AI 해시태그 생성 및 검색 조회 기능 |

* [요구사항 명세서](https://docs.google.com/spreadsheets/d/12-bzeP10GFYD7vwEOQrfJbKsLZVSEEEZ/edit?usp=sharing&ouid=116721417601261265482&rtpof=true&sd=true)

---
 
## 🛠 기술 스택
 
| 분류 | 기술 |
| --- | --- |
| Language | Python |
| Framework | Django |
| 데이터베이스 | SQLite |
| 프론트엔드 | HTML, CSS, JavaScript |
| AI 연동 | OpenAI API |
| 지도 | Kakao Map API |
| 버전 관리 | GitHub |

<br>

---
 
## 🔸 주요 기능
 
* **회원 관리:** 회원 가입, 로그인, 로그아웃
* **개인 계정 로그인 및 피드 접근 (마이페이지):**
본인 또는 타 유저의 생성/참여/종료된 모임 목록 확인, 좋아요(또 뭉) 수 확인
* **‘벙개’ 모임 모집 피드 작성**
  ➖ 모집 피드 작성 / ai 기반 해시태그 생성
  ➖ 참여자 존재 여부에 따라 삭제 기능 제한
* **피드 하단 댓글 기능:**
댓글 작성 및 삭제, 모임장(작성자)의 댓글 공지 기능
* **검색 및 조회 기능:**
해시태그 기반 검색 / 지도 api 연동 위치 기반 모임 검색
* **‘벙개’ 모임 참여 관리:**
상세 페이지에서 버튼을 이용한 모임 참여 및 취소, 참여자 목록 조회, 대기 기능
<br>

---
 
## ▪️ 프로젝트 구조
 
```
Moong_pro/
├── config/               # Django 설정
├── moong/                # 메인 앱 (모임 게시글)
├── users/                # 유저 앱
├── locations/            # 지역 데이터
├── templates/            # HTML 템플릿
├── static/               # CSS, JS, 이미지
├── docs/images/          # README 첨부 파일들
├── manage.py
├── requirements.txt      # 의존성 목록
└── README.md
```
<br>

---
 
## 🔹 앞으로 추가할 내용 및 회고
 
* **배포 추가한다면:** 무료 서비스 중엔 `Railway`, 유료 서비스면 `AWS EC2 + Docker` 예정
* **배포 추가시 고려해야할 사항들:** `.env` 키들 환경변수로 따로 설정해야함, `DEBUG = FALSE` 변경, static 처리, SQLite보다 `PostgreSQL`이 나을것같음
* 번개모임만 특화된 플랫폼이 아직 많이 없기 때문에 차별화를 좀 더 하면 실제 서비스로 구현도 가능해보임. 번개모임 관련 서비스 이용자들이 어떤 것들이 필요할지 좀 더 시장조사를 해보고 서비스를 추가해보고 싶음. 상업화가 된다면 수익 구조나 유료 멤버십 구상까지
* 코드 가독성, 유지보수성, 효율성 높게 더 수정하고 싶다... 코드 리팩토링 예정!
<br>
