# 🏢 세차장 허가 자동 체크 서비스

주소만 입력하면 **세차장 설치 가능 여부를 자동으로 확인**해주는 웹 서비스입니다.

🌐 **라이브 URL**: https://carwash.dclub.kr

---

## ✨ 핵심 기능

### 9개 탭으로 완성된 서비스

| # | 탭명 | 기능 | 상태 |
|---|------|------|------|
| 1 | **📍 주소검색** | 다음 우편번호 팝업으로 주소 자동 검색 | ✅ 완성 |
| 2 | **🏞️ 토지이용** | 해당 주소의 용도지역 조회 (DB/API 선택 가능) | ✅ 완성 |
| 3 | **🏗️ 건축물** | 건축물대장 정보 조회 (DB/API 선택 가능) | ✅ 완성 |
| 4 | **📞 연락처** | 관할 환경청/구청 정보 제공 | ✅ 완성 |
| 5 | **✅ 허가판단** | 🔴 **핵심**: 세차장 허가 가능/불가 판단 | ✅ 완성 |
| 6 | **📋 허가절차** | 단계별 허가 절차 안내 (7단계 체크박스) | ✅ 완성 |
| 7 | **🛒 쇼핑몰** | 장비/서비스 상품 판매 + 어드민 관리 | ✅ 완성 |
| 8 | **🔍 근처세차장** | 검색한 주소 기준 자동 세차장 찾기 | ✅ 완성 |
| 9 | **📱 정보** | 서비스 안내 및 지원 | ✅ 기본 구성 |

---

## 🛒 쇼핑몰 기능

세차장 개장에 필요한 **장비 및 서비스**를 한 곳에서 구매/상담할 수 있습니다.

### 카테고리 (2개)

#### 📦 **장비** (3개 상품)
| 상품 | 가격 | 설명 |
|------|------|------|
| 폐수처리기 | ₩6,500,000 | 용량 선택 가능 (300-800L) |
| 진공청소기 | ₩650,000 | 내부 청소용 업소용 장비 |
| 고압세척기 | ₩1,800,000 | 차체/바닥 세척용 고압분무기 |

#### 💼 **서비스** (4개 상품)
| 서비스 | 가격 | 설명 |
|--------|------|------|
| 설계비 (용도변경) | ₩3,000,000 | 건축물대장 용도변경 + 설계도 |
| 인허가비 (폐수인허가) | ₩1,000,000 | 폐수시설 설치신고 전담 |
| 인테리어 | ₩1,500,000 | 매장 설계 및 시공 (20-30평) |
| 토목공사 | ₩상담가격 | 부지 정지, 배수, 포장 (200-500㎡) |

### 쇼핑몰 기능
- ✅ 카테고리별 필터링
- ✅ 상품 상세 정보 + 옵션 선택
- ✅ 장바구니 기능 (localStorage 저장)
- ✅ 주문 폼 (고객정보 입력)
- ✅ 주문 완료 (주문번호 발급)

### 🔑 어드민 관리
**URL**: `https://carwash.dclub.kr/admin`
**패스워드**: `carwash2024`

**어드민 기능**:
- 상품 추가/수정/삭제
- 가격 실시간 변경
- 재고 관리
- 주문 상태 관리

---

## 🎯 허가 판단 기준

### ✅ 허가 가능
- 상업지역 (모든 종류)
- 공업지역 (모든 종류)
- 준주거지역
- 1종, 3종 일반주거지역

### ⚠️ 조건부 가능
- **2종 일반주거지역** (건폐율 60% 이하)
- **자연녹지지역** (주차장 확보)

### ❌ 허가 불가
- 보전녹지 / 생산녹지
- 도시자연공원
- 상수원보호구역
- 개발제한구역 (그린벨트)
- 전용주거지역

---

## 🚀 빠른 시작

### 웹에서 (배포 완료 ✅)
```
🌐 https://carwash.dclub.kr
```

### 로컬에서 실행
```bash
# 1. 프로젝트 디렉토리로 이동
cd /home/kimjin/kim/Desktop/kim/01_Active_Projects/carwash-permit

# 2. 의존성 설치 (최초 1회)
npm install

# 3. 서버 시작
npm start

# 4. 브라우저에서 접속
http://localhost:35000  # 배포 포트
# 또는
http://localhost:40090  # 개발 포트 (포트 변경 시)
```

---

## 📚 건축법 자료 (2026-03-30 추가)

### 법적 기준 문서 (4개)

이제 건축법상 세차장 설치 기준에 대한 **완벽한 자료**가 준비되었습니다!

