# Over the Rainbow — Interaction Test Prototype

반려동물 사별 이후, 사용자가 기억을 회상하는 흐름의 **UX Writing과 Interaction Design**을 검증하기 위한 저충실도 모바일 프로토타입입니다. 시각 디자인이 아니라 문장·침묵·전환·사용자 통제를 테스트합니다.

## 범위

- 393 × 852 모바일 프레임
- 6개 장면의 기억 회상 흐름
- 문장 페이드인, 문장 사이의 침묵, CTA 등장 시점 검증
- 언제든 멈추고 이어갈 수 있는 흐름
- `[이름]의 자리`라는 관계 중심 공간명

## 실행

배포된 URL 또는 아래 파일을 브라우저에서 열어 실행합니다.

`index.html`

질문 JSON을 실제로 불러오는 환경이 필요하면 프로젝트 루트에서 간단한 정적 서버를 실행합니다.

```powershell
python -m http.server 8000
```

그다음 `http://localhost:8000`으로 접속합니다. `file://`로 직접 열면 브라우저 보안 정책상 `questions.json`을 읽지 못할 수 있으며, 이 경우 화면은 내장된 동일 기본 질문으로 동작합니다.

## A/B 질문

질문 카피는 `assets/questions.json`에 분리되어 있습니다.

- `memory_question_a`: 창가 단서
- `memory_question_b`: 현관 단서

특정 variant를 고정해 볼 때는 URL에 `?variant=memory_question_a` 또는 `?variant=memory_question_b`를 추가합니다. variant를 지정하지 않으면 세션에 하나를 배정하고, 모든 로그에 `variantId`를 기록합니다.

## 테스트 모드

일반 참가자에게는 디버그 패널이 보이지 않습니다. 운영자 테스트에서는 URL에 `?test=true`를 추가합니다.

- 현재 화면·화면 체류 시간·전체 시간
- Animation Skip
- Previous / Next Screen
- 애니메이션 다시 보기
- JSON Export

실제 참가자에게 리듬을 검증할 때는 테스트 모드를 사용하지 않습니다.

## 로그와 개인정보

입력한 반려동물의 기억은 민감한 텍스트입니다.

- 입력 내용은 참가자 **기기의 LocalStorage에만 임시 저장**됩니다.
- JSON Export에는 입력 원문·사진 파일명·사진 파일을 넣지 않습니다.
- Export에는 입력 여부, 글자 수, 화면 진입 시각, 체류 시간, 버튼 클릭, 뒤로가기, 중도 종료, 완료 여부, 총 소요 시간, 질문 variant ID만 담깁니다.
- LocalStorage 방식이므로 참가자가 테스트 종료 후 **Export JSON을 내려받아 연구자에게 전달해야** 결과를 모을 수 있습니다.

## 배포

이 저장소는 Voice Guide, Memory Cue Library, Letter Prompt Rules 등 핵심 자산을 포함하므로 **Private GitHub Repository**로 운영합니다. Vercel은 private repository와 연동해도 자동 배포가 가능합니다.

`vercel.json`은 루트 URL을 인터랙션 프로토타입으로 연결합니다.
