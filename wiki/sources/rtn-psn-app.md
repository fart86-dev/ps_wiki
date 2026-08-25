---
title: "rtn_psn 탑승자 앱 (코드 분석)"
type: "source"
tags: ["mshuttle", "passenger", "react-native", "app", "webview"]
created: "2026-08-25"
updated: "2026-08-25"
source_url: "internal:rtn_psn (React Native 리포)"
source_date: "2026-08-25"
---

# rtn_psn 탑승자 앱 (코드 분석)

**원본:** `rtn_psn/` 리포지토리 (위성 위키 `rtn_psn/llm-wiki/` 기준)
**패키지:** com.modooshuttle.psn · **앱 이름:** 모두의셔틀 탑승자

> 이 요약은 rtn_psn 코드에서 직접 검증된 사실만 담는다. 도메인 일반론은 [탑승자 앱](../concepts/passenger-app.md) 개념 페이지 참고.

## 핵심 성격

rtn_psn은 **탑승자(유저)용 하이브리드 WebView 셸 앱**이다. 화면·예약·탑승 흐름 등 도메인 로직은 원격 웹(`https://psnapp.mosher.co.kr`)에 있고, 앱은 웹이 필요로 하는 **네이티브 능력만 브릿지로 노출**한다.

- React Native 0.84.1, MobX, react-native-webview 기반
- 커스텀 Turbo Module(rtn-*) 12종을 형제 디렉토리 `../rtn_modules/`에서 참조

## 주요 발견

- **4계층 브릿지**: WebView `onMessage` → `FuncStore`(라우터) → Controller(22종) → Service(27종) → `rtn-*` Turbo Module → 응답 역순 전달.
- **메시지 계약(3종 envelope)**:
  - 요청(웹→네이티브): `{ reqId, name, type:'function', action, params }`
  - 응답(네이티브→웹): `{ reqId, name, type, action, ok, data?, error? }`
  - 이벤트(네이티브→웹): `{ name, action, data, type:'listener' }` (단방향, reqId 없음)
- **자체 OTA(JS 번들 무선 업데이트)**: 앱 시작 시 WebView보다 먼저 OTA를 체크(게이트). `GET {드라이버앱 API}/ota` → `{rnVer, preSignedUrl, fileSize}` 응답. 임시파일 원자적 교체 + 재시도 3회 + 최소 크기 검증 후 `RNRestart`로 재시작. CodePush/EAS 미사용.
- **iOS 쿠키 수동 영속화**: WKWebView 쿠키 유실 대응으로 UserDefaults 백업/복원/flush 직접 구현. 인증 쿠키 `MSUW_SES`/`MSUW_AT`, 도메인 `.mosher.co.kr` 서브도메인 공유.
- **인앱 브라우저**: 웹이 `inApp.open({url})` 호출 → 모달 WebView, 닫을 때 `reqId`로 결과 반환(iOS는 쿠키 동기화 동반).

## 레포 간 의존성 (검증 필요)

- OTA가 탑승자 전용이 아닌 **드라이버앱 API(`CLIENT_API_DRAPP`)**를 공유 사용. 현재 `chore/260824_rtn_psn_sync` 브랜치에서 드라이버앱(rtn_drapp) 기준으로 리스너·InApp 계약을 "정렬(sync)" 중.
- 브릿지 메시지 계약이 웹·드라이버앱과 공통 계약인지 미확정. (needs-verification)

## 알려진 이슈 (rtn_psn 위성 위키 gotchas 기준)

- 이관된 네이티브 리스너(`CommonListener`)가 렌더 트리에서 주석 처리되어 현재 미마운트.
- WebView 진입 URL·UserAgent stage(`dev`)·OTA `ms-api-key`가 하드코딩.
- 브릿지 응답이 항상 `ok:true`(에러 응답 경로 없음).

## 관련 개체 및 개념

- [mshuttle (회사)](../entities/mshuttle.md)
- [탑승자 앱](../concepts/passenger-app.md)
- [기사 운행 (Driver Operation)](../concepts/driver-operation.md)
- [관제 (Control)](../concepts/control.md)