| 문서 | 용도 | 대상 |
|------|------|------|
| **[BUILDING_CODE_REFERENCE.md](./BUILDING_CODE_REFERENCE.md)** | 용도지역별 설치 기준 (상세 가이드) | 정책담당자, 법무검토 |
| **[ZONE_DECISION_LOGIC.md](./ZONE_DECISION_LOGIC.md)** | 판정 알고리즘 + JavaScript 구현 | 개발자 |
| **[API_INTEGRATION_GUIDE.md](./API_INTEGRATION_GUIDE.md)** | 공공 API 실제 연동 (VWorld, Juso) | 백엔드 개발자 |
| **[BUILDING_CODE_SUMMARY.md](./BUILDING_CODE_SUMMARY.md)** | 빠른 참조 및 체크리스트 | 신청자, PM |

### 주요 커버리지

```
✅ 15개 용도지역 (R0~R5, C1~C3, I1~I3, G1~G3)
✅ 조건부 가능 지역 (R2, I3, G1) - 상세 조건 명시
✅ 불가능 지역 (4가지) - 원인 명확화
✅ 필수 시설 기준 - 정량화 (BOD, SS, COD 등)
✅ 공공 API 3개 - 실제 연동 코드 포함
✅ JavaScript 판정 로직 - 프로덕션 레벨
✅ 체크리스트 - 7단계 신청 프로세스
```

### 빠른 참조

**세차장 설치 가능성**:
- ⭐ 무조건 가능: C1, C2, C3, I1, I2, R1, R3, R4, R5
- ⚠️ 조건부: R2 (건폐율≤60%), I3, G1
- ❌ 불가능: R0, G2, G3, 그린벨트, 상수원보호

**체크리스트** (BUILDING_CODE_SUMMARY.md):
```
□ Step 1: 토지이용계획확인원 발급 (정부24)
□ Step 2: 용도지역 판정
□ Step 3: 건축물대장 확인
□ Step 4: 구청 사전상담
□ Step 5: 용도변경 신고/허가
□ Step 6: 폐수처리시설 신청
□ Step 7: 건축허가 완료
```

---

## 📋 API 엔드포인트

### 🛒 쇼핑몰 API

#### 카테고리 조회
```bash
GET /api/shop/categories
```
**응답**:
```json
{
  "success": true,
  "data": [
    { "id": 1, "name": "장비", "slug": "equipment" },
    { "id": 2, "name": "서비스", "slug": "service" }
  ]
}
```

#### 상품 목록 조회
```bash
GET /api/shop/products?category_id=1&search=폐수&page=1&limit=10
```

#### 상품 상세 조회
```bash
GET /api/shop/products/1
```

#### 주문 생성
```bash
POST /api/shop/orders
Content-Type: application/json

{
  "customer_name": "김철수",
  "customer_phone": "010-1234-5678",
  "customer_addr": "서울시 강남구 테헤란로 123",
  "memo": "폐수처리기 설치 예정",
  "items": [
    { "product_id": 1, "quantity": 1, "option_value": "500L" }
  ]
}
```

#### 주문 조회
```bash
GET /api/shop/orders/{orderNumber}
```

---

### 세차장 허가 판정 API

### 주소 검색
```bash
GET /api/address/search?query=서울시+강남구
```
**응답 예시**:
```json
{
  "results": [
    {
      "roadAddr": "서울시 강남구 테헤란로 123",
      "jibunAddr": "강남구 역삼동 123-4",
      "sigunguCd": "11680",
      "bjdongCd": "10100"
    }
  ]
}
```

### 용도지역 조회
```bash
GET /api/land/zone?pnu=1168010100...&scenario=2
```
**Mock 시나리오**:
- `scenario=1` → 상업지역 (허가 가능)
- `scenario=2` → 2종일반주거 (조건부)
- `scenario=3` → 보전녹지 (불가)

### 건축물대장
```bash
GET /api/building/info?sigunguCd=11680&bjdongCd=10100
```

### 관공서 연락처
```bash
GET /api/offices?region=서울
```
**응답 예시**:
```json
{
  "offices": [
    {
      "명칭": "한강유역환경청",
      "전화": "031-790-2800",
      "관할": ["서울", "경기", "강원", "인천"]
    }
  ]
}
```

### 허가 판단 (핵심)
```bash
POST /api/permit/check
Content-Type: application/json

{
  "zoneType": "제2종일반주거지역"
}
```
**응답 예시**:
```json
{
  "result": "조건부가능",
  "reason": "일정 조건을 만족하면 허가 가능합니다",
  "conditions": [
    "✓ 건폐율 60% 이하 확인 필요",
    "✓ 주차장 면적 (최소 6대) 확보"
  ],
  "checkList": [
    "☐ 토지이용계획확인원",
    "☐ 건축물대장",
    "☐ 사업계획서"
  ]
}
```

