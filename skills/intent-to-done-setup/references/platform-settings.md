# 모델 설정의 도구별 적용

설정 시점의 공식 문서와 설치 버전을 확인한다. 아래는 2026-10-30 확인한 항목이며 계정 권한과 현재 클라이언트 지원을 보장하지 않는다.

## Codex

[공식 subagents 문서](https://learn.chatgpt.com/docs/agent-configuration/subagents)의 전체 기본값은 config.toml의 agents.default_subagent_model과 agents.default_subagent_reasoning_effort다. 역할별 사용자 정의 에이전트는 model과 model_reasoning_effort를 둘 수 있다. 역할 파일에는 별도 이름, 설명과 지침이 필요하다.

역할 파일의 명시 값은 기본값과 호출 지정값을 덮어쓸 수 있다. 설치 버전의 규칙을 확인하고 설정 원본을 한 곳으로 정한다. 상속은 TOML의 model에 미지원 inherit 문자열을 쓰지 말고, 관련 override를 생략하거나 요청 범위에서 제거한다.

agents.max_concurrent_threads_per_session은 주 담당 제외 상한이므로 2가 보조 동시 상한에 대응한다. 다른 작업이 쓰는 전역 에이전트 정의를 무단 교체하지 않는다.

## Claude Code

[공식 subagents 문서](https://code.claude.com/docs/en/sub-agents)에 따르면 역할 정의의 model과 effort로 모델과 추론을 정할 수 있다. model은 환경에서 지원하는 ID, alias 또는 inherit를 쓴다. 전역 기본값 CLAUDE_CODE_SUBAGENT_MODEL과 단발 호출, 역할 정의, 강제 환경 설정의 우선순위를 확인한다.

CLAUDE_CODE_EFFORT_LEVEL은 역할 effort보다 우선할 수 있다. 모델별 지원 수준을 확인하고 충돌 시 요청값과 실제 적용값을 보고한다.

CLAUDE_CODE_MAX_CONCURRENT_SUBAGENTS를 2로 설정할 수 있지만 fork, 재개와 별도 에이전트 기능 등에 예외가 있다. 호출 지침에도 주 담당 포함 총 3개 규칙을 둔다. 재위임은 기본으로 끄거나 주 담당의 명시적 배분에 한정한다.

## 적용 검증

- 기존 파일에서 요청한 필드와 정의만 최소 변경한다.
- 현재 검증기와 파서로 문법과 도구의 설정 인식을 확인한다.
- 계정의 모델 표시, 요청 가능 여부와 실제 호출 적용을 구분한다.
- 실제 호출이 필요하면 이미 필요한 작은 작업에 연결한다. 불필요한 유료 호출을 반복하지 않는다.
- 적용값을 제공하지 않으면 “요청한 값”과 “적용 미확인”을 보고한다. 없는 상태 조회 명령을 지어내지 않는다.
- 다음 실행부터 적용되면 재시작이나 새 세션 조건을 알린다. 현재 모델이 이미 바뀌었다고 표시하지 않는다.
