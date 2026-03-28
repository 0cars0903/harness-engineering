# Harness Engineering Plugin

하네스 엔지니어링(HE) 일반화 메타 프레임워크 플러그인. 문제를 던지면 업무 유형을 자동 분류하고, 이해관계자 분석 → CPS → 5단계 파이프라인(Input → Plan → Design → Execute → Lint)을 자동 설계한다.

## Overview

코딩에서 검증된 HE 파이프라인을 **모든 지식 노동**에 일반화한다. AI 에이전트가 어떤 업무를 수행하든 구조화된 파이프라인을 거쳐 일관된 품질의 결과물을 생성하도록 한다.

### 핵심 설계 원칙

1. **구조는 고정, 내용은 동적** — 5단계 순서는 불변, 구체적 행동만 변한다
2. **설계와 실행의 분리** — 파이프라인 설계 후 사용자 승인을 거쳐 실행
3. **Lint는 하드 가이드** — 검증 미통과 결과물은 출력 불가
4. **Normal Form 수렴** — 같은 파이프라인이면 같은 구조의 결과물
5. **점진적 구체화** — 기초 템플릿 80% + 동적 생성 20%

## Components

### Skills (4개)

| 스킬 | 역할 | 트리거 |
|------|------|--------|
| `pipeline-designer` | 메타 스킬 — 문제 분류 → 파이프라인 자동 설계 | "파이프라인 설계", "하네스", "구조 잡아줘" |
| `writing-harness` | 글쓰기 전용 하네스 (Blueprint + W-01~W-08 Lint) | "글 써줘", "보고서", "에세이", "첨삭" |
| `analysis-harness` | 기획/분석 전용 하네스 (MECE + A-01~A-05 Lint) | "분석해줘", "기획서", "SWOT", "전략" |
| `research-harness` | 리서치 전용 하네스 (출처 검증 + R-01~R-05 Lint) | "조사해줘", "리서치", "트렌드", "비교" |

### Hooks (1개)

- **PreToolUse (Write|Edit)** — 파일 쓰기 전 활성 하네스의 Lint 규칙 사전 검증
- **Stop** — Execute 완료 후 Lint 미수행 시 경고

### MCP Servers (1개)

- **Notion** — 외부 문서/데이터 연동

## Usage

### 기본 사용법

문제를 던지면 `pipeline-designer`가 자동 트리거된다:

```
"해커톤 사이트 만들고 싶어"
→ 업무 유형: 코딩/빌딩 | 파이프라인 자동 설계 | 검토 후 실행

"자소서 쓰고 싶어"
→ 업무 유형: 글쓰기 | writing-harness 위임 | W-01~W-08 Lint 적용

"시장 분석 보고서 만들어줘"
→ 업무 유형: 기획/분석 | analysis-harness 위임 | A-01~A-05 Lint 적용
```

### 직접 하네스 호출

특정 하네스를 직접 사용할 수도 있다:

```
"이 글 writing-harness로 첨삭해줘"
"analysis-harness로 SWOT 분석해줘"
"research-harness로 기술 트렌드 조사해줘"
```

## Lint 규칙 요약

### 코딩 (C-01~C-04)
- C-01: 파일명 Blueprint 준수 | C-02: 에러 핸들링 | C-03: SRP | C-04: 테스트 통과

### 글쓰기 (W-01~W-08)
- W-01: 문장 60자 | W-02: 수동태 15% | W-03: H3 이내 | W-04: 단락 5문장
- W-05: 금지 어휘 | W-06: 두괄식 | W-07: 숫자 단위 | W-08: SSOT 정합성

### 기획/분석 (A-01~A-05)
- A-01: 출처 명시 | A-02: MECE | A-03: 논리적 도출 | A-04: 가설-검증 매핑 | A-05: Actionable

### 리서치 (R-01~R-05)
- R-01: 출처 존재 | R-02: 발행일 범위 | R-03: RQ 완결성 | R-04: 소스 다양성 | R-05: 관점 균형

## Setup

Notion MCP 연동을 위해 Notion integration이 설정되어 있어야 한다.

## Reference

- [HE 일반화 메타 프레임워크 (Notion)](https://www.notion.so/32d0654986f281e7b673ce3fe4e6c3a8)