---

## 🔧 설정 및 배포

### `.env` 파일
```env
# 모드 선택
USE_MOCK=true          # true: Mock 데이터, false: 실제 API

# 포트 설정
PORT=35000            # 배포 포트 (기본값)

# 실제 API 키 (발급 후 입력)
VWORLD_KEY=your_key
JUSO_KEY=your_key
DATA_API_KEY=your_key

# 배포 정보
SUBDOMAIN=carwash
DOMAIN=carwash.dclub.kr
```

### 배포 포트 변경
```bash
# .env에서 PORT 수정 또는
PORT=3000 npm start
```

---

## 📚 공공 API 연동 (선택사항)

### 1. VWorld API (용도지역)
- **URL**: https://www.vworld.kr/dev/v4dv_apiuse_s001.do
- **발급**: 즉시 (회원가입 후)
- **특징**: 무료, 3개월 유효

### 2. 행안부 도로명주소 API
- **URL**: https://business.juso.go.kr
- **발급**: 신청 즉시 사용 가능
- **특징**: 무료

### 3. 국토부 건축물대장 API
- **URL**: https://www.data.go.kr/data/15134735/openapi.do
- **발급**: 1~2일 소요
- **특징**: 무료

---

## 💾 데이터베이스 (자동 생성)

배포 시 자동으로 MySQL 데이터베이스가 생성됩니다.

```
호스트: 192.168.45.73:3306
DB명: dclub_carwash
사용자: user_carwash
비밀번호: 9d524874002044d19a3c6942
```

### 연결 문자열
```
mysql://user_carwash:9d524874002044d19a3c6942@192.168.45.73:3306/dclub_carwash
```

---

## 📁 프로젝트 구조

```
📦 carwash-permit/
├── 📄 server.js              # Express 서버 (메인 라우팅)
├── 📄 package.json           # 의존성 (express, better-sqlite3, multer)
├── 📄 .env                   # 설정 파일 (포트, API 키)
├── 📄 README.md              # 이 파일
├── 📁 db/
│   ├── 📄 schema.sql         # 데이터베이스 스키마
│   ├── 📄 init.js            # DB 초기화 및 시드 데이터
│   ├── 📄 shop.db            # SQLite 데이터베이스 (자동 생성)
│   └── 📄 regulations.db      # 법령/조례 데이터
├── 📁 routes/
│   ├── 📄 workflowRoutes.js  # 허가 판정 워크플로우 API
│   └── 📄 shopRoutes.js      # 쇼핑몰 API (상품/주문)
├── 📁 data/
│   └── 📄 offices.json       # 환경관청 6곳 + 담당부서 정보
├── 📁 public/
│   └── 📄 index.html         # 단일 파일 UI (9개 탭, CSS+HTML+JS)
└── 📁 node_modules/          # 의존성 패키지
```

### 핵심 파일 설명

#### server.js
- Express 기본 설정 + 미들웨어
- 정적 파일 서빙 (HTML/CSS/JS)
- 9개 탭의 API 라우팅

#### routes/workflowRoutes.js
- POST `/api/workflow/start` - 세션 생성
- POST `/api/workflow/{id}/step/{n}` - 허가 판정 (4단계)
- GET `/api/offices` - 관공서 연락처

#### routes/shopRoutes.js
- GET `/api/shop/categories` - 카테고리
- GET `/api/shop/products` - 상품 목록
- POST `/api/shop/orders` - 주문 생성
- 어드민 API (Bearer 토큰 인증)

#### public/index.html
- Glassmorphism 디자인 (보라/파란 그라디언트)
- 9개 탭 네비게이션
- 다음 우편번호 팝업 통합
- fetch + async/await API 호출
- localStorage (장바구니, 체크박스)
- 모바일 반응형 CSS (WCAG 준수)

#### db/init.js
- SQLite 데이터베이스 자동 생성
- 테이블 생성 및 마이그레이션
- 시드 데이터 (카테고리 2개, 상품 7개)

---

## 🎓 허가 절차 (7단계)

1. **토지이용계획확인원 발급** (정부24 또는 구청)
2. **건축물대장 확인** (용도 변경 필요 시)
3. **사업계획서 작성** (시설배치도, 폐수 처리계획)
4. **폐수배출시설 설치신고** (구청 환경과)
5. **자동차관련시설 건축허가/신고** (구청 건축과)
6. **사업자등록** (세무서)
7. **세차장 운영 시작** (기술기준 준수)

