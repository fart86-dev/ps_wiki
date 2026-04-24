# 프로젝트 진행 상황

LLM Wiki → AI Agent System으로의 진화 과정

---

## 📊 현재 상태 (2026-04-24)

### ✅ 완료된 것들

#### 1. LLM Wiki 구축 (기본 구조)
- [x] CLAUDE.md - 스키마 및 워크플로우 정의
- [x] index.md - 페이지 카탈로그
- [x] log.md - 작업 기록
- [x] 폴더 구조 설정 (raw/, wiki/)

#### 2. 개념 페이지 작성 (16개 페이지)

**Learning Domain (3):**
- [x] spaced-repetition.md
- [x] active-recall.md
- [x] interleaving.md

**mshuttle Domain (11):**
- [x] route.md - 경로의 정의와 생명주기
- [x] dispatching.md - 7단계 배차 프로세스
- [x] operation-state.md - 경로 상태 관리
- [x] control.md - 실시간 모니터링
- [x] settlement.md - 월 1회 정산
- [x] driver-operation.md - 기사 운행
- [x] simulation.md - 경로 사전 확인
- [x] quotation.md - 견적 처리
- [x] scheduling-criticality.md - 스케줄링 가치
- [x] chaining-operations.md - 연계 운행
- [x] marketing-for-demand.md - 수요 기반 마케팅
- [x] clustering.md - 공간적 그룹화
- [x] route-creation-process.md - 6단계 경로 생성

**Entity (1):**
- [x] mshuttle.md - 회사 개요

**Sources (3):**
- [x] mshuttle-overview.md
- [x] route-and-dispatch-detail.md
- [x] effective-learning.md

#### 3. Source 문서 수정 및 반영
- [x] route_and_dispatch.md v2 수정 (클러스터링 상세화)
- [x] route_and_dispatch.md v3 수정 (경로추천 등록 정책 변경)
- [x] 모든 변경사항 log.md에 기록

#### 4. Agent 시스템 설계 (이 대화)
- [x] 7개 Core Agent 정의
  - RouteManagerAgent (경로 생성)
  - DispatcherAgent (배차)
  - MarketingAgent (마케팅)
  - ControlAgent (관제)
  - SettlementAgent (정산)
  - QuotationAgent (견적)
  - DriverAgent (기사)
- [x] Agent별 책임/입력/산출물 명시
- [x] Agent 협력 흐름도 작성
- [x] 우선순위 결정: **Settlement Agent 우선**

---

## 🔄 현재 진행 중

### Settlement Agent 설계

**상태:** 계산 로직 분석 완료 → 구현 준비 단계

**정보 수집 완료 (2026-04-24):**
- [x] 정산 계산 공식 — 6단계 공식 (코드 분석)
- [x] 데이터 엔티티 구조 — 8개 엔티티 (DrPay, DrSetl, Cald 등)
- [x] 특수 케이스 처리 규칙 — 운행중단, 이슈, 조정금액, 소개비
- [x] 정산 상태 흐름 — 미정산 → 정산완료 → 이체완료

**남은 정보:**
- [x] DB 테이블 ↔ 프론트 인터페이스 매핑 (8개 테이블 확인 완료 2026-04-24)
- [x] 백엔드 API 엔드포인트 분석 (13개 엔드포인트 확인 완료 2026-04-24)

---

## 📋 다음 단계

### Phase 1: Settlement Agent (우선순위 1)
1. ~~**정산 정보 수집**~~ ✅ 완료 (2026-04-24)
   - 계산 공식 6단계 파악
   - 8개 데이터 엔티티 구조 확인
   - 특수 케이스 분류 완료

2. ~~**DB 테이블 매핑**~~ ✅ 완료 (2026-04-24)
   - 8개 테이블 스키마 확인 (dr_pay, dr_setl, cald, rt_pause, dr_iss, dr_iss_amount, dr_pay_adjust, dr_ref)

