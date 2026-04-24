---
title: "mshuttle"
type: "entity"
tags: ["company", "shared-shuttle", "service"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# mshuttle

공유셔틀을 운행하는 회사.

## 비즈니스 모델

- 버스나 기사를 직접 소유하지 않음
- 경로 생성, 배차, 관제, 정산까지 **운행 전반을 관리**하고 책임
- 스케줄링을 통해 효율성과 비용 합리성 추구

## 핵심 운영 원칙

**스케줄링이 서비스의 핵심**

여러 유저가 같은 경로를 공유하고, 한 기사가 여러 경로를 담당하는 구조에서:
- 공차거리(deadheading) 최소화
- 비용 합리성 달성
- 운영팀의 수동 스케줄링 의존 → DB 쿼리로 근거 데이터 제공받아 의사결정

## 참여 주체

| 주체 | 역할 |
|------|------|
| [외부 업체/개인](../entities/external-customer.md) | 셔틀 운행 요청, 비용 지급 |
| [유저 (탑승자)](../entities/user.md) | 실제 탑승 |
| [운영팀](../entities/operations-team.md) | 경로 생성, 배차, 관제, 정산 |
| [기사](../entities/driver.md) | 셔틀 운행 |
| [전세버스 업체](../entities/bus-company.md) | 기사 소속, 기사비 수령 |

## 운영 흐름

→ [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)

## 도메인 구조

- [견적](../concepts/quotation.md)
- [경로](../concepts/route.md)
- [배차](../concepts/dispatching.md)
- [관제](../concepts/control.md)
- [정산](../concepts/settlement.md)

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
