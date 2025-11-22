# Gemini CLI

## 1. 설치

```bash
# Gemini CLI 설치
npm install -g @google/gemini-cli

# Gemini CLI 접속
gemini
```
<br/>

## 2. 기본 터미널 명령어

 - __기본 도움말 및 사용 관련__
    - `/help`: 도움말
    - `/about`: 버전 정보 출력
    - `/docs`: 브라우저에서 Gemini CLI 문서 열기
    - `/auth`: 인증 방식 변경
 - __대화 이력 관련__
    - `/chat`: 대화 관리
        - `/chat list`: 대화 목록 출력
        - `/chat save <tag>`: 현재 대화를 체크포인트로 저장
        - `/chat resume <tag>`: 저장된 체크포인트 불러오기
        - `/chat delete <tag>`: 체크포인트 삭제
        - `/chat share <file>`: 현재 대화를 마크다운 또는 JSON 파일로 저장
    - `/clear`: 대화 히스토리 전체 초기화
    - `/compress`: 대화 내용을 요약해 대화 크기를 줄임
    - `/copy`: 마지막 결과 또는 코드를 클립보드에 복사
 - __워크스페이스 관련__
    - `/directory`: 워크스페이스 디렉토리 관리
        - `/directory add`: 디렉토리 추가 (/directory add dir1,dir2 식으로 여러 개 가능)
        - `/directory show`: 워크스페이스에 등록된 모든 디렉터리 표시
    - `/init`: 현재 프로젝트 분석 후 GEMINI.md 자동 생성
 - __MCP(Model Context Protocol) 관련__
    - `/mcp`: MCP 관련
        - `/mcp list`: MCP 서버 목록 출력
        - `/mcp desc`: MCP 서버 목록과 설명 출력
        - `/mcp schema`: MCP 서버 스키마 출력
        - `/mcp auth`: OAuth 기반 MCP 서버 인증
        - `/mcp refresh`

<br/>

## 3. 기본 키보드 단축키

 - `Ctrl + C`: CLI 종료
 - `Ctrl + Enter`: 새 줄 입력
 - `Ctrl + L`: 화면 지우기
 - `Ctrl + S`: 선택 모드(복사) 시작
 - `Ctrl + X`: 외부 에디터 열기 (해당 에디터에서 입력할 내용을 적으면 복사된다.)
 - `Ctrl + Y`: YOLO 모드 전환
    - YOLO 모드는 작업시 권한을 묻지 않고, 중단 없이 실행하게 해준다.
 - `ESC`: 명령 취소 / 입력창 초기화
