# Operation Log

Append-only record of all ingest, query, and lint operations.

## [2026-08-25] ingest | rtn_psn 탑승자 앱 (코드 분석)

- **Source:** rtn_psn/ (React Native 하이브리드 WebView 앱, 위성 위키 llm-wiki/ 기준)
- **Pages created:** 2
  - wiki/sources/rtn-psn-app.md — 탑승자 앱 코드 분석 요약
  - wiki/concepts/passenger-app.md — 탑승자 앱 개념 (탑승/유저 노드)
- **Pages updated:** 1
  - index.md — concept/source 항목 추가, 카운트 25 pages / 5 sources
- **Key findings:**
  - 도메인 개념 트리에 없던 "탑승자(유저)" 측 페이지 공백을 메움 (기존 driver-operation의 대응)
  - 4계층 브릿지 + 3종 메시지 계약(function/response/listener) 문서화
  - 자체 OTA 프로토콜, iOS 쿠키 수동 영속화 요약
  - 레포 간 의존성(OTA가 드라이버앱 API 공유, drapp 정렬 진행)은 needs-verification로 표기

---

## [2026-04-24] update | dispatch 테이블 + 보충 정보

- **Source:** 사용자 직접 제공
- **추가된 정보:**
  - dispatch 테이블 스키마 (9개 테이블로 확장)
  - cald는 전역 캘린더 (경로별 아님)
  - runnCaldSchd = 경로별 운행 요일 정의
  - orgList = 서비스 제공 업체 (기사비와 직접 무관)
  - 기업/단체 정산(받는 방향)은 기사비와 직접 연결 어려움
- **Pages updated:** 1
  - settlement-calc-code.md — dispatch 스키마, 보충 설명 추가

---

## [2026-04-24] ingest | 정산 백엔드 API 분석

- **Source:** admin-drcal-restapi/ (Fastify 백엔드)
- **Endpoints found:** 13개 (GET 4, POST 5, PUT 1, DELETE 2, PUT 1)
- **Pages updated:** 1
  - settlement-calc-code.md — 백엔드 API 섹션 추가, 데이터 흐름 다이어그램
- **Files updated:** 1
  - PROGRESS.md — 모든 정보 수집 완료 상태로 업데이트
- **Key findings:**
  - 계산은 프론트엔드에서 수행, 백엔드는 결과 저장만
  - Setl2Service: 데이터 조회 (cal, period, findIss, findAdjust, findRtPause)
  - DrSetlService: CRUD + transfer 처리
  - dr_pay_adjust.amount DOUBLE 타입은 실수 확인
  - bizCd 구분: 0=일반, 1=변형, 2=소개비

---

## [2026-04-24] ingest | 정산 DB 스키마 매핑

- **Source:** DB CREATE TABLE 직접 제공 (8개 테이블)
- **Tables:** dr_pay, dr_setl, cald, rt_pause, dr_iss, dr_iss_amount, dr_pay_adjust, dr_ref
- **Pages updated:** 1
  - settlement-calc-code.md — DB 스키마 섹션 추가, ER 다이어그램 추가
- **Files updated:** 2
  - AGENT_SYSTEM.md — DB 매핑 블로킹 해소
  - PROGRESS.md — 진행 상황 업데이트
- **Key findings:**
  - dr_setl에 계산 결과 전체가 저장됨 (총 16개 금액/일수 칼럼)
  - dr_pay_adjust.amount가 DOUBLE 타입 (다른 금액은 INT) — 소수점 주의
  - dr_iss_amount.board_reward_ids가 JSON 타입 — 탑승 보상 연동
  - 모든 날짜가 VARCHAR 타입 — 문자열 비교 처리 필요

---

## [2026-04-24] ingest | 정산 계산 로직 코드 분석

- **Source:** admin_drcal/src/pages/Setl/Setl/ (프론트엔드 코드)
- **Pages created:** 1
  - settlement-calc-code.md — 정산 계산 공식, 데이터 모델, 특수 케이스 상세
- **Pages updated:** 1
  - settlement.md — 실제 계산 공식, 정산 기간, 상태 흐름 추가
- **Files updated:** 2
  - AGENT_SYSTEM.md — Settlement Agent 블로킹 해소, 상세 계산 로직 반영
  - PROGRESS.md — 진행 상황 업데이트
- **Key findings:**
  - 6단계 계산 공식: 계약금액 → 일수계산 → 미운행차감 → 이슈조정 → VAT → 최종금액
  - 8개 데이터 엔티티: DrPay, DrSetl, Cald, RtPause, DrIss, DrIssAmount, DrPayAdjust, DrRef
  - 정산 기간은 setlStartDay에 따라 당월/전월 시작 분기
  - 정산 상태: 미정산 → 정산완료 → 이체완료(잠금)
  - **블로킹 해소:** 계산 공식 + 특수 케이스 모두 파악 완료

---

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
