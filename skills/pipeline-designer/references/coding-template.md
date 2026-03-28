# 코딩/빌딩 파이프라인 템플릿

## 5단계 구체적 행동

| 단계 | 구체적 행동 | 출력물 | 사용 도구/방법론 |
|------|-----------|--------|----------------|
| Input | 기능 요구사항 수집, 이해관계자별 유스케이스 정의 | CPS + 유스케이스 맵 | AskUserQuestion, CPS 프레임 |
| Plan | 기술 스택 선정, 아키텍처 방향, 작업 분해(WBS) | PRD + 기술 스택 결정문 | TodoWrite, CPS → PRD 변환 |
| Design | DDD 도메인 모델, API 설계, 파일 구조 Blueprint | Blueprint 명세서 | SKILL.md Blueprint, DDD |
| Execute | 코드 작성 | 소스 코드 | project-setup, api-scaffold 스킬 |
| Lint | 코드 컨벤션, 타입 체크, 테스트, 네이밍 규칙 검증 | 린트 보고서 + 수정된 코드 | ESLint, TypeScript, tdd-test 스킬 |

## Input 단계 상세

AskUserQuestion으로 수집할 항목:

1. **Context**: 어떤 프로젝트/서비스인가? 기존 코드베이스가 있는가?
2. **Problem**: 현재 어떤 기능이 없거나 불편한가?
3. **Solution**: 기대하는 기능 범위, 기술 스택 선호, 배포 환경
4. **이해관계자별 유스케이스**: Primary User가 수행할 핵심 시나리오 3~5개

## Plan 단계 상세

TodoWrite로 작업을 분해한다:

1. 이해관계자별 기능 요구사항 정리
2. 기술 스택 결정 (프레임워크, DB, 인프라)
3. MVP 범위 확정 (v1 스코프)
4. 페이지/API 엔드포인트 목록 작성
5. 파일 구조 초안

## Design 단계 상세

Blueprint에 포함할 항목:

- **도메인 모델**: 핵심 엔티티와 관계 (예: User, Product, Order)
- **페이지 구조**: URL 라우팅 맵
- **API 설계**: 엔드포인트 목록 (Method + Path + 설명)
- **파일 네이밍 규칙**: `{도메인}_{기능}.tsx` 또는 프로젝트 컨벤션
- **컴포넌트 계층**: 페이지 → 레이아웃 → 위젯 → 원자 컴포넌트

## Execute 단계 스킬 체인

실행 순서:

1. `project-setup` — 프로젝트 구조 + 보일러플레이트
2. `api-scaffold` — API 엔드포인트 스캐폴딩
3. 페이지/컴포넌트 구현
4. 연동 및 통합

## Lint 규칙

| ID | 규칙 | 검증 방법 |
|----|------|----------|
| C-01 | 파일명은 Blueprint의 네이밍 규칙을 따른다 | 파일 목록 vs Blueprint 대조 |
| C-02 | 모든 API 엔드포인트에 에러 핸들링이 존재한다 | try-catch 또는 에러 미들웨어 확인 |
| C-03 | 컴포넌트는 단일 책임 원칙(SRP)을 준수한다 | 컴포넌트당 역할 1개 확인 |
| C-04 | 커밋 전 모든 테스트가 통과한다 | tdd-test 스킬 또는 `npm test` 실행 |

### C-01 상세: 네이밍 규칙 검증

Blueprint에 정의된 네이밍 패턴과 실제 생성된 파일명을 1:1 대조한다.
위반 시 파일명을 자동 수정하고, import 경로도 함께 업데이트한다.

### C-02 상세: 에러 핸들링 검증

모든 라우트 핸들러에 다음이 존재하는지 확인한다:
- try-catch 블록 또는 에러 미들웨어
- 적절한 HTTP 상태 코드 반환
- 에러 로깅

### C-03 상세: SRP 검증

각 컴포넌트/모듈이 하나의 책임만 가지는지 확인한다:
- 파일당 export된 컴포넌트/함수가 명확히 하나의 도메인에 속하는가
- UI와 비즈니스 로직이 분리되어 있는가

### C-04 상세: 테스트 검증

`tdd-test` 스킬을 호출하거나, 프로젝트의 테스트 러너를 실행하여 모든 테스트 통과를 확인한다.
실패 시 실패 원인을 분석하고 코드를 수정한 후 재실행한다.

## 파이프라인 인스턴스 예시

```
📌 업무 유형: 코딩/빌딩 (+ 기획 복합)
📌 이해관계자: 참가자 / 심사위원 / 스폰서 / 운영팀

━━━ 자동 생성된 파이프라인 ━━━

[Input] AskUserQuestion으로 수집:
  - Context: 어떤 해커톤인가? (사내/외부/학교)
  - Problem: 기존에 어떻게 운영했고, 뭐가 불편했나?
  - Solution: 기대하는 기능 범위 (등록만? 제출+심사까지?)
  - 이해관계자별 핵심 유스케이스 확인

[Plan] TodoWrite 파이프라인:
  1. 이해관계자별 기능 요구사항 정리
  2. 기술 스택 결정 (Next.js + Supabase + Vercel)
  3. MVP 범위 확정 (v1: 등록+제출+심사)
  4. 페이지/API 엔드포인트 목록 작성

[Design] Blueprint 명세:
  - 도메인 모델: Team, Submission, Judge, Score
  - 페이지 구조: /, /register, /submit, /admin, /judge
  - API 설계: /api/teams, /api/submissions, /api/scores
  - 파일 네이밍: {도메인}_{기능}.tsx

[Execute] 스킬 체인:
  project-setup → api-scaffold → 페이지 구현 → 연동

[Lint] 검증 체크리스트:
  □ C-01: Blueprint 네이밍 규칙 준수
  □ C-02: 모든 API에 에러 핸들링 존재
  □ C-03: 이해관계자별 유스케이스 100% 커버
  □ C-04: 모든 테스트 통과
```
