# 🚀 GitHub 배포 가이드

세차장 허가 자동 체크 서비스를 GitHub에서 배포하는 방법입니다.

---

## 1️⃣ GitHub 리포지토리 생성

### 웹에서 생성
1. https://github.com/new 접속
2. **Repository name**: `carwash-permit`
3. **Description**: `세차장 허가 자동 체크 서비스`
4. **Public** 선택 (공개 서비스)
5. **README.md** 체크 해제 (이미 있음)
6. **Create repository** 클릭

### 또는 GitHub CLI 사용
```bash
gh repo create carwash-permit \
  --public \
  --source=. \
  --remote=origin \
  --push \
  --description="세차장 허가 자동 체크 서비스"
```

---

## 2️⃣ 로컬 저장소 GitHub에 연결

```bash
# 프로젝트 디렉토리로 이동
cd /home/kimjin/kim/Desktop/kim/01_Active_Projects/carwash-permit

# GitHub 원격 추가
git remote add github https://github.com/[username]/carwash-permit.git

# 또는 SSH 사용 (권장)
git remote add github git@github.com:[username]/carwash-permit.git

# 확인
git remote -v
# github  https://github.com/[username]/carwash-permit.git (fetch)
# github  https://github.com/[username]/carwash-permit.git (push)
```

---

## 3️⃣ GitHub에 푸시

```bash
# main 브랜치로 변경
git branch -M main

# GitHub에 푸시
git push -u github main

# 또는 대시보드에서
git push --all github  # 모든 브랜치 푸시
git push --tags github # 모든 태그 푸시
```

---

## 4️⃣ GitHub Secrets 설정

### 리포지토리 Secrets 생성

1. **Settings > Secrets and variables > Actions**
2. **New repository secret** 클릭
3. 다음 secrets 추가:

| Name | Value | 설명 |
|------|-------|------|
| `ADMIN_PASSWORD` | `carwash2024` | 관리자 패스워드 |
| `VWORLD_KEY` | `D8C6FAA0-D909-3BA4-8E7D-F17178F57932` | VWorld API 키 |
| `JUSO_KEY` | `<행안부_API_키>` | 주소 API 키 (선택) |
| `DATA_API_KEY` | `<국토부_API_키>` | 건축물 API 키 (선택) |
| `DEPLOY_HOST` | `carwash.dclub.kr` | 배포 호스트 (선택) |
| `DEPLOY_USER` | `deploy` | 배포 사용자 (선택) |
| `DEPLOY_KEY` | `<SSH_프라이빗_키>` | 배포 SSH 키 (선택) |
| `SLACK_WEBHOOK_URL` | `<Slack_Webhook_URL>` | Slack 알림 (선택) |

### GitHub CLI로 설정
```bash
gh secret set ADMIN_PASSWORD --body "carwash2024"
gh secret set VWORLD_KEY --body "D8C6FAA0-D909-3BA4-8E7D-F17178F57932"
```

---

## 5️⃣ CI/CD 워크플로우 확인

### 자동 생성된 워크플로우

`.github/workflows/` 디렉토리:
- `test.yml` - 테스트 및 품질 검사
- `deploy.yml` - 프로덕션 배포

### 워크플로우 실행 확인

1. **GitHub 리포지토리 > Actions 탭**
2. 워크플로우 선택 (Test & Quality / Deploy to Production)
3. 실행 상태 확인

### 로컬에서 워크플로우 테스트
```bash
# act 설치 (필요 시)
brew install act  # macOS
# 또는
choco install act  # Windows

# 워크플로우 테스트 실행
act push  # test.yml 실행
act -W .github/workflows/deploy.yml push  # deploy.yml 실행
```

---

## 6️⃣ 자동 테스트 실행

### PR(Pull Request) 작업 흐름

```bash
# 1. 개발 브랜치 생성
git checkout -b feature/new-feature

# 2. 코드 수정 및 커밋
git add .
git commit -m "✨ 새 기능 추가"

# 3. GitHub에 푸시
git push -u github feature/new-feature

# 4. GitHub에서 PR 생성
# → Actions가 자동으로 테스트 실행
# → 통과 시 Merge 가능

# 5. main에 Merge
# → deploy.yml이 자동으로 프로덕션 배포
```

### 테스트 상태 확인

```bash
# GitHub CLI로 확인
gh run list --workflow test.yml

# 또는 웹 대시보드
# https://github.com/[username]/carwash-permit/actions
```

---

## 7️⃣ Release 생성 (버전 관리)

### 수동으로 Release 생성

```bash
# 1. 버전 태그 생성
git tag -a v1.0.0 -m "Initial release: 74/74 tests passing"

# 2. GitHub에 푸시
git push github v1.0.0

# 3. GitHub에서 Release 생성
# → https://github.com/[username]/carwash-permit/releases
# → Draft a new release
# → Tag: v1.0.0 선택
# → Release title, description 작성
# → Publish release
```

### 또는 GitHub CLI 사용
```bash
gh release create v1.0.0 \
  --title "Initial Release" \
  --notes "74/74 tests passing, 32.17% coverage"
```

### npm 버전 동기화
```bash
# npm 버전 업데이트 (자동으로 git 태그 생성)
npm version patch   # v1.0.1
npm version minor   # v1.1.0
npm version major   # v2.0.0

# 푸시
git push github main
git push github --tags
```

---

## 🔄 배포 프로세스

### 자동 배포 흐름

