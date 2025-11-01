# Claude Code 

## 1. 설치 및 기본 설명

### 1-1. Claude Code 설치

 - `Mac 환경`
```bash
# Homebrew 설치
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 환경 변수 등록
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# Git 설치
brew install git

# Node 설치
brew install node
```

 - Git, Node가 설치되어야 한다.
```bash
# 설치
npm install -g @anthropic-ai/claude-code

# 설치 확인
claude --version

# 프로젝트 초기화
claude
/login
$ /init
```
<br/>

### 1-2. 권한 모드

Claude가 파일을 수정하거나 빌드 명령을 실행하기 전, 이 모드가 동작한다.

 - __plan__
    - 실행 대신 계획만 보여줌
    - “이 코드를 이렇게 바꿀게요” 수준
 - __ask__
    - 실행 전마다 사용자 승인 요청
    - 기본 안전 모드
 - __auto__
    - Claude가 자동으로 실행
    - 반복 빌드나 파일 수정 루프 시 유용

<br/>

## 2. 터미널

 - __작업__
    - `Ctrl + C`: 현재 입력 중이거나 생성 중인 작업을 취소
    - `Ctrl + D`: 세션 종료
    - `Esc + Esc`: 직전에 보낸 메시지를 수정(edit) 할 수 있는 모드로 전환
    - `Shift + Tab`: 권한 모드(permission mode) 변경 (기본, Auto-Accept, Plan)
 - __커서 이동__
    - `Ctrl + A`: 커서를 줄 맨 앞으로 이동
    - `Ctrl + E`: 커서를 줄 맨 끝으로 이동
    - `Alt + B` 또는 `Ctrl + <`: 이전 단어로 이동
    - `Alt + F` 또는 `Ctrl + >`: 다음 단어로 이동
 - __삭제 / 잘라내기 / 붙여넣기__
    - `Ctrl + U`: 커서 앞쪽 전체 삭제 (잘라내기)
    - `Ctrl + K`: 커서 뒤쪽 전체 삭제 (잘라내기)
    - `Ctrl + W`: 커서 앞쪽 한 단어 삭제
    - `Alt + D`: 커서 뒤쪽 한 단어 삭제
    - `Ctrl + Y`: 마지막 잘라낸 내용 붙여넣기 (yank)
    - `Ctrl + H`: 백스페이스 (한 글자 삭제)
    - `Ctrl + D`: 커서 위치의 글자 삭제 (Delete) / 입력이 비었을 경우 세션 종료
 - __편집 / 탐색 / 실행 제어__
    - `Ctrl + L`: 터미널 화면 클리어 (Claude Code 상태 유지됨)
    - `Ctrl + R`: 히스토리 검색 (이전 명령어 빠르게 검색)
    - `Ctrl + G`: 히스토리 검색 취소 / 나가기
    - `Ctrl + P` 또는 `Ctrl +N`: 이전 / 다음 명령으로 이동 (↑ ↓ 과 동일)
    - `Ctrl + C`: 현재 입력 또는 실행 중인 작업 취소
    - `Ctrl + Z`: 현재 작업을 백그라운드로 일시 `중지
    - `fg`: Ctrl+Z로 중지한 작업을 포그라운드로 복귀
    - `!!`: 직전 명령 재실행
    - `!abc`: abc로 시작하는 이전 명령 재실행

<br/>

## 3. 명령어

 - __터미널 실행__
    - `claude`: 대화형 REPL 모드로 시작
    - `claude "query"`: 질문을 던지면서 시작
    - `claude -p "query"`: print 모드로 실행하고 REPL을 종료 (스크립트나 파이프라인에 유용)
    - `cat file | claude -p "query"`: 파일 내용을 Claude에게 파이프해서 질문
    - `claude update`: 최신 버전으로 업데이트
 - __권한(퍼미션) 관련__
    - Claude Code는 파일 편집, 빌드, 실행 등은 “Permission Mode”로 제어된다.
    - `/mode plan`: Claude가 명령 실행 전에 계획만 설명
    - `/mode auto`: Claude가 자동으로 명령 실행 (자동 승인 모드)
    - `/mode ask`: 실행 전마다 승인 여부 물어봄 (기본값)
    - `Shift + Tab`: 모드 전환 단축키 (plan → auto → ask 순환)
    - `/permissions`: 현재 허용된 디렉토리/명령 목록 표시
 - __기본 명령어__
    - `/help`: 사용 가능한 모든 Slash 명령어를 출력
    - `/clear`: 현재 대화 맥락(context)과 히스토리 초기화
    - `/resume`: 특정 세션 ID를 불러와서 이어서 대화
    - `/compact`: 현재 맥락 중 불필요한 부분 정리 (Claude가 자동으로 중요 맥락만 유지)
    - `/status`: 현재 세션 상태 및 권한 모드(plan/auto 등) 표시
    - `/memory`: Claude의 기억(memory) 상태 표시
    - `/forget`: 특정 기억 또는 전체 기억 삭제
    - `/edit`: 직전 프롬프트 수정 (Esc 두 번 눌러도 진입 가능)
    - `/vim`: 내부 vim 편집기 모드로 전환 (설정 필요)
    - `/terminal-setup`: 줄바꿈/단축키 설정을 OS 터미널 환경에 맞게 구성
    - `/reload`: 현재 설정 및 프로젝트 파일 다시 로드
    - `/sandbox`: Claude의 코드 실행 환경(격리 환경) 정보 확인
 - __파일 및 프로젝트 관련__
    - `/add-dir <path>`: Claude가 접근할 수 있는 폴더 추가
    - `/remove-dir <path>`: 접근 가능 폴더 제거
    - `/project`: 현재 프로젝트 상태 및 인덱싱 상태 표시
    - `/analyze`: Claude에게 현재 디렉토리의 코드 구조 분석 요청
    - `/index`: Claude가 새로 추가된 파일/디렉토리를 인덱싱하도록 요청
 - __Shell 명령어 사용__
    - Claude Code는 !로 시작하는 입력을 직접 시스템 셸 명령으로 실행한다.
    - `!ls`, `!dir`: 현재 디렉터리 파일 목록 출력
    - `!pwd`: 현재 작업 디렉터리 경로 표시
    - `!cd <path>`: 디렉터리 이동
    - `!cat <file>`: 파일 내용 보기
    - `!code <file>`: 해당 파일을 Claude 편집기로 연다.
    - `!git status`, `!git diff`: git 명령어 그대로 사용 가능
    - `!npm run dev`, `!gradle build`: 실제 로컬 빌드 명령 실행 가능
    - `!!`: 직전 ! 명령 재실행
    - `!history`: 최근에 실행한 ! 명령어 히스토리 보기

<br/>

## 4. 사용 예시

### 4-1. 주요 명령어

 - __프로젝트 초기 세팅 관련__
    - `/init`
        - 현재 디렉터리를 Claude 프로젝트로 초기화하고 CLAUDE.md 파일을 생성
        - 프로젝트 첫 세팅 시 반드시 1회 실행. CLAUDE.md 안에 프로젝트 개요·기술스택·컨벤션 작성
    - `/add-dir <path>`
        - Claude가 접근할 수 있는 폴더 추가
        - 예: /add-dir src → src 디렉토리의 파일을 Claude가 읽고 편집 가능
    - `/remove-dir <path>`
        - Claude 접근 제거
        - 보안·비공개 디렉토리 제외할 때 사용
    - `/project`
        - 현재 프로젝트와 Claude 인덱싱 상태 확인
        - Claude가 어떤 파일들을 인식하고 있는지 점검용
 - __코드 작성 & 편집 관련__
    - `!ls`, `!cat`, `!code <file>`
        - 파일 목록 / 내용 보기 / Claude 편집기로 열기
        - !code src/App.java → Claude가 직접 코드 열고 수정 제안
    - `/edit`
        - 직전 입력 프롬프트 수정
        - Esc 두 번 눌러도 동일 (입력 중 빠르게 수정할 때 편함)
    - `/analyze`
        - Claude에게 현재 프로젝트 코드 구조를 분석시킴
        - 새로 가져온 레포지토리일 때 전체 파악용
    - `/compact`
        - 대화 맥락 정리 — 불필요한 정보 삭제
        - 긴 세션에서 Claude가 느려질 때 가볍게 리셋
 - __실행 & 자동화 관련__
    - `!<command>`
        - 실제 시스템 셸 명령 실행
        - 예: `!npm run dev`, `!gradle build`, `!pytest tests`
    - `Shift + Tab`
        - 모드 순환 단축키
        - `plan → ask → auto → plan` 순환
    - `/status`
        - 현재 모드, 세션 상태, 모델, 메모리 확인
        - 실행 전 Claude 상태 점검용
 - __맥락 및 기억 관리__
    - `/memory`
        - Claude가 기억 중인 항목 조회 (CLAUDE.md, 최근 작업 등)
        - 어떤 정보가 맥락으로 유지되는지 확인
        - `/forget [키워드]`
            - 특정 기억 삭제
            - 오래된 규칙이나 설정 제거 시
        - `/clear`
            - 현재 대화 맥락 리셋 (세션은 유지)
            - Claude가 “이전 내용”을 계속 기억해서 혼동할 때 사용
        - `/resume <id>`
            - 특정 세션 재개
            - 이전 프로젝트 세션 이어서 작업할 때 유용
 - __설정 및 버전 관리__
    - `/config`
        - 현재 설정 확인 (~/.claude/config.yaml)
        - 모델 버전, 권한 모드, 기본 디렉토리 등 확인
    - `/models`
        - 사용 가능한 Claude 모델 목록 보기
        - 예: claude-sonnet-4, claude-haiku-3, claude-opus 등
    - `/update`
        - Claude CLI 업데이트
        - 주기적으로 실행 (새 명령어 반영용)
    - `/version`
        - CLI와 모델 버전 출력
        - 디버깅 시 “현재 버전” 명시할 때 유용

```bash
# 첫 프로젝트 세팅
claude
/init
/add-dir src
/project

# 구조 분석 후 리팩토링
/analyze
/mode ask
!code src/main/java/com/example/service/UserService.java

# 반복 빌드 테스트
/mode auto
!gradle build
!java -jar build/libs/app.jar

# 세션 정리
/compact
/clear
```
