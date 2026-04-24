---
title: "mshuttle 서비스 전체 흐름"
type: "source"
tags: ["mshuttle", "service", "business-model", "operations"]
created: "2026-04-22"
updated: "2026-04-22"
source_url: "internal"
source_date: "2026-04-22"
---

# mshuttle 서비스 전체 흐름

**원본:** raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md

## 핵심 개념

mshuttle은 공유셔틀을 운행하는 회사. 버스나 기사를 직접 소유하지 않으나, **경로 생성부터 배차, 관제, 정산까지 운행 전반을 관리**.

**스케줄링이 서비스의 핵심**: 여러 유저가 같은 경로 공유 + 기사 한 명이 여러 경로 담당 → 누가 언제 어디서 타는지를 얼마나 효율적으로 배치하느냐가 공차거리 최소화와 비용 합리성에 직결.

## 주요 흐름

```
견적 요청/수요 판단
    ↓
경로 생성 (운영팀)
    ↓
배차 (기사 배정)
    ↓
운행 상태 진입
    ├─ 기사 운행 (앱 사용, 탑승 체크)
    ├─ 관제 (실시간 모니터링)
    └─ 탑승 (유저)
    ↓
정산 (월 1회)
```

## 주요 발견

- **두 가지 경로 생성 경로**: 외부 견적 요청 vs 유저 수요 판단 (자체)
- **배차가 두 상태에서 발생**: 운행예정(시작) vs 운행(교체)
- **운행 상태의 동시성**: 기사 운행, 관제, 탑승이 동시에 진행
- **경로 상태**: 운행예정 → 운행 → (선택: 홀딩, 일시중단, 충원, 통폐합, 폐지)
- **일반 경로의 상품화**: 2일 무료 → 1달 단위 전환

## 관련 개체 및 개념

- [mshuttle (회사)](../entities/mshuttle.md)
- [경로 (Route)](../concepts/route.md)
- [배차 (Dispatching)](../concepts/dispatching.md)
- [운행 상태](../concepts/operation-state.md)
- [정산 (Settlement)](../concepts/settlement.md)
- [관제 (Control)](../concepts/control.md)
- [스케줄링의 중요성](../concepts/scheduling-criticality.md)
