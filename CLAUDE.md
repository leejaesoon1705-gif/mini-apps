# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 개요

`mini-apps/`에 있는 독립 실행형 브라우저 미니 앱 모음입니다(한국어 UI). 빌드 시스템, 패키지 매니저, 테스트, 린터, git 저장소가 모두 없습니다. 각 앱은 `<style>`과 `<script>`가 인라인으로 들어간 단일 `.html` 파일이며 외부 의존성이나 외부 URL이 없습니다. 루트의 `hello.txt`, `*.png`는 앱과 무관한 샘플/임시 파일입니다.

## 실행 방법

`mini-apps/index.html`을 브라우저에서 직접 열면 됩니다. 별도 명령어는 필요 없습니다.

## 구조

- `mini-apps/index.html`은 런처입니다. `<a class="card">` 링크를 손으로 나열한 그리드입니다. **새 앱을 추가하려면 `mini-apps/<이름>.html`을 만들고 `index.html`에 카드를 직접 추가해야 합니다.** 자동 탐색은 없습니다.
- 각 앱은 완전히 독립적이며 공유 CSS/JS가 없습니다. 공통 관례는 복사해서 씁니다.
  - `<html lang="ko">`, UI 문구는 한국어, 폰트는 `"Segoe UI","Malgun Gothic",system-ui`.
  - 테마는 `:root`의 CSS 변수로 관리합니다(`focus-timer.html`은 `prefers-color-scheme: dark` 오버라이드도 있음).
  - 캔버스 앱(`kaleidoscope.html`, `star-dodge.html`)은 `requestAnimationFrame`으로 렌더링합니다.
- 저장은 `localStorage`를 쓰며, 저장소가 막힌 환경에서도 동작하도록 항상 `try/catch`로 감쌉니다. 키는 앱별 접두사를 붙입니다.
  - `ft-state`, `ft-tasks`, `ft-active` (focus-timer, 스크립트 상단의 `load`/`save` JSON 헬퍼 사용)
  - `sd-best` (star-dodge 최고 점수)
  - 앱에 저장 기능을 추가할 때도 이 접두사 규칙과 try/catch 패턴을 따르세요.
