# 모델 설정의 도구별 적용

설정 시점의 공식 문서와 실제 설치 버전을 확인한다. 아래는 2026-10-30 확인한 항목이며, 계정별 이용 권한과 현재 클라이언트 지원을 보장하지 않는다.

## Codex

[공식 subagents 문서](https://learn.chatgpt.com/docs/agent-configuration/subagents)에 따르면 전체 기본값은 config.toml의 agents.default_subagent_model과 agents.default_subagent_reasoning_effort다. 역할별 사용자 정의 에이전트에는 model과 model_reasoning_effort를 둘 수 있다. 역할 파일은 별도 이름과 설명, 지침이 필요하다.

역할 파일의 명시 값이 기본값과 호출 시 지정값을 덮어쓸 수 있다. 설치된 버전의 규칙을 확인하고 한 곳을 명확한 설정 원본으로 정한다. 상속을 원하면 지원하지 않는 inherit 문자열을 TOML의 model에 쓰지 말고 관련 override를 생략하거나 사용자가 요청한 범위에서 제거한다.

agents.max_concurrent_threads_per_session은 주 담당 제외 상한이므로 2를 설정하면 보조 동시 상한에 대응한다. 이미 다른 작업이 쓰는 전역 에이전트 정의를 무단 교체하지 않는다.

## Claude Code

[공식 subagents 문서](https://code.claude.com/docs/en/sub-agents)에 따르면 역할 정의의 model과 effort로 모델과 추론을 정할 수 있다. model은 해당 환경에서 지원하는 ID나 alias, 또는 inherit를 사용한다. 전역 기본값으로 CLAUDE_CODE_SUBAGENT_MODEL이 있지만 단발 호출과 역할 정의, 강제 환경 설정에 따른 우선순위를 확인해야 한다.

CLAUDE_CODE_EFFORT_LEVEL 환경값이 역할 effort보다 우선할 수 있다. 모델별 지원 수준을 확인하고 충돌 시 요청값과 실제 적용값을 보고한다.

CLAUDE_CODE_MAX_CONCURRENT_SUBAGENTS를 2로 설정하는 수단이 있지만 fork, 재개와 별도 에이전트 기능 등에 예외가 있다. 워크플로의 주 담당 포함 총 3개 규칙을 호출 지침에도 둔다. 재위임은 기본으로 끄거나 주 담당의 명시적 배분에 한정한다.

## 적용 검증

- 기존 파일을 읽고 요청한 필드와 정의만 최소 변경한다.
- 현재 제공되는 검증기와 파서를 이용해 문법을 확인하고 도구가 설정을 읽는지 확인한다.
- 계정에 모델이 표시되는 것, 요청에 사용할 수 있는 것, 실제 호출에서 적용된 것은 구분한다.
- 실제 호출이 필요하면 이미 필요한 작은 작업에 연결해 확인하고, 불필요한 유료 호출을 반복하지 않는다.
- 도구에서 적용값을 제공하지 않으면 “요청한 값”과 “적용 미확인”을 보고한다. 존재하지 않는 상태 조회 명령을 만들어내지 않는다.
- 설정이 다음 실행부터 적용되는 경우 재시작이나 새 세션 조건을 알린다. 이번 실행의 모델이 이미 바뀌었다고 표시하지 않는다.
