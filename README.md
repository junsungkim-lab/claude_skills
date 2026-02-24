# Claude Code 커스텀 명령어 (Slash Commands) 만들기

> Claude Code에서 `/명령어` 형태로 나만의 자동화 명령어를 만드는 방법

---

## 목차

1. [개념 이해](#1-개념-이해)
2. [폴더 구조](#2-폴더-구조)
3. [명령어 만들기 (Step-by-step)](#3-명령어-만들기-step-by-step)
4. [파일 옵션 (Frontmatter)](#4-파일-옵션-frontmatter)
5. [예시 명령어 모음](#5-예시-명령어-모음)
6. [Skills vs Commands 차이](#6-skills-vs-commands-차이)

---

## 1. 개념 이해

Claude Code에서는 `.md` 파일 하나만 만들면 나만의 `/명령어`를 생성할 수 있습니다.

```
/풀스택생성 주식 알림 봇
/코드리뷰
/배포
```

**파일명 = 명령어 이름**

| 파일명 | 사용하는 명령어 |
|--------|---------------|
| `풀스택생성.md` | `/풀스택생성` |
| `코드리뷰.md` | `/코드리뷰` |
| `deploy.md` | `/deploy` |

---

## 2. 폴더 구조

### 프로젝트별 (해당 프로젝트에서만 사용)

```
내프로젝트/
└── .claude/
    └── commands/
        ├── 풀스택생성.md
        ├── 코드리뷰.md
        └── 배포.md
```

### 글로벌 (모든 프로젝트에서 사용)

```
~/.claude/
└── commands/
    ├── 풀스택생성.md
    ├── 코드리뷰.md
    └── 배포.md
```

> **추천:** 자주 쓰는 명령어는 글로벌(`~/.claude/commands/`)에, 프로젝트 전용은 `.claude/commands/`에 저장

---

## 3. 명령어 만들기 (Step-by-step)

### Step 1. 폴더 생성

```bash
# 글로벌 (모든 프로젝트에서 사용)
mkdir -p ~/.claude/commands

# 또는 프로젝트별
mkdir -p .claude/commands
```

### Step 2. md 파일 생성

만들고 싶은 명령어 이름으로 `.md` 파일을 생성합니다.

```bash
# /풀스택생성 명령어 만들기
touch ~/.claude/commands/풀스택생성.md
```

### Step 3. 파일 내용 작성

```markdown
---
description: React + Node.js 풀스택 앱을 생성합니다
argument-hint: <프로젝트 설명>
---

$ARGUMENTS 를 기반으로 아래 조건에 맞는 풀스택 프로젝트를 생성해줘.

**조건:**
- React (Vite + TypeScript) 프론트엔드
- Node.js (Express + TypeScript) 백엔드
- 폴더 구조, package.json 포함
- npm install 후 즉시 실행 가능하게
- README에 실행 방법 포함
```

### Step 4. Claude Code에서 사용

```
/풀스택생성 주식 실시간 알림 봇. Naver/Daum 크롤링 + Telegram 발송.
```

`$ARGUMENTS` 자리에 내가 입력한 텍스트가 자동으로 들어갑니다.

---

## 4. 파일 옵션 (Frontmatter)

```markdown
---
description: 명령어 설명 (/help 에서 표시됨)
argument-hint: <필수인자> [선택인자]
allowed-tools: Read, Glob, Grep, Bash
model: sonnet
---
```

| 옵션 | 설명 |
|------|------|
| `description` | `/help` 명령어에서 보이는 설명 |
| `argument-hint` | 명령어 입력할 때 힌트로 표시 |
| `allowed-tools` | 이 명령어에서 허용할 도구 지정 (매번 권한 확인 생략) |
| `model` | 사용할 모델 지정 (`haiku` / `sonnet` / `opus`) |

---

## 5. 예시 명령어 모음

### `/풀스택생성`

```markdown
---
description: React + Node.js 풀스택 앱 생성
argument-hint: <프로젝트 설명>
---

$ARGUMENTS 를 기반으로 풀스택 프로젝트를 생성해줘.
- React (Vite + TypeScript) + Node.js (Express + TypeScript)
- 폴더구조, package.json 포함
- npm install && npm run dev 로 바로 실행 가능하게
```

**사용:**
```
/풀스택생성 쇼핑몰 MVP. 상품목록, 장바구니, 주문 기능.
```

---

### `/코드리뷰`

```markdown
---
description: 현재 코드베이스 리뷰
allowed-tools: Read, Glob, Grep
---

현재 프로젝트의 코드를 리뷰해줘.
- 버그 가능성
- 성능 이슈
- 보안 취약점
- 개선 제안
순서로 정리해줘.
```

**사용:**
```
/코드리뷰
```

---

### `/배포`

```markdown
---
description: 프로덕션 배포 실행
argument-hint: [web|api|all]
allowed-tools: Bash
---

$ARGUMENTS 타겟을 배포해줘.
배포 전 변경사항 확인하고, 문제 없으면 배포 진행.
배포 후 상태 확인까지.
```

**사용:**
```
/배포 web
/배포 all
```

---

### `/커밋`

```markdown
---
description: 변경사항 분석 후 커밋 메시지 생성 및 커밋
allowed-tools: Bash
---

현재 변경된 파일을 분석하고 적절한 커밋 메시지를 생성해서 커밋해줘.
- git diff로 변경사항 파악
- 컨벤셔널 커밋 형식 사용 (feat/fix/refactor/docs 등)
- 한국어로 작성
```

**사용:**
```
/커밋
```

---

## 6. Skills vs Commands 차이

| 구분 | Commands | Skills |
|------|----------|--------|
| 호출 방식 | 사용자가 `/명령어`로 직접 호출 | Claude가 상황 보고 자동 실행 |
| 파일 위치 | `.claude/commands/이름.md` | `.claude/skills/이름/SKILL.md` |
| 용도 | 반복 작업 자동화 | Claude 동작 방식 가이드 |
| 추천 상황 | "이 작업을 자주 한다" | "이 상황에선 항상 이렇게 해줘" |

---

## 바로 써보기

```bash
# 1. 글로벌 commands 폴더 생성
mkdir -p ~/.claude/commands

# 2. 예시 명령어 파일 생성
curl -o ~/.claude/commands/풀스택생성.md \
  https://raw.githubusercontent.com/junsungkim-lab/claude_skills/main/examples/풀스택생성.md

# 3. Claude Code 열고 사용
# /풀스택생성 내 프로젝트 설명
```

---

## 기여 & 공유

유용한 명령어가 있다면 PR 보내주세요!
이 레포를 ⭐ Star 하면 새로운 명령어 업데이트 알림을 받을 수 있어요.
