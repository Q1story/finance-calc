# 단숨 (Dansum) — 프로젝트 연동서

일상 생활 도구 모음 정적 사이트. 구 이름 "금융계산소" → 리브랜딩으로 **단숨 / DANSUM** (뜻: 단숨에, 순식간에).
배포: Vercel 자동배포 (main 푸시 시) — https://finance-calc-q22.vercel.app
저장소: https://github.com/Q1story/finance-calc (브랜치 `main`)

## 작업 규칙 (반드시 지킬 것)

1. **작업 시작 전 `git pull`, 끝나면 `git add` / `commit` / `push`.** 맥·윈도우 두 컴퓨터에서 같은 저장소를 작업함.
2. **빌드 도구 금지** (webpack, vite 등). 순수 HTML/CSS/JS 유지. `npm install` 불필요.
3. 외부 라이브러리는 **CDN 방식으로만**.
4. 새 페이지는 기존 디자인 톤 재사용: 짙은 녹색(`#0f4d3a`) 급여명세서 느낌, Noto Sans KR / Noto Serif KR, 동일한 CSS 변수.
5. 커밋 메시지는 한국어, 끝에 `Co-Authored-By` 트레일러 추가.

## 파일 구조 (전부 루트에 평면 배치)

| 파일 | 역할 |
|---|---|
| `index.html` | 카테고리 허브 홈 (5개 카드) |
| `finance.html` | 연봉 실수령액 / 퇴직금 / 대출 상환 / 예금·적금 (탭 4개) |
| `date.html` | D-Day / 날짜 계산 / 두 날짜 사이 / 나이 계산 |
| `text.html` | 글자수 세기(실시간) / 텍스트 변환 |
| `unit.html` | 길이 / 무게 / 온도 / 부피 변환 |
| `life.html` | BMI / 기초대사량·칼로리 / 알바 급여(주휴수당) |
| `about.html` `contact.html` `privacy-policy.html` `terms.html` | 소개·문의·법적 고지 |

## 코드 규칙 (기존 관례)

- **페이지마다 CSS·JS를 인라인으로 중복 보유** (공유 파일 없음). 공통 수정(헤더/푸터/CSS 변수)은 **전 페이지에 동일 적용**해야 함.
- 도구 페이지 구조: `header`(로고 + 드롭다운 네비) → `nav.tabs`(탭) → `main` 안에 `section.panel`(탭별) → `footer` → 하단 `<script>`.
- 탭 전환: `.tab-btn[data-tab="x"]` ↔ `#panel-x`. 선택 버튼 그룹은 `.seg` + `aria-pressed`.
- 결과 카드는 `.slip`(명세서형) 시그니처 컴포넌트. 광고 자리는 `<div class="ad-slot">AD</div>`.
- 헤더 드롭다운은 `<details class="nav-drop">` (JS 없음). 현재 페이지의 링크에 `aria-current="page"`.
- FAQ는 `details.faq`.
- 날짜는 `new Date(y, m-1, d)`로 파싱 (UTC 파싱 금지, 타임존 오류 방지).
- 파비콘은 인라인 SVG data URI(번개 아이콘, 금색 `#b98a2e` on 녹색).
- 연봉 요율은 `finance.html` 스크립트 상단 `RATES` 객체 (매년 갱신, 국민연금 상한액은 7월 변경 확인 필요).

## 새 도구/카테고리 추가 시 체크리스트

1. 기존 도구 페이지(예: `unit.html`)를 복사해 시작
2. 허브 `index.html`에 카드 추가
3. **모든 페이지**의 드롭다운 메뉴에 링크 추가 (10개 파일)
4. `index.html` 푸터 카테고리 링크, `about.html` 도구 그리드 갱신
5. 로컬 확인: `python3 -m http.server 8000` → http://localhost:8000

## 미완료 / 보류 항목

- **`robots.txt`, `sitemap.xml` 미작성** — 운영 도메인 확정 후 작성 (URL을 추측해서 넣지 말고 사용자에게 확인). 루트 URL 내용이 바뀌었으므로 sitemap에 `finance.html` 등 반영.
- **문의 이메일 공란** — `contact.html`의 `mailto:` 가 비어 있음. 실제 주소 필요.
- **AdSense** — 스크립트/사이트 인증 코드 미삽입. `.ad-slot` div 위치가 광고 자리.
- 추가 후보 카테고리: 생활 요금(전기요금 등), 이모지/특수문자 도구 등.
- 모바일에서는 헤더 네비를 축소 표시 (숨기지 않음).
