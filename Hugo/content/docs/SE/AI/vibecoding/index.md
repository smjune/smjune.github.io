---
title: Vibe Coding
description: 
date: 2025-04-22T17:58:45+09:00
draft: false
---
## What is Vibe Coding

![Vibe Coding](vibecoding.png)

### Assembly, C/C++, Python

물리적인 자원을 더 쉽고, 싸게 사용함에 따라 프로그램밍 언어도 같이 변화 할 수 밖에 없다. 
물리적 리소스를 사용하는 컴파일시 더 많은 자원을 사용하고, 
코드를 작성하는것은 점점 자연어 (Pseudo code) 코드의 지시형태로 되어 간다.

0과 1의 기계어로 번역하는 것이 컴파일이라 하면, 자연어를 프로그래밍 syntax 로 변역해 주는 것은 뭐라 불러야 하나?

- Assembley: 
컴파일시 물리적 자원 사용은 적지만, 프로그래밍은 난해하다.   

```assembly
section .data
    filename db "test.txt", 0  ; 파일 이름
    content  db "test", 0      ; 쓸 내용
    content_len equ $ - content -1 ; 내용 길이 (NULL 문자 제외)

section .text
    global _start

_start:
    ; 파일을 생성하거나 열기 (sys_open)
    mov rax, 2          ; sys_open 시스템 콜 번호
    mov rdi, filename   ; 파일 이름 포인터
    mov rsi, 0101o      ; 플래그 (O_WRONLY | O_CREAT | O_TRUNC) - 쓰기 전용, 없으면 생성, 있으면 내용 삭제
    mov rdx, 0644o      ; 모드 (rw-r--r--)
    syscall             ; 시스템 콜 호출
    mov r12, rax        ; 파일 디스크립터를 r12에 저장 (오류 처리 안 함)

    ; 파일에 쓰기 (sys_write)
    mov rax, 1          ; sys_write 시스템 콜 번호
    mov rdi, r12        ; 파일 디스크립터
    mov rsi, content    ; 쓸 내용 포인터
    mov rdx, content_len ; 쓸 내용 길이
    syscall             ; 시스템 콜 호출

    ; 파일 닫기 (sys_close)
    mov rax, 3          ; sys_close 시스템 콜 번호
    mov rdi, r12        ; 파일 디스크립터
    syscall             ; 시스템 콜 호출

    ; 프로그램 종료 (sys_exit)
    mov rax, 60         ; sys_exit 시스템 콜 번호
    xor rdi, rdi        ; 종료 코드 0
    syscall             ; 시스템 콜 호출
```

- C/C++: 
아직까지 syntax 의 벽은 여전히 남아 있다.   

```C
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *fp;

    fp = fopen("test.txt", "w");
    if (fp == NULL) {
        perror("파일 열기 오류");
        return EXIT_FAILURE;
    }

    if (fputs("test", fp) == EOF) {
        perror("파일 쓰기 오류");
        fclose(fp);
        return EXIT_FAILURE;
    }

    fclose(fp);
    return EXIT_SUCCESS;
}
```

- python
쉽다고 해도, 일상언어는 아니다.   
```python
try:
    with open("test.txt", "w") as f:
        f.write("test")
except IOError as e:
    print(f"파일 쓰기 오류: {e}")
```

- Pseudocode: 
각 프로그래밍 언어의 syntax 보다 논리적인 구조가 더 중요하게 되었다.
```
파일 "test.txt"를 쓰기 모드로 연다.
만약 파일 열기에 실패하면, 오류를 출력하고 종료한다.
파일에 "test" 문자열을 쓴다.
파일을 닫는다.
```

- **vibe coding**: 
전체적인 context, prompt 등 LLM 적인 요소가 더 중요하게 되었다.  
``` test.txt 파일을 열어서 'text'쓰는 코드 작성해줘 ```


### Essence and Accident

- Pair programming with AI generating code ?
- Assembly 으로 코딩하던 사람이 C/C++ 으로 코딩하는 것을 보고 어떤 생각이 들었을까? 
	- C/C++ 을 사용하지만, Assembly 도 배움.
- 제품을 위한 코드 보다는 제품 코드를 테스트 하는 코드를 생산
	- 제품을 위한 코드는 의외로 매우 보수적임 (신기술을 적용하기 힘듬)
- 어떻게 내가 의도하는 코드를 LLM 이 생산하도록 만들것 인가?
	- agent, prompt, context aware, ... 
	- 
### Tools 

- Knowledge Management tool : Notion, Obsidian
- Access to an LLM : GPT, Claude, Gemini 
- AI Code Editor : Cursor, Windsurf
- IDE AI Extension : Continue, Cline, AutoPilot, Gemini Code Assist
- VCS : Git

## Pre-Vibe Coding Routine

### Ideation
	
- 당연히 구현하기 전에 계획은 중요하다. 
- Idea을 작성 지속적으로 구체화하고,
- 관련자료를 모으고 분류하고, 
- 정보들을 연결한다. 
- 이 모든걸 위해 Knowledge Management tool 이 필요함.

### Refs. Index

- Codebase indexing
- Online Refs. (e.g., Cursor|Docs)
	- Language Syntax Guide (e.g., Python)
	- Domain Knowledge (e.g., Scipy, Sklearn)
- Live Refs (e.g., MCP:Brave Search, context7)

### Persona (Template)

- User (e.g., Cursor|User rules)
- Project (e.g., Cursor|Project rules)
	- ...
- Product (e.g., Product Requiremet Document)
	- ...

## Harmonize with SDLC 

-  Design - Code - Test - Build - Deploy
- Iterative incremental , evolutionary 

### Design

- Project & Task management : taskmaster-ai
- PRD : Notion, Obsidian
- UI/UX : Figma 
- Diagram : UML, Mermaid
### Code 
 
- Choosing LLM Model
	- AI Code Editor, IDE AI Extentions, Chatbot 
	- Cloud vs Local (Open Source)
- Context-Aware
	- memory 
- Prompt Engineering
	- 잘통하는 prompt는 DB화 할것   
- Agentic Approch
	- Access to resource (e.g., [MCP](https://modelcontextprotocol.io/introduction)) 
	- Make a Agent (e.g., [ADK](https://google.github.io/adk-docs/))
	- Connect Agent to Agent (e.g., [A2A](https://github.com/google/A2A))
- Project Ochestration 
	- Managing Non-deterministic 
	- Restore checkpoint
- Human-In-The-Loop
	- AI 생산한 code 의 품질 확보 방안 

### Build

- Android Studio 
- XCode

### Deploy

- App
- WEB

## 추가 읽을거리

- [kakao AI blog](https://tech.kakao.com/posts/696)