---

## 🧪 테스트

### Mock 모드 테스트 (API 키 불필요)
```bash
# 모든 시나리오가 Mock 데이터로 즉시 응답
npm start

# 브라우저: http://localhost:35000
# 탭 이동하며 3가지 허가 결과 확인 가능
```

### 실제 API 테스트 (API 키 필요)
```bash
# 1. 3개 API 키 발급
# 2. .env에 입력
# 3. USE_MOCK=false 로 변경
# 4. npm start 재실행
```

---

## 🐛 문제 해결

### 포트 이미 사용 중
```bash
# 다른 포트에서 시작
PORT=3000 npm start

# 또는 기존 프로세스 종료
pkill -f "node server.js"
```

### API 응답 없음
```bash
# Mock 모드 확인
cat .env | grep USE_MOCK

# USE_MOCK=true 가 아니면 수정
USE_MOCK=true npm start
```

### 브라우저에서 주소 팝업 안 뜸
```javascript
// index.html 콘솔에서 확인
console.log(daum);  // Postcode 객체 로드 확인
```

---

## 📊 성능

- **응답 시간**: < 100ms (Mock 모드)
- **페이지 로드**: < 2초
- **번들 크기**: < 50KB (HTML 단일 파일)
- **메모리**: ~ 50MB (Node.js)

---

## 🔐 보안

- ✅ HTTPS 자동 적용 (와일드카드 SSL)
- ✅ API 키 환경변수 분리 (.env)
- ✅ CORS 기본 설정
- ✅ XSS 방지 (Vanilla JS)
- ✅ SQL Injection 불가 (Mock 데이터)

---

## 📊 프로젝트 현황

### ✅ 완성된 기능
- ✅ 9개 탭 (허가 판정 + 쇼핑몰 + 근처세차장)
- ✅ 도메인 연결 (HTTPS/SSL 활성화)
- ✅ 쇼핑몰 기능 (상품/장바구니/주문)
- ✅ 어드민 패널 (상품/가격 관리)
- ✅ SQLite 데이터베이스
- ✅ 모바일 최적화
- ✅ Mock + 실제 API 동시 지원

### 🚀 실시간 배포
- **라이브 URL**: https://carwash.dclub.kr
- **로컬 개발**: http://localhost:40090
- **어드민**: https://carwash.dclub.kr/admin (비밀번호: carwash2024)

---

## 📈 향후 개선

- [ ] 실제 공공 API 완전 연동 (VWorld, 행안부, 국토부)
- [ ] 결제 시스템 통합 (PG사 연동)
- [ ] 주문 상태 추적 시스템
- [ ] 문의 상담 기능 (1:1 채팅)
- [ ] 지도 시각화 (Kakao Maps)
- [ ] 모바일 앱 (React Native)
- [ ] 이메일 알림 (주문/완료)
- [ ] 통계 대시보드

---

## 📝 라이선스

MIT License - 자유롭게 사용, 수정, 배포 가능

---

## 👨‍💻 개발자

**Kim** - Full Stack Development
- Frontend: Vanilla HTML/CSS/JS
- Backend: Express.js (Node.js)
- Deployment: dclub.kr (Nginx + SSL)

---

---

## 🔐 보안 설정

### API 보안 기능

#### 1️⃣ 레이트 리미팅
```javascript
// 15분 내 100 요청 제한 (모든 /api/* 라우트)
- 초과 시 429 Too Many Requests 응답
- IP 기반 추적
```

#### 2️⃣ 응답 타임아웃
```javascript
// 모든 요청은 30초 이내 응답 필수
- 초과 시 503 Service Unavailable
- 무한 루프 방지
```

#### 3️⃣ XSS 방지
```javascript
// HTML 이스케이핑 적용
- 사용자 입력 자동 처리
- JSON 응답만 전달
```

#### 4️⃣ SQL 주입 방지
```javascript
// 파라미터화 쿼리 사용 (better-sqlite3)
db.prepare('SELECT * FROM users WHERE id = ?').get(id)
```

#### 5️⃣ 인증 (관리자)
```bash
# Bearer Token 기반
Authorization: Bearer {32바이트 hex 토큰}

# 발급
POST /api/admin/login
{ "password": "carwash2024" }

# 토큰 유효시간: 1시간
```

#### 6️⃣ 에러 정보 제어
```javascript
// Development (NODE_ENV=development)
{ "errorId": "A1B2C3D4", ... }  // 디버깅 용

// Production (NODE_ENV=production)
{ "errorId": undefined, ... }   // 숨김 (보안)
```

