# 📖 BookInquiry - Intentional 1:1 Reading Compass Engine

> **"Stop Summarizing, Start Questioning."**  
> (책 요약은 일주일이면 휘발됩니다. 책을 펼치기 전 4개의 날카로운 질문(Spark)을 장착하여 삶을 바꾸는 독서를 안내합니다.)  
> 🌐 **Official Live**: [https://bookinquiry.com](https://bookinquiry.com)

---

## 🕊️ 0. 서비스의 본질과 철학 (Core Philosophy)

> **"질문에 전부 답변하는 것이 목적이 아닙니다.**  
> **질문은 시험이나 숙제가 아니라, 독서 내내 독자의 뇌리에 가벼운 파동을 일으키는 지적 촉매제(The Spark)입니다."**

- **Zero-Gate Reading Sanctuary**: 불필요한 회원가입 강제나 광고 배너 없이, 누구나 책 제목을 검색해 즉시 4대 소크라테스 질문을 장착하고 독서를 시작할 수 있습니다.
- **Thought Timeline**: 책을 읽는 도중 형식에 구애받지 않고 스친 생각, 단편적인 메모를 '생각의 타임라인(Raw Reflections)'에 가볍게 기록합니다.
- **100% Private Ownership**: 중앙 데이터베이스가 없습니다. 독자의 모든 기록은 독자 본인의 브라우저 로컬 저장소(`localStorage`), 개인 **Google Drive**, 또는 **Obsidian 마크다운 볼트**에 안전하게 보존됩니다.

---

## 🧭 1. 4대 질문 프레임워크 (The 4 Catalytic Sparks)

BookInquiry는 책을 펼치기 전, 독자의 독서 의도(Compass Direction)와 도서 시놉시스를 결합하여 아래 4단계의 사색 촉매를 생성합니다:

| 단계 | 프롬프트 명칭 | 역할 및 기능 |
| :--- | :--- | :--- |
| **1. Spark** | The Spark | 첫 장을 넘기기 전, 고정관념을 흔드는 관점 전환 질문 |
| **2. Lens** | The Active Lens | 페이지를 넘기는 동안 능동적으로 관찰해야 할 핵심 긴장(Tension) |
| **3. Quest** | The Socratic Quest | 독자의 현실과 강하게 충돌하는 저자의 급진적 주장 또는 철학적 난제 |
| **4. Echo** | The Lifelong Echo | 책을 덮은 뒤에도 삶의 실행력과 내면적 자유를 이끄는 지속적 질문 |

---

## 📂 2. 스토리지 규격 (Obsidian & Google Drive Protocol)

사용자의 개인 저장소(Google Drive `drive.file` 및 Obsidian Vault)에는 아래의 미니멀한 마크다운 규격으로 1초 만에 복사 및 저장됩니다:

```markdown
---
title: "Zero to One"
author: "Peter Thiel"
year: 2026
status: "Reading" # Reading ➔ Completed
tags:
  - bookinquiry
  - business
  - philosophy
compass: "Work & Growth"
---

# Zero to One

### 💡 The Spark
> "남들은 모두 맞다고 고개를 끄덕이는데, 나 혼자 속으로 '아닌데?' 싶었던 사소한 신념 하나가 있나요?"

### 🔍 The Lens
> "경쟁을 당연시하는 사회적 통념과 저자가 주장하는 '창조적 독점' 사이의 긴장을 추적하세요."

### ⚔️ The Quest
> "저자는 '경쟁은 패배자들의 것이다'라고 단언합니다. 완독 후 당신은 여전히 공정한 경쟁이 사회를 발전시킨다고 믿을 수 있을까요?"

### 🌊 The Echo
> "당신의 비즈니스나 삶에서 남들이 복제할 수 없는 '0에서 1'을 만드는 단 하나의 영역은 어디인가요?"

---

## ✍️ My Reflections (생각의 타임라인)
- **14:20** (p.42) 경쟁하지 말고 독점하라는 말... 우리 팀 지금 다른 회사랑 단가 싸움하는 거 완전 바보짓이었네.
- **14:55** (p.88) "0에서 1로 가는 건 기술이고, 1에서 N으로 가는 건 세계화다." 이 문장 블로그 글감으로 꼭 쓰자.
```

---

## 🏛️ 3. 하이브리드 아키텍처 (Zero-Server + Edge Worker Proxy)

```text
[ End Reader (Client Web) ] (https://bookinquiry.com)
  ├─ 🌐 Zero-Server SPA (Vanilla JS + CSS, No Bundler, Pure Clean Light)
  ├─ 🔒 Private LocalStorage (기록 & 타임라인 완전 로컬 보관)
  └─ 📁 Optional Google Drive API (drive.file 스코프로 사용자 개인 드라이브 동기화)
       │
       ▼ (1) 도서 검색 및 소크라테스 4대 질문 생성 요청
[ Cloudflare Edge Worker Proxy ] (https://bookiry-worker.chicstory.workers.dev)
       │ (클라이언트 측 API 키 노출 0% 보장 / 환경변수 Secret 암호화 격리)
       ▼ (2) Gemini API 호출 (gemini-flash-latest)
[ Google Gemini AI Engine ]
       │ (책 시놉시스 + 독자의 무드/나침반 결합 ➔ 구조화된 JSON 질문 생성)
       ▼
[ 독서 중 : 타임라인 메모 누적 (Append-Only Event Log) ]
       │
       ▼ (3) 완독 버튼 클릭 ("Finish Book & Mint Resonance Card")
[ Obsidian 1-Click Vault Export & Google Drive 자동 백업 ]
```

---

## 📁 4. 프로젝트 구조

```text
bookinquiry/
├── README.md               # 서비스 기획 및 통합 아키텍처 정의서 (본 문서)
├── TASK_HISTORY.md         # 프로젝트 통합 개발 작업 히스토리 (누적 마스터)
├── CNAME                   # bookinquiry.com 커스텀 도메인 라우팅
├── index.html              # 메인 UI (나침반 토끼, 4대 질문, 서재, 생각 타임라인)
├── about.html              # 1인 빌더 철학("Built When Needed") 및 커피 후원 안내
├── contact.html            # 도서 제안 및 피드백 공식 창구
├── privacy.html            # 개인정보처리방침 (Zero Server Database 철학 명시)
├── terms.html              # 서비스 이용약관
├── robots.txt, sitemap.xml # 검색 엔진 최적화(SEO) 자산
│
├── css/
│   ├── base.css            # Plus Jakarta Sans + Newsreader, 클린 라이트 토큰
│   └── components.css      # 나침반 토끼 모션, 카드 반응형, 제로 오버플로우
│
├── js/
│   └── app.js              # 클라이언트 코어 엔진 (나침반, 로컬 서재, 드라이브 연동, Worker 프록시)
│
└── worker/                 # Cloudflare Edge Worker (서버리스 AI 프록시 백엔드)
    ├── wrangler.toml       # 워커 배포 설정
    └── src/
        └── index.js        # 클라이언트 API 키 은닉 및 Gemini Flash 라우팅 엔진
```
