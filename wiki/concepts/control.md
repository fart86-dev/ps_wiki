---
title: "관제 (Control/Monitoring)"
type: "concept"
tags: ["mshuttle", "control", "monitoring", "operations"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# 관제 (Control/Monitoring)

운영팀이 실시간으로 운행 상태를 모니터링하는 활동.

## 특징

- **정기 경로만** 진행 (비정기 운행은 관제 없음)
- **운행 상태 중** 매 운행일마다 진행
- 운영팀이 관제 앱을 통해 실시간 모니터링

## 데이터 수집 의존성

운영팀이 관제 데이터를 수집하려면:
- **기사가 기사 앱 사용 필수**
- 앱 미사용 시 관제 데이터 수집 불가
- 따라서 기사 앱 사용 여부 확인이 중요

## 관제의 역할

- 실시간 운행 상태 파악
- 문제 상황 신속 대응 (예: 기사 지연, 탑승 오류 등)
- 운행 데이터 기록 (정산 근거)

## 운행 상태에서의 동시 진행

관제는 다음과 함께 동시에 진행:
- [기사 운행](../concepts/driver-operation.md) — 기사가 앱 사용
- 탑승 — 유저 탑승

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
