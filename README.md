# m-SIGNAL · Materials Signal Intelligence

SK hynix 소재전략팀 전용 인텔리전스 시스템 — 소재 시장 동향 · 기술 변곡점 · BP 활동을 자동 수집 · 분석 · 보고서화

**🌐 Live**: https://piko9388.github.io/mSIGNAL/

---

## 시스템 구성 (v2.1.1 통합 아키텍처)

| 영역 | URL | 역할 |
|---|---|---|
| 🛰️ **크롤링** | `/crawler/` | 400+ 외부 소스 자동 수집 · Gemini/Claude 기반 LLM 필터링 · Bundle 생성 (구 mSMI 흡수) |
| 🗺️ **OVERVIEW** | `/overview.html` | 시스템 구조 · 데이터 파이프라인 · 5 Tier 구조 안내 |
| 📊 **보고서** | `/index.html`, `/weekly/` | 매주 금 발행되는 Weekly Report 아카이브 |
| 📈 **누적관리** | `/trend.html` | BP·소재군·키워드 누적 트렌드 (Phase 2 개발 예정) |

## 폴더 구조

```
/
├── index.html              # 랜딩 · 보고서 아카이브 허브
├── overview.html           # System Overview
├── trend.html              # 누적관리 (Phase 2 placeholder)
├── crawler/
│   └── index.html          # 크롤링 시스템 (구 mSMI v1.8.7 흡수)
├── weekly/
│   ├── WW17.html           # 주간 보고서 (WW별 1파일)
│   └── WW18.html           # (차주 발행 예정)
├── assets/
│   └── logo.png            # SK hynix 로고
└── templates/
    ├── daily-signal.html   # Daily Signal 이메일 템플릿
    └── key-signal.html     # Key Signal 공유 카드
```

## 통합 워크플로우

매주 금요일 오전 발행 사이클:

```
1. 크롤링 페이지 접속 → ⟳ Refresh (60~120초)
2. 4개 탭 순회: 산업·소재·BP·SKH 데이터 검토
3. 🎁 Bundle 클릭 → Standard 크기 + Dual-read 스타일 선택
4. 📋 클립보드 복사 → Claude/ChatGPT/Gemini 등 LLM 채팅에 붙여넣기 → 보고서 생성
5. 결과를 weekly/WW{NN}.html 템플릿에 정리하여 발행
6. index.html Archive 섹션에 카드 추가
```

## 산출물

| 산출물 | 발송 주기 | 설명 |
|---|---|---|
| **Daily Signal** | 매일 08:00 KST | 전일 신규 Signal 요약 이메일 |
| **Weekly Report** | 매주 금 10:00 KST | Tier별 종합 10p 보고서 |
| **Key Signal** | Signal 발생 즉시 | 고영향 Signal 단건 공유 카드 |
| **BP Deep Dive** | 요청 시 48h 내 | 특정 BP 연간 종합 분석 |

## 배포 방법

### GitHub Pages 설정
1. Repository `Settings` → `Pages`
2. `Source`: `Deploy from a branch`
3. `Branch`: `main` / `root`
4. Save → `https://piko9388.github.io/mSIGNAL/`에서 자동 배포

### 주차별 보고서 추가
1. `weekly/WW{NN}.html` 생성 (이전 주 파일 복사 후 내용 교체)
2. `index.html`의 Archive 섹션에 카드 한 장 추가
3. `git commit -m "WW18 발행"` → `git push`

## 신뢰도 배지

- 🟢 **공식** — 기업 IR · 정부 발표 · 보도자료
- 🟠 **업계** — 전문 매체 다수 보도
- 🔴 **추정** — 단일 소스 · 정황 근거

## 보안 원칙

- **API Key는 HTML 코드에 직접 하드코딩 금지** — GitHub Pages 공개 배포 시 즉시 노출됨
- Gemini/Claude API Key는 브라우저 설정 탭에서 입력하고 `localStorage`에만 저장
- 이미 노출된 API Key는 즉시 폐기 후 재발급
- 팀 배포 시 Cloudflare Worker/Vercel Serverless Function 등 서버리스 프록시 권장
- 발행물(HTML) + 정형 JSON은 GitHub Pages 공개 가능 — 외부 인용 가능한 공개 정보만 포함
- BP 가중치·자사 관심 키워드 사전·내부 평가 매핑은 사내 별도 보관 (Confluence/Wiki/로컬)
- 누적 트렌드·BP 순위 데이터는 사내자산 — 사외 블로그·외부 플랫폼 절대 업로드 금지
- 사내 시스템명·플랫폼·평가체계는 본문에 절대 노출 금지 (Bundle 옵션으로 LLM 프롬프트에서 차단)

## 변경 이력

- **v2.1.1** (2026-04) — Gemini 1.5 계열 종료 대응: 기본 모델을 `gemini-2.5-flash`로 변경, `gemini-2.5-flash-lite`/`gemini-2.5-pro` 선택 옵션 추가, 기존 localStorage의 1.5 모델명 자동 마이그레이션
- **v2.1** (2026-04) — Gemini API Direct 호출 지원, Claude/Gemini Provider 선택, JSON 응답 파싱 및 API Key localStorage 저장 방식 반영
- **v2.0** (2026-04) — mSMI v1.8.7 통합 흡수 (`/crawler/`), 4개 메뉴 통합 네비, trend.html 신설, Issue→Signal 통일
- **v1.8.7** (이전) — Report Bundle, 기간 필터, 기사 누적, arXiv 학술 논문 수집
- **v1.7** (폐기) — 단일 보고서 스타일, 110 BP, 매번 새로 fetch

## 문의

**이정훈 TL**
- 📱 010-3376-7923
- ✉ junghoon12.lee@sk.com

---

*m-SIGNAL v2.1.1 · Materials Signal Intelligence · SK hynix 소재전략 · 내부용 · 무단 외부 공유 금지*