```
개발자가 main에 푸시
         ↓
GitHub Actions 시작
         ↓
✅ test.yml 실행
   - npm test (74/74 통과)
   - npm run test:coverage
   - codecov 업로드
         ↓
✅ deploy.yml 실행 (성공 시)
   - SSH로 배포 서버 접속
   - npm install --production
   - .env 설정
   - npm test 재실행
   - pm2 restart
         ↓
✅ Slack 알림 전송
   - 배포 완료 메시지
   - 커밋 정보 포함
         ↓
🎉 배포 완료!
   https://carwash.dclub.kr
```

### 수동 배포 (선택)

```bash
# SSH로 서버 접속
ssh deploy@carwash.dclub.kr

# 프로젝트 디렉토리로 이동
cd /var/www/carwash-permit

# 최신 코드 받기
git pull origin main

# 의존성 설치
npm install --production

# 환경 변수 설정 (.env 파일)
# - ADMIN_PASSWORD
# - NODE_ENV=production

# 테스트 실행
npm test

# 서비스 재시작
pm2 restart carwash-permit

# 상태 확인
pm2 status
curl http://localhost:40090/api/shop/categories
```

---

## 📊 모니터링

### GitHub Actions 로그 확인

```bash
# 웹 대시보드
https://github.com/[username]/carwash-permit/actions

# CLI로 확인
gh run view <run-id>
gh run log <run-id>

# 실패 시 디버깅
gh run logs --failed <run-id>
```

### 배포 상태 확인

```bash
# 라이브 URL 테스트
curl -I https://carwash.dclub.kr
curl https://carwash.dclub.kr/api/shop/categories | jq .

# 관리자 페이지
curl -I https://carwash.dclub.kr/admin
```

### Slack 알림

배포 완료/실패 시 Slack 채널에 자동 알림:
- ✅ 배포 성공: 초록 메시지
- ❌ 배포 실패: 빨간 메시지
- 커밋 정보 포함

---

## 🔐 보안 주의사항

### .env 파일 보안

```bash
# ❌ 절대 금지
git add .env  # .env 파일 커밋 금지

# ✅ 올바른 방법
echo ".env" >> .gitignore
git add .gitignore
git commit -m "chore: .env를 .gitignore에 추가"
```

### Secrets 관리

```bash
# ❌ 코드에 하드코딩 금지
const PASSWORD = "carwash2024"  // 위험!

# ✅ 환경 변수 사용
const PASSWORD = process.env.ADMIN_PASSWORD  // 안전!
```

### Deploy Key 설정 (선택)

배포 서버 SSH 접속용:

```bash
# 1. SSH 키 생성 (배포 서버에서)
ssh-keygen -t ed25519 -f deploy_key -N ""

# 2. GitHub에 공개키 등록
# Settings > Deploy keys > Add deploy key
cat deploy_key.pub

# 3. GitHub Secrets에 개인키 등록
# Settings > Secrets > New secret: DEPLOY_KEY
cat deploy_key  # 이 내용을 복사
```

---

## 📝 커밋 메시지 규칙

### 권장 형식

```
<타입>: <제목>

<본문>

<꼬리말>
```

### 타입

- ✨ `feat`: 새 기능
- 🐛 `fix`: 버그 수정
- 📚 `docs`: 문서 변경
- 🎨 `style`: 코드 스타일 변경
- ♻️ `refactor`: 코드 재구성
- ⚡ `perf`: 성능 개선
- ✅ `test`: 테스트 추가
- 🔧 `chore`: 빌드/도구 변경

### 예시

```bash
git commit -m "✨ feat: GitHub Actions CI/CD 파이프라인 추가

- test.yml: 유닛 테스트 및 커버리지 검사
- deploy.yml: 프로덕션 배포 자동화
- .env.example: 환경 변수 템플릿 추가

Closes #123"
```

---

## 🚀 최종 확인 체크리스트

- [ ] GitHub 리포지토리 생성
- [ ] 로컬 저장소 GitHub 연결
- [ ] main 브랜치 첫 푸시
- [ ] GitHub Secrets 설정
- [ ] Actions 탭에서 워크플로우 실행 확인
- [ ] 테스트 통과 확인
- [ ] 배포 로그 확인
- [ ] 라이브 URL 접속 확인
- [ ] 관리자 페이지 로그인 테스트
- [ ] README.md 최신화

---

## 📞 문제 해결

### 배포 실패

```bash
# 1. 워크플로우 로그 확인
gh run view <run-id> --log

# 2. SSH 키 권한 확인
chmod 600 ~/.ssh/deploy_key

# 3. 배포 서버 접속 테스트
ssh -i deploy_key deploy@carwash.dclub.kr

# 4. 배포 서버 로그 확인
pm2 logs carwash-permit
```

### 테스트 실패

```bash
# 1. 로컬에서 테스트 실행
npm test

# 2. 전체 테스트 실행
npm test -- --verbose

# 3. 특정 테스트만 실행
npm test -- shopRoutes.test.js

# 4. 커버리지 확인
npm run test:coverage
```

### GitHub API 제한

```bash
# GitHub CLI 인증 확인
gh auth status

# 새로 인증
gh auth login
```

---

## 📖 추가 자료

- [GitHub Actions 문서](https://docs.github.com/actions)
- [Semantic Versioning](https://semver.org/lang/ko/)
- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [GitHub Security](https://docs.github.com/security)

---

**🎉 GitHub 배포 설정이 완료되었습니다!**

이제 코드를 푸시하면 자동으로 테스트되고 배포됩니다.
