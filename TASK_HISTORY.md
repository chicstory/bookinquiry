# 📖 BookInquiry Task History

## [2026-09-27] 구글 로그인 잠금 전면 해제 및 Buy Me a Coffee 후원 연동
- **1. 요청사항**: 
  - 미완성인 구글 OAuth 게이트를 풀고 모든 독자가 자유롭게 4대 질문과 서재를 이용할 수 있도록 전면 개방
  - 애드센스 대신 서비스 철학에 부합하는 Buy Me a Coffee(`thepathlab`) 후원 위젯/버튼 연동
  - About 페이지에 "불편하거나 필요하면 만들어서 공개한다"는 1인 빌더 철학 영문 반영
- **2. 솔루션 & 구현**:
  - [app.js](file:///c:/Users/chics/OneDrive/문서/gemini/bookinquiry/js/app.js) & [components.css](file:///c:/Users/chics/OneDrive/문서/gemini/bookinquiry/css/components.css): `library-locked`, `prompt-locked`, 게이트 오버레이 전면 제거하여 게이트 프리(Zero-gate) 개방
  - [index.html](file:///c:/Users/chics/OneDrive/문서/gemini/bookinquiry/index.html): 헤더 네비게이션에 앙증맞은 `☕ Coffee` 버튼 추가, 구글 버튼을 "Sync Drive (선택적 클라우드 백업)"로 리프레이밍, 글로벌 푸터에 클린한 커피 후원 배너 탑재
  - [app.js](file:///c:/Users/chics/OneDrive/문서/gemini/bookinquiry/js/app.js): 완독(Finish & Mint) 축하 시 자발적 커피 후원 안내 연동
  - [about.html](file:///c:/Users/chics/OneDrive/문서/gemini/bookinquiry/about.html): 1인 독립 빌더 철학("Built When Needed, Shared Openly") 및 커피 후원 위젯 추가
- **3. 결과 & 검증**:
  - 커밋 `a9f15e2`, `4b97ef9`, `694d85a`, `366bc1c`, `8d4c90d`:
    - 모바일 360px 헤더 버튼 슬림화로 우측 잘림 해결
    - 모바일 미디어 쿼리 내 `.user-profile-badge`의 `display: inline-flex !important;` 충돌 버그 수정 (로그아웃/미연결 상태에서 배지가 강제 노출되던 현상 완벽 해결)
    - **[긴급 보안] 클라이언트 `app.js` 내 하드코딩된 Gemini API 키 전면 영구 박멸, `.gitignore` 신규 구축, 서버리스 엣지 워커 및 사용자 로컬스토리지 전용 격리 아키텍처로 안전 전환**
    - Cloudflare Worker 엔드포인트 `/api/sparks` 및 응답 파싱 완벽 매핑
  - GitHub Pages(`bookinquiry.com`) 즉시 배포 완료
- **4. 주요 합의 사항**:
  - 광고 배너 없는 순수 미니멀 독서 성소(Reading Sanctuary) 톤앤매너 유지
  - 구글 연동은 필수가 아닌 선택적 드라이브 백업 기능으로 위치 유지
  - 모바일 360px 뷰포트에서 헤더 모든 버튼(탐색, 서재, 커피, 구글싱크) 1줄 노출 표준 준수
  - 클라이언트 소스코드에 어떠한 API 비밀 키도 하드코딩 금지 (보안 절대 수칙 준수)
