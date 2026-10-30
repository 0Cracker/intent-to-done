# 출처와 조정

2026-10-30 사용자가 제공한 자료와 인터뷰에서 정한 작업 방식을 바탕으로 새로 작성했다. 원문 전체의 복제나 원본 스킬의 무조건 호출을 요구하지 않는다.

- 사용자 제공 TalkFile_intent-workflow.zip.zip: 의도 초안과 인터뷰, 크기별 문서 조절, 기존 작업 재개와 정본 동기화. 위임 대상인 sdd-interview와 test-driven-development 본문은 ZIP에 포함되지 않았다.
- 사용자 제공 AI Native SDLC Playbook PDF: 단계별 산출물 연결, 자체 피드백과 별도 컨텍스트 검증의 구분, 검증 기준 보호. 기업 승인과 Claude 전용 훅을 그대로 이식하지 않았다.
- 사용자 제공 흐름도 이미지: 크기별 준비와 인계 문서의 조건부 사용.
- [pstack how](https://github.com/cursor/plugins/blob/main/pstack/skills/how/SKILL.md), [why](https://github.com/cursor/plugins/blob/main/pstack/skills/why/SKILL.md), [teach](https://github.com/cursor/plugins/blob/main/pstack/skills/teach/SKILL.md): 코드 흐름과 역사적 이유 조사, 쉬운 설명. 기능은 구분하고 주 담당 실행을 기본으로 재구성했다.
- [pstack tdd](https://github.com/cursor/plugins/blob/main/pstack/skills/tdd/SKILL.md), [동작 검사 원칙](https://github.com/cursor/plugins/blob/main/pstack/skills/principle-test-behavior-not-implementation/SKILL.md): 사양에 따른 기대값, 실행한 RED와 GREEN, 구현 세부에 덜 의존하는 검사. 버그 중심 원본의 생략 범위 대신 사용자와 합의한 TDD 적용과 예외를 사용했다.
- [pstack interrogate](https://github.com/cursor/plugins/blob/main/pstack/skills/interrogate/SKILL.md), [setup](https://github.com/cursor/plugins/blob/main/pstack/skills/setup-pstack/SKILL.md): 독립 검토와 실행 근거, 역할별 모델 설정. 고정 모델과 강제 병렬 조사, 자동 PR과 외부 전송 권한은 가져오지 않았다.
- [eli5](https://github.com/anthropics/claude-plugins-community/blob/main/eli5/skills/eli5/SKILL.md): 큰 그림과 적은 글자의 설명. 모든 응답의 HTML과 이미지 생성을 강제하지 않고 목적에 맞는 캡처, Mermaid, 표와 HTML을 선택한다.
- [Codex 스킬](https://learn.chatgpt.com/docs/build-skills), [Codex subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents), [Claude Code 스킬](https://code.claude.com/docs/en/skills), [Claude Code subagents](https://code.claude.com/docs/en/sub-agents): 도구별 지원은 실제 설정 시 다시 확인한다.

핵심 선택은 사용자 인터뷰에서 확정했다. 단계별 확인이 기본이며 명시된 구간만 자동 진행한다. 의도와 SDD는 충분히 인터뷰한다. 최초 테스트 근거 확인 후 확정 사양 안의 추가 테스트는 자동 진행한다. 리팩터링은 통과 기준선과 동등성 확인을 사용한다. 주 담당 포함 동시 총 3개이며 필수 검증을 못 하면 검증 완료를 보류한다.
