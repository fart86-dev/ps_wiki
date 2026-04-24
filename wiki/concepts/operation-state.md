---
title: "운행 상태 (Operation State)"
type: "concept"
tags: ["mshuttle", "operation-state", "route-management", "workflow"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# 운행 상태 (Operation State)

경로의 생명주기를 나타내는 상태값.

## 주요 상태

### 운행예정 (Pre-Operation)
**유저를 모집하는 단계**

- 유저 탑승 신청 수락
- 일정 인원 충족 기다림
- 충족 시 [배차](../concepts/dispatching.md) 진행
- 배차 완료 후 "운행" 상태로 전환

### 운행 (In-Operation)
**실제 운행이 이루어지는 단계**

동시 진행 사항:
- [기사 운행](../concepts/driver-operation.md) — 기사가 앱 사용, 탑승 체크
- [관제](../concepts/control.md) — 실시간 모니터링 (정기만)
- 탑승 — 유저 탑승

특수 상황:
- **기사 교체 필요** → 배차 재발생 (상태 유지)
- **인원 감소** → 충원/통폐합/폐지 검토
- **일시중단 필요** → 기간 데이터 추가

## 상태 전환도

```
운행예정
  ↓ (일정 인원 충족 + 배차)
운행
  ├─→ (기사 교체) → 배차 → [운행 유지]
  ├─→ (일시중단) → 기간 추가 → [자동 재개]
  ├─→ (인원 충원) → 마케팅
  ├─→ (경로 통폐합) → 병합 처리
  └─→ (경로 폐지) → 종료
```

## 중요 구분

### "운행"은 도메인이 아니라 상태값

"운행"은 경로의 상태를 나타낼 뿐, 다음 세 도메인이 동시에 진행됨:

1. [기사 운행](../concepts/driver-operation.md)
2. [관제](../concepts/control.md)
3. 탑승 (사용자 경험)

## 특수 상황 처리

### 일시중단
- 상태값 변경 아님 (상태는 여전히 "운행")
- **중단 기간 데이터를 추가**하는 방식
- 기간 종료 시 자동 재개
- **기사비 정산에서 해당 일자 차감**

### 인원 감소 시 처리 순서

1. **인원 충원** (마케팅 활동)
2. **경로 통폐합** (유사 경로 병합, 유저 이동)
3. **경로 폐지** (위 두 방법 모두 불가)

## 관련 개념

- [경로](../concepts/route.md) — 상태를 가지는 객체
- [배차](../concepts/dispatching.md) — 상태 전환의 트리거
- [정산](../concepts/settlement.md) — 상태 기반 금액 계산

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