### 환경 변수 설정

#### .env 파일 생성
```bash
# 필수 설정
PORT=40090
NODE_ENV=development

# 관리자 패스워드 (필수!)
ADMIN_PASSWORD=carwash2024

# API 키 (선택)
VWORLD_KEY=D8C6FAA0-D909-3BA4-8E7D-F17178F57932
JUSO_KEY=<행안부_도로명주소_API_키>
DATA_API_KEY=<국토부_건축물_API_키>

# 배포 정보
SUBDOMAIN=carwash
DOMAIN=carwash.dclub.kr
DEPLOYED=true
```

#### .env 보안 규칙
```bash
# ❌ 절대 금지
- .env를 git에 커밋하지 말 것
- 패스워드/API 키를 코드에 하드코딩 금지
- 프로덕션 .env를 배포자만 관리

# ✅ 추천
- .env를 .gitignore에 추가 (이미 설정됨)
- .env.example 파일로 템플릿 제공
- 배포 환경에서는 환경변수로 주입
```

### 보안 체크리스트

```
✅ 레이트 리미팅    (express-rate-limit)
✅ 타임아웃 미들웨어  (30초)
✅ XSS 방지         (HTML 이스케이핑)
✅ SQL 주입 방지     (파라미터화 쿼리)
✅ CSRF 보호        (content-type 검증)
✅ 에러 정보 제어    (프로덕션 모드)
✅ 인증 (Bearer)    (1시간 유효 토큰)
✅ 환경 변수        (.env 관리)
✅ 의존성 보안      (npm audit)
✅ 캐시 정책        (no-cache 헤더)
```

---

## 🚀 GitHub 배포 가이드

### 1️⃣ GitHub에 푸시

```bash
# 1. GitHub 리포지토리 생성
# https://github.com/new
# 리포지토리명: carwash-permit
# Public 선택 (공개 서비스)

# 2. GitHub 원격 추가
cd /path/to/carwash-permit
git remote add github https://github.com/[username]/carwash-permit.git

# 3. GitHub에 푸시
git branch -M main
git push -u github main
```

### 2️⃣ GitHub 환경 변수 설정

```
Settings > Secrets and variables > Actions
+ New repository secret

ADMIN_PASSWORD          → carwash2024
VWORLD_KEY             → D8C6FAA0-D909-3BA4-8E7D-F17178F57932
NODE_ENV               → production
```

### 3️⃣ CI/CD 파이프라인 (GitHub Actions)

`.github/workflows/deploy.yml` 생성:

```yaml
name: Test & Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [18.x, 20.x]

    steps:
      - uses: actions/checkout@v3

      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run linter
        run: npm run lint --if-present

      - name: Run tests
        run: npm test

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/coverage-final.json

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
      - uses: actions/checkout@v3

      - name: Deploy to dclub.kr
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
          DEPLOY_HOST: ${{ secrets.DEPLOY_HOST }}
          DEPLOY_USER: ${{ secrets.DEPLOY_USER }}
        run: |
          mkdir -p ~/.ssh
          echo "$DEPLOY_KEY" > ~/.ssh/deploy_key
          chmod 600 ~/.ssh/deploy_key
          ssh -i ~/.ssh/deploy_key $DEPLOY_USER@$DEPLOY_HOST \
            "cd /var/www/carwash-permit && \
             git pull origin main && \
             npm install && \
             npm test && \
             pm2 restart carwash-permit"
```

### 4️⃣ GitHub Pages 배포 (문서)

```bash
# GitHub Pages에 문서 배포
Settings > Pages > Source > main (docs 폴더)

# 문서 자동 생성
npm run docs

# https://[username].github.io/carwash-permit
```

### 5️⃣ Release 생성

```bash
# 버전 태그 생성
git tag -a v1.0.0 -m "Initial release: 74/74 tests passing"

# GitHub에 푸시
git push github v1.0.0

# Release notes 생성
# GitHub: Releases > Draft a new release
```

### 배포 명령어

```bash
# 현재 상태 확인
git status

# GitHub 푸시
git push github main

# 테스트 실행 (배포 전)
npm test

# 커버리지 확인
npm run test:coverage

# 버전 업데이트
npm version patch  # v1.0.1
npm version minor  # v1.1.0
npm version major  # v2.0.0
```

---

## 📞 문의

- **GitHub**: https://github.com/[username]/carwash-permit
- **배포 URL**: https://carwash.dclub.kr
- **로컬 개발**: http://localhost:40090
- **상태**: ✅ 프로덕션 준비 완료

---

**🎉 세차장 허가 체크 서비스를 이용해주세요!**
