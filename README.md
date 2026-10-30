# Intent to Done v1

의도 인터뷰부터 SDD, TDD, 구현, 독립 검증과 완료 보고까지 연결하는 개인 코딩 워크플로다. Codex와 Claude Code에서 같은 공통 규칙을 사용한다.

## 구성

- [intent-to-done](skills/intent-to-done/SKILL.md): 충분한 의도와 사양 인터뷰, 테스트, 구현과 독립 검증.
- [intent-to-done-setup](skills/intent-to-done-setup/SKILL.md): 역할별 모델과 추론 설정 확인과 변경.
- how, why, teach는 별도 플레이북이며 기본 실행은 주 담당이다.
- 보고는 쉬운 설명과 필요한 캡처, Mermaid, 표와 HTML을 사용한다.

## 진행 규칙

단계별 사용자 확인이 기본이며 명시적으로 허용한 구간만 자동 진행한다. 최초 테스트 시나리오와 실제 변경 전 근거를 확인받은 뒤 확정 사양 안의 추가 테스트는 자동 수행한다. 새로운 기대 동작과 사양은 다시 확인한다.

신규 동작과 버그는 실제 RED부터 시작하고, 리팩터링은 변경 전 통과 기준선과 변경 후 동등성 확인을 사용한다. 동작 변경 없는 문서, 주석, 포맷팅과 폐기용 목업, 프로토타입은 이유와 대체 검증을 남기는 자동 예외다.

주 담당 포함 동시 최대 3개다. 같은 문제를 두 차례 수정해도 실패하면 보고하고, 필수 검증을 못 하면 검증 완료를 보류한다. 모델 값은 하드코딩하지 않으며 미설정은 부모 상속이다.

## 설치와 사용

Codex에서는 다음 요청으로 두 스킬을 설치한다.

```text
$skill-installer 0Cracker/intent-to-done 저장소의 skills/intent-to-done과 skills/intent-to-done-setup을 개인 스킬로 설치해줘.
```

Claude Code에서는 저장소를 로컬로 clone한 뒤 skills 안의 두 폴더 전체를 개인 스킬 위치인 ~/.claude/skills/에 복사한다. 기존 동명 폴더가 있으면 차이를 확인하고 기존 변경을 보존한다.

설치 후 Codex에서는 $intent-to-done, Claude Code에서는 /intent-to-done을 호출한다. 설정 스킬은 각각 $intent-to-done-setup, /intent-to-done-setup으로 호출한다. 보이지 않으면 새 세션에서 확인한다.

전 프로젝트에서 기본 적용하려면 Codex의 전역 AGENTS.md, Claude Code의 전역 CLAUDE.md에 다음 규칙을 기존 내용과 합친다.

> 코딩 작업에는 intent-to-done을 적용한다. 조사와 설명만 요청하면 해당 기능만 수행한다.

원본 수정은 이 저장소에서 관리하고, 업데이트 후 설치본에 해당 변경을 반영한다. GitHub에 push하는 것만으로 로컬 설치본이 자동 갱신되지는 않는다.

## 검증 범위

v1은 스킬 형식과 내부 링크 검사, 제한된 Python 사례의 독립 행동 평가를 수행했다. 모호한 요청의 인터뷰 대기, 신규 기능의 실제 RED, 리팩터링 통과 기준선, 테스트 승인 후 구현과 다음 단계 대기를 확인했다.

도구별 모델 적용, 모든 자동 진행과 재개 경로, 실제 앱 통합을 보장하지 않는다. 실제 환경에서 적용과 결과를 확인한다. 별도 플러그인 manifest나 실행 엔진은 포함하지 않는다.

## 참고 자료

아래 자료를 참고하고, 사용자와 합의한 작업 방식에 맞게 재구성했다.

- **intent-workflow:** 의도 인터뷰, SDD 연결, 작업 크기에 따른 절차 조절.
- **AI-Native SDLC Playbook:** 단계별 산출물 연결, 검증 루프, 독립 검증.
- **[pstack](https://github.com/cursor/plugins/tree/main/pstack):** 코드 탐색과 설계 이유 조사, 쉬운 설명, TDD와 근거 중심 검증, 모델 설정.
- **[eli5](https://github.com/anthropics/claude-plugins-community/tree/main/eli5):** 큰 그림과 적은 글자로 전달하는 설명 방식.
- **Codex와 Claude Code 공식 문서:** 스킬 구성, 서브에이전트와 모델 설정 방식.