3. ~~**백엔드 API 분석**~~ ✅ 완료 (2026-04-24)
   - 13개 API 엔드포인트 파악
   - 핵심: 계산은 프론트엔드, 백엔드는 저장만
   - 서비스: Setl2Service (조회) + DrSetlService (CRUD)

3. **Agent 코드 구현**
   - Python + FastAPI
   - 자동 계산 로직
   - 기존 정산 결과와 대조 검증

4. **자동 스케줄러 설정**
   - APScheduler로 매월 5일 자동 실행
   - 알림 설정 (Slack/이메일)

### Phase 2: RouteManagerAgent (우선순위 2)
- 클러스터링 알고리즘 구현
- 경로 자동 생성 로직
- DB 저장

### Phase 3: DispatcherAgent (우선순위 3)
- 기사 풀 분석
- 최적 배차 알고리즘
- 연계 운행 고려

### Phase 4: 나머지 Agent들
- MarketingAgent
- ControlAgent
- QuotationAgent

---

## 📁 파일 구조 (현재)

```
ps_wiki/
├── CLAUDE.md                 # 스키마 정의
├── AGENT_SYSTEM.md          # ⭐ 새로 추가 (Agent 설계)
├── PROGRESS.md              # ⭐ 새로 추가 (진행 상황)
├── index.md                 # 페이지 카탈로그
├── log.md                   # 작업 기록
├── raw/
│   ├── papers/
│   │   ├── mshuttle 서비스 전체 흐름.md
│   │   └── route_and_dispatch.md (v3 수정됨)
│   ├── articles/
│   │   └── example-effective-learning.md
│   ├── screenshots/
│   └── assets/
└── wiki/
    ├── entities/
    │   └── mshuttle.md
    ├── concepts/
    │   ├── route.md
    │   ├── dispatching.md
    │   ├── operation-state.md
    │   ├── control.md
    │   ├── settlement.md
    │   ├── driver-operation.md
    │   ├── simulation.md
    │   ├── quotation.md
    │   ├── scheduling-criticality.md
    │   ├── chaining-operations.md
    │   ├── marketing-for-demand.md
    │   ├── clustering.md
    │   ├── route-creation-process.md
    │   ├── spaced-repetition.md
    │   ├── active-recall.md
    │   └── interleaving.md
    ├── sources/
    │   ├── mshuttle-overview.md
    │   ├── route-and-dispatch-detail.md
    │   └── effective-learning.md
    └── syntheses/
        (아직 없음)
```

---

## 💡 주요 통찰

### Wiki 문서화의 가치
- 운영 프로세스를 "사람이 이해할 수 있는 형태"로 정리
- Agent 설계의 기초 자료가 됨
- 미래 유지보수 시 참고 자료

### Agent 자동화의 필요성
- 현재 운영팀이 업무에 관심 없음 → 자동화 필수
- DB 구조는 있지만 불완전 → 마이그레이션 필요
- 정산부터 시작하면 즉시 효과 (월 3-4시간 단축)

### 다른 PC에서 계속하기
- 이 파일들을 git commit으로 보존
- AGENT_SYSTEM.md에 필요한 정보 정리 (블로킹 리스트)
- PROGRESS.md로 현재 상태 추적

---

## 🎯 현재 블로킹 요소

**Settlement Agent → 보류 (2026-04-24)**

```
정보 수집은 완료:
✅ 계산 공식 (6단계)
✅ DB 스키마 (9개 테이블)
✅ 백엔드 API (13개 엔드포인트)
✅ 데이터 흐름 (프론트 계산 → 백엔드 저장)

보류 사유:
- 시스템은 이미 잘 되어있음 (계산, API, 어드민 완비)
- 병목은 사람: 오프라인 이슈를 시스템에 등록하지 않음
- 자동화해도 입력 데이터가 불완전하면 의미 없음
```

**프로젝트 방향 전환: 위키 지식 축적에 집중**

---

## 🔗 참고 링크

- AGENT_SYSTEM.md - 7개 Agent의 상세 설계
- CLAUDE.md - Wiki 스키마 및 컨벤션
- wiki/concepts/settlement.md - 정산의 개념적 이해
