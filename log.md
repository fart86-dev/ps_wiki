# Operation Log

Append-only record of all ingest, query, and lint operations.

## [2026-04-24] design | AI Agent System 설계

- **Phase:** Wiki → Agent 자동화 시스템으로 진화
- **주요 결정:**
  - 7개 Core Agent 정의 (RouteManager, Dispatcher, Marketing, Control, Settlement, Quotation, Driver)
  - Settlement Agent 우선 자동화 선정 (월 1회 고정, 규칙 기반)
- **산출물:**
  - AGENT_SYSTEM.md — 7개 Agent의 상세 설계, 협력 흐름, 구현 계획
  - PROGRESS.md — 프로젝트 진행 상황, 블로킹 요소, 다음 단계
- **블로킹:** Settlement 정산 DB 구조 및 계산 공식 정보 필요
- **기대 효과:**
  - 정산: 월 3-4시간 수동 작업 → 0시간 (자동화)
  - 경로: 운영팀 의사결정 → 자동 생성
  - 배차: 수동 선택 → 최적화 자동 배정
  - 전체: 운영팀 3명 → 1명 (모니터링만)

---

## [2026-04-22] update | 경로 제작 및 배차 (v3 - 경로추천 항목)

- **Source:** raw/papers/route_and_dispatch.md (경로추천 등록 항목 수정)
- **Change:** 경로추천 등록 주의사항
  - Before: "신규 경로 안정화 후 켜는 것을 권장"
  - After: "추후 별도 등록"
- **Pages updated:** 1
  - route-creation-process.md — 테이블 항목 수정
- **Reason:** 경로추천 등록이 수동으로 진행되는 별도 프로세스임을 반영

---

## [2026-04-22] ingest | 경로 제작 및 배차 (v2 - 수정)

- **Source:** raw/papers/route_and_dispatch.md (수정 버전)
- **Pages created:** 2 (추가)
  - clustering.md — 경로 생성의 공간적 기초
  - route-creation-process.md — 시스템 6단계 + 10개 메타데이터
- **Pages updated:** 3
  - route-and-dispatch-detail.md — 클러스터, 시스템 프로세스, 메타데이터 추가
  - route.md — 클러스터와 경로 생성 프로세스 링크 추가
  - index.md — 21개 페이지로 업데이트
- **New Insights:**
  - 클러스터링이 경로 생성의 기초 (육각형 구역, Zoom 조절)
  - 경로제작은 6단계: 데이터 불러오기 → Point → LineString → 정류장 → 자동 생성 → 수동 저장
  - 메타데이터 10개 항목이 고객 경험과 정산에 직접 영향
  - "클러스터를 이해하지 못하면 경로 판단 불가능" — 핵심 개념

---

## [2026-04-22] ingest | 경로 제작 및 배차 (상세)

- **Source:** raw/papers/route_and_dispatch.md
- **Pages created:** 3
  - 1 source summary (route-and-dispatch-detail.md)
  - 2 new concepts (chaining-operations, marketing-for-demand)
- **Pages updated:** 2
  - route.md — 수요 기반 vs 요청 기반 경로 구분 강화
  - dispatching.md — 7단계 배차 프로세스 상세화

---

## [2026-04-22] ingest | mshuttle 서비스 전체 흐름

- **Source:** raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md
- **Pages created:** 12
  - 1 source summary (wiki/sources/mshuttle-overview.md)
  - 1 entity (mshuttle)
  - 10 concepts (route, dispatching, control, settlement, driver-operation, simulation, quotation, operation-state, scheduling-criticality)
- **Cross-references:** Established links between 10 concepts
- **Index updated:** 12 new pages, organized by domain
- **Key insights:**
  - Scheduling is the core value of mshuttle
  - Route is the fundamental unit of all operations
  - Dispatch occurs in two situations with different purposes
  - Settlement is a bidirectional monthly process
  - Data quality (from driver app) directly impacts settlement accuracy

---

## [2026-04-22] ingest | The Science of Effective Learning

- **Source:** raw/articles/example-effective-learning.md
- **Pages created:** 4
  - 1 source summary (wiki/sources/effective-learning.md)
  - 3 concepts (spaced-repetition, active-recall, interleaving)
- **Index updated:** 4 new pages added
- **Key topics:** learning, memory, spaced-repetition, active-recall, interleaving

---

## [2026-04-22] setup | LLM Wiki initialized

- Created schema (CLAUDE.md)
- Created index.md and log.md
- Set up folder structure
- Ready for first ingest

---

> 사용 패턴: `## [YYYY-MM-DD] operation-type | description`
> Operation types: ingest, query, lint, maintenance
