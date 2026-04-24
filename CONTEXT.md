# LLM Wiki Context for Handoff

## 프로젝트 개요

**mshuttle** 서비스의 운영을 관리하기 위한 LLM 기반 개인 위키입니다.

- **목적**: 회사 운영 문서의 구조화 및 지식 관리
- **단계**: Overview 단계 완료 → Domain Detail 단계 진입
- **현재 상태**: mshuttle 서비스 전체 흐름 overview 문서 완성

---

## 위키 구조

```
ps_wiki/
├── CLAUDE.md                 # 위키 스키마 및 컨벤션
├── index.md                  # 페이지 카탈로그
├── log.md                    # 작업 기록
├── raw/                      # 원본 소스 (수정 금지)
│   ├── articles/
│   ├── papers/
│   │   └── mshuttle 서비스 전체 흐름.md
│   └── ...
└── wiki/                     # 생성 페이지 (LLM 관리)
    ├── entities/
    │   └── mshuttle.md
    ├── concepts/
    │   ├── route.md
    │   ├── dispatching.md
    │   ├── control.md
    │   ├── settlement.md
    │   ├── driver-operation.md
    │   ├── simulation.md
    │   ├── quotation.md
    │   ├── operation-state.md
    │   └── scheduling-criticality.md
    └── sources/
        └── mshuttle-overview.md
```

---

## 컨벤션

**파일명**: 영어 kebab-case (자동화/LLM 분석 용이)
**제목**: 프론트매터 title에 한글 (사용자 친화)
**위키 운영**: Overview → Domain Detail → Synthesis

---

## mshuttle 서비스 개요

### 핵심 원칙
- **스케줄링이 서비스의 핵심** — 공차거리 최소화, 비용 합리성
- **경로가 기본 단위** — 모든 운행의 시작점

### 주요 흐름
```
견적 요청 또는 수요 판단
    ↓
경로 생성 (운영팀)
    ↓
배차 (기사 배정)
    ↓
운행 상태 진입
├─ 기사 운행 (앱 사용)
├─ 관제 (실시간 모니터링, 정기만)
└─ 탑승 (사용자)
    ↓
정산 (월 1회, 양방향)
```

### 주요 도메인 (7개)

1. **견적** — 외부 요청에 대한 가격 제시 및 협상
2. **기업/단체 계약** — 계약 체결 및 관리
3. **경로** — 상태 관리, 폐지, 통폐합
4. **유저 신청/탑승** — 알림받기, 탑승 신청, 홀딩
5. **배차/기사** — 기사 등록 관리, 시뮬레이션
6. **관제** — 정기 경로의 실시간 모니터링
7. **정산** — 기업 정산, 기사비 정산

### 현재까지의 Concept 페이지 (10개)

Learning domain (3):
- Spaced Repetition, Active Recall, Interleaving

mshuttle domain (7):
- Route, Dispatching, Control, Settlement
- Driver Operation, Simulation, Quotation
- Operation State, Scheduling Criticality

---

## 다음 작업: Domain Detail 단계

### 작업 방식

**각 도메인별로 다음 구조로 상세 문서 작성:**

```
wiki/domains/{domain_name}/
├── overview.md              # 도메인 개요
├── process.md               # 상세 프로세스
├── decision-framework.md    # 의사결정 기준
├── constraints.md           # 제약 조건 & 제한사항
├── edge-cases.md            # 예외 상황 처리
├── metrics.md               # 성과 측정 기준
└── risks.md                 # 리스크 & 오류 처리
```

### 각 도메인별 작성 가이드

**견적 (Quotation)**
- 가견적 생성 기준
- 마진율 구조
- 견적 확정 판단 기준
- 계약 변수

**경로 (Route)**
- 수익성 계산 방식
- 경로 폐지/통폐합 기준
- 인원 충원 판단 기준
- 일시중단 사유

**배차 (Dispatching)**
- 기사 선택 기준
- 배차 시간 (예정 vs 운행 상태)
- 기사 교체 트리거
- 효율성 평가

**관제 (Control)**
- 모니터링 항목
- 이상 감지 기준
- 개입 기준
- 데이터 검증

**정산 (Settlement)**
- 금액 계산 방식
- 데이터 검증 프로세스
- 오류 처리
- 분쟁 해결

**기사 관리 (Driver Management)**
- 기사 모집
- 교육 체계
- 성과 평가
- 이탈률 관리

**고객 관리 (Customer Management)**
- 고객 세분화 (기업 정기/비정기, 일반)
- 수익성 분석
- 이탈 위험 요소

---

## 현재 상태

- **Overview 문서**: ✓ 완성
- **Concept Pages**: ✓ 10개 완성 (교차참조 포함)
- **Index**: ✓ 업데이트됨
- **Log**: ✓ 작업 기록 있음

---

## 사용 방식

다른 환경에서 계속 진행할 때:

1. 이 파일(CONTEXT.md)을 참고해 맥락 파악
2. raw/papers의 mshuttle 원본 문서 참조
3. 각 도메인별로 wiki/domains/{domain_name}/ 폴더 생성
4. 위 "작성 가이드" 참고해 상세 문서 작성
5. 완성 후 index.md와 log.md 업데이트

---

## 다음 우선순위 (제안)

1. **정산** — 가장 중요한 도메인 (데이터 품질, 정확성)
2. **경로** — 핵심 단위 (상태 관리, 폐지 기준)
3. **배차** — 운영팀 핵심 업무 (자동화 기회)
4. 기타 도메인

