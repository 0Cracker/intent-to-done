# 출처와 조정

2026-10-30 사용자 자료와 인터뷰에서 정한 작업 방식을 바탕으로 작성했다. 원문 전체 복제와 원본 스킬의 무조건 호출은 요구하지 않는다.

- 사용자 제공 TalkFile_intent-workflow.zip.zip: 의도 초안과 인터뷰, 크기별 문서 조절, 작업 재개와 정본 동기화. 위임 대상 sdd-interview와 test-driven-development 본문은 ZIP에 없었다.
- 사용자 제공 AI Native SDLC Playbook PDF: 단계별 산출물 연결, 자체 피드백과 별도 컨텍스트 검증의 구분, 검증 기준 보호. 기업 승인과 Claude 전용 훅을 그대로 이식하지 않았다.
- 사용자 제공 흐름도 이미지: 크기별 준비와 인계 문서의 조건부 사용.
- [pstack how](https://github.com/cursor/plugins/blob/main/pstack/skills/how/SKILL.md), [why](https://github.com/cursor/plugins/blob/main/pstack/skills/why/SKILL.md), [teach](https://github.com/cursor/plugins/blob/main/pstack/skills/teach/SKILL.md): 코드 흐름과 역사적 이유 조사, 쉬운 설명. 기능은 구분하고 주 담당 실행을 기본으로 재구성했다.
- [pstack tdd](https://github.com/cursor/plugins/blob/main/pstack/skills/tdd/SKILL.md), [동작 검사 원칙](https://github.com/cursor/plugins/blob/main/pstack/skills/principle-test-behavior-not-implementation/SKILL.md): 사양에 따른 기대값, 실행한 RED와 GREEN, 구현 세부에 덜 의존하는 검사. 버그 중심 원본의 생략 범위 대신 사용자와 합의한 TDD 적용과 예외를 사용했다.
- [pstack interrogate](https://github.com/cursor/plugins/blob/main/pstack/skills/interrogate/SKILL.md), [setup](https://github.com/cursor/plugins/blob/main/pstack/skills/setup-pstack/SKILL.md): 독립 검토와 실행 근거, 역할별 모델 설정. 고정 모델과 강제 병렬 조사, 자동 PR과 외부 전송 권한은 가져오지 않았다.
- [eli5](https://github.com/anthropics/claude-plugins-community/blob/main/eli5/skills/eli5/SKILL.md): 큰 그림과 적은 글자의 설명. 모든 응답의 HTML과 이미지 생성을 강제하지 않고 목적에 맞는 캡처, Mermaid, 표와 HTML을 선택한다.
- [Codex 스킬](https://learn.chatgpt.com/docs/build-skills), [Codex subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents), [Claude Code 스킬](https://code.claude.com/docs/en/skills), [Claude Code subagents](https://code.claude.com/docs/en/sub-agents): 도구별 지원은 실제 설정 시 다시 확인한다.

핵심 선택은 사용자 인터뷰에서 확정했다. 기본은 단계별 확인이며 명시된 구간만 자동 진행한다. 의도와 SDD는 충분히 인터뷰한다. 최초 테스트 근거 확인 후 확정 사양 안의 추가 테스트는 자동 진행한다. 리팩터링은 통과 기준선과 동등성 확인을 쓴다. 주 담당 포함 동시 총 3개이며 필수 검증 불가 시 검증 완료를 보류한다.

## 2026-10-31 문서 템플릿 보완

아래 자료의 실제 본문과 이미지를 확인해 보완했다. 자료의 프로젝트 전용 규칙은 참고했으며 현재 사용자의 실행 지시로 취급하지 않았다.

| 확인한 자료 | 반영한 내용 | 현재 워크플로에 맞춘 조정 |
| --- | --- | --- |
| 사용자 첨부 `intent-workflow.zip`의 `intent-template.md`, `tasks-template.md`, `SKILL.md`, `origins.md` | 사용자 상황과 원하는 결과, 기존 구조의 경계, 미결 전수 인계, 파일과 순서, 위험과 증명 | 원본의 특정 서비스, 상태 라벨, 강제 커밋과 전송 절차는 가져오지 않고 독립된 한국어 템플릿으로 작성 |
| 사용자 첨부 `KakaoTalk_20261030_112514459.jpg`의 흐름도 | 크기에 맞춘 기록 깊이, 새 방향의 상세 의도, 인계 시에만 작업지시서 사용 | 기존 문서 모드와 단계별 확인을 유지하고, 문서의 분량과 선택적 분리 기준에 반영 |
| [저장소 README](https://github.com/0Cracker/intent-to-done/blob/main/README.md) | 레퍼런스 범위와 기존 진행 규칙 | 로컬 설치본의 문서화 보완을 유지하고 모델 설정용 스킬과 분리 |
| [Anthropic AI-native SDLC Playbook](https://claude.com/resources/articles/the-ai-native-sdlc-playbook)의 Plan, Design, Build | 의도에서 미결을 사양으로 연결, 변경 파일과 순서, 위험과 검증, 대화를 읽지 않은 담당자를 위한 계획 | 사용자 요청에 따라 기본 산출물을 intent.md, SDD.md, implementation.md, report.md로 나누며 자동 커밋, PR, 병합과 배포는 요구하지 않음 |
| [pstack how](https://github.com/cursor/plugins/blob/main/pstack/skills/how/SKILL.md), [why](https://github.com/cursor/plugins/blob/main/pstack/skills/why/SKILL.md), [teach](https://github.com/cursor/plugins/blob/main/pstack/skills/teach/SKILL.md) | 흐름과 소유 경계, 결정 근거와 추정의 구분, 사용자 행동 중심 설명 | 원본의 고정 모델, 병렬 조사와 매번 그림 생성을 가져오지 않음 |
| [pstack tdd](https://github.com/cursor/plugins/blob/main/pstack/skills/tdd/SKILL.md), [행동 검사](https://github.com/cursor/plugins/blob/main/pstack/skills/principle-test-behavior-not-implementation/SKILL.md), [검증 가능한 단위](https://github.com/cursor/plugins/blob/main/pstack/skills/principle-sequence-verifiable-units/SKILL.md) | 요구에서 구한 기대값, 실제 RED와 GREEN, 단위별 완료 증거 | 기존 TDD 적용 범위와 예외를 유지하고 원본의 재배치나 커밋 순서를 강제하지 않음 |
| [pstack interrogate](https://github.com/cursor/plugins/blob/main/pstack/skills/interrogate/SKILL.md), [show-me-your-work](https://github.com/cursor/plugins/blob/main/pstack/skills/show-me-your-work/SKILL.md) | 실제와 기대 결과, 재현 근거, 결정 이유와 후속 결과 | 정적 근거와 미확인 위험도 보존하고 별도 TSV 장부나 다른 모델의 필수 호출을 추가하지 않음 |
| [eli5](https://github.com/anthropics/claude-plugins-community/blob/main/eli5/skills/eli5/SKILL.md) | 적은 설명과 이해에 필요한 시각 자료 | HTML과 이미지 산출물을 필수로 만들지 않음 |
| [Codex 스킬 문서](https://learn.chatgpt.com/docs/build-skills), [Claude Code 지원 파일](https://code.claude.com/docs/en/skills#add-supporting-files) | 필요한 시점에 상세 템플릿을 읽는 구성 | 도구 전용 실행 옵션과 모델 설정은 이번 템플릿 변경 범위에 포함하지 않음 |

사용자 후속 요청으로 기존 문서 구조가 없으면 `docs/tasks/<작업-id>/`를 기본 적용한다. 의도는 `intent.md`, 사양은 `SDD.md`, 구현과 실행 근거는 `implementation.md`, 검증 판정과 결과는 `report.md`에 둔다. `task.md`는 재개할 상태와 승인 이력의 진입점이다. 이 파일명과 배치는 현재 사용자가 요청한 운영 방식이며 외부 레퍼런스의 의무 규격이 아니다. 기존 정본 위치와 승인 이력은 보존한다.
