# Praxis

*From thought to action.*

디자이너가 티켓 하나를 끝까지 직접 가져가기 위한 에이전트 스킬입니다.
조사하고, 문제를 정의하고, 프로토타입으로 검증하고, 구현한 뒤 결과를 보고합니다.

각 스킬은 한 단계만 맡고, 그 단계에서 무엇을 판단해야 하는지와 어디까지 하면 끝인지를 정해 둡니다.
에이전트는 시키면 다 하지만, 기준이 없으면 진입 경로 하나를 열어 보지 않고 "안내가 어디에도 없다"고 쓰거나
결정이 끝난 토글을 프로토타입에 남겨 둡니다. 이 기준은 실제 티켓을 하면서 그런 실수를 고쳐 가며 정했습니다.

Claude Code, Codex 같은 코딩 에이전트에서 씁니다.

## 설치

```bash
npx skills@latest add Hyunmin99/skills
```

## 흐름

| 단계 | 스킬 | 하는 것 |
|---|---|---|
| 1 | [`ticket-brief`](skills/ticket-brief/SKILL.md) | 티켓·채팅·PRD·고객 요청·코드·운영 화면을 조사해 배경과 As-is 보고서를 만든다 |
| 2 | [`screen-capture`](skills/screen-capture/SKILL.md) | 운영·로컬 화면을 데이터를 바꾸지 않고 캡처한다 |
| 3 | [`decision-prototype`](skills/decision-prototype/SKILL.md) | 아직 결정하지 않은 축만 토글하는 HTML 프로토타입을 만든다 |
| 4 | [`prd-fill`](skills/prd-fill/SKILL.md) | 정한 내용을 PRD의 기획·디자인 칸에 옮긴다 |
| 5 | [`design-implement`](skills/design-implement/SKILL.md) | 확정한 UI 변경을 제품 레포에 직접 구현하고 로컬에서 확인한다 |
| 6 | [`impl-report`](skills/impl-report/SKILL.md) | 전/후 캡처와 동작 규칙으로 구현 결과를 보여 준다 |
| - | [`html-report`](skills/html-report/SKILL.md) | 1·6단계의 보고서를 HTML로 만든다 (공용) |

단계는 건너뛰어도 됩니다. 문구 하나 바꾸는 티켓이면 1 → 5 → 6만 씁니다.

## 원칙

- **한 스킬은 한 단계만 합니다.** 각 SKILL.md 첫머리에 하지 않는 일과 그 일을 맡는 스킬을 적었습니다.
- **형식은 대문자 참고 파일에 둡니다.** 프로토타입 틀([`HARNESS.md`](skills/decision-prototype/HARNESS.md))처럼 반복해서 쓰는 결과물은 그대로 복사하게 합니다.
  에이전트는 규칙 문장보다 예시를 따라 하므로, 예시를 하나로 고정해 두는 편이 결과가 안정적입니다.
- **확인한 것과 확인하지 못한 것을 나눕니다.** 화면으로 본 것, 코드로만 본 것, 보지 못한 것을 섞어 쓰지 않습니다.
- **요청하지 않은 엣지케이스를 덧붙이지 않습니다.** 걸리는 점은 결과물 밖에서 한 줄로 말합니다.

## 디자인 기준

보고서는 [salesmap.kr/design.md](https://salesmap.kr/design.md)의 Report 패턴을 따릅니다. 세일즈맵이 외부 에이전트용으로 공개한
디자인 문서입니다. 다른 디자인 시스템을 쓰려면 `html-report`의 1절 링크만 바꾸면 됩니다.

## 레포마다 다른 것

빌드 명령, 로컬 서버 띄우는 법, 테스트 함정처럼 제품 레포마다 다른 내용은 공개하지 않고 `local/<레포>.md`에 둡니다
(`.gitignore` 대상). `design-implement`가 있으면 읽습니다. 형식은 [`REPO-NOTES.example.md`](skills/design-implement/REPO-NOTES.example.md)를 보세요.

## License

MIT
