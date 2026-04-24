---
title: "견적 (Quotation)"
type: "concept"
tags: ["mshuttle", "quotation", "sales", "operations"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# 견적 (Quotation)

외부 업체/개인의 셔틀 운행 요청에 대해 운영팀이 진행하는 가격 제시 및 협상 프로세스.

## 견적 요청 (Request)

외부 업체/개인이:
- **홈페이지** 또는 **전화**로 셔틀 운행 요청
- 운영팀이 접수

## 3단계 프로세스

### 1단계: 가견적 생성 (Preliminary Quote)
- 경로 및 기사 조건 검토
- 가견적 작성
- 업체/개인과 대화 시작

### 2단계: 견적 확정 (Confirmed Quote)
- 경로·기사 조건 조율 완료
- 업체/개인과 협의
- **견적 확정 및 계약 성사**

### 3단계: 경로 생성 (Route Creation)
- 계약 성사 후 정식 경로 생성
- [경로](../concepts/route.md) 상태로 진입

## 경로 유형 결정

견적을 통해 생성되는 경로는:
- **정기** (출퇴근 등)
- **비정기** (1회성)

로 구분되어 이후 운영 방식이 달라짐

## 특징

- **주요 수익 원천** (외부 계약 고객)
- **운영팀의 수동 의사결정** 중심
- DB 쿼리로 근거 데이터 제공받음
- 협상 과정 필수

## 관련 개념

- [경로](../concepts/route.md) — 견적 확정 후 생성
- [배차](../concepts/dispatching.md) — 견적 후 다음 단계

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
