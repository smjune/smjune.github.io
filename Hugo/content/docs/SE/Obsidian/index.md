---
title: Obsidian
description: Obsidian 활용법
date: 2025-04-12T09:22:14+09:00
draft: false
---
## Obsidian + Github + Hugo

**1. Obsidian 기본 정보 (웹 검색 기반):**  

*   **로컬 저장:** 데이터가 사용자 기기에 직접 저장되어 데이터 소유권과 프라이버시 보장.
*   **Live Preview**: Source 형태 edit ( VScode) 가 아닌 문서 형태로 edit (Scrivener)가능
*   **마크다운 기반:** 표준 마크다운 문법 사용.
*   **양방향 링크 (백링크):** 노트 간 연결을 통해 아이디어를 네트워크처럼 구성.
*   **그래프 뷰:** 노트 연결 관계 시각화.
*   **플러그인:** 다양한 커뮤니티 플러그인을 통한 기능 확장. (예: git, copilot, smart compose ...)

**2. 일반적인 Obsidian 사용 시 장점:**

*   **데이터 완전 통제:** 클라우드 종속성 및 위험 회피. (로컬저장)
*   **유연성/확장성:** 표준 마크다운 호환성, 플러그인을 통한 맞춤 설정.
*   **지식 연결:** 아이디어 관계 발견 및 지식 구조화 용이 (예: 제텔카스텐).
*   **오프라인 작업:** 인터넷 연결 없이 사용 가능.

**3. 일반적인 Obsidian 사용 시 단점:**

*   **학습 곡선:** 기능, 플러그인, 마크다운 적응 시간 필요.
*   **동기화 설정:** 여러 기기 사용 시 직접 동기화 솔루션 설정 필요 (유료 Obsidian Sync 또는 외부 서비스).
*   **모바일 기능 제한:** 데스크톱 대비 기능 제한 가능성.
*   **협업 기능 부족:** 기본적으로 개인용 앱.

**4. 사용자 Vault 분석 (`smjune.github.io`):**

*   Steps : Obsidian 에서 마크다운 글 작성 -> Hugo server 로 로컬에서  Publish 확인 ->  GitHub Repository Push -> Github actions: Hugo -> 웹사이트 (Github Pages) 게시  방식으로 추정됩니다.

**5. 사용자 Vault 활용 방식의 장점:**

*   **통합 워크플로우:** 콘텐츠 생성부터 발행까지 효율적 관리.
*   **버전 관리:** Git으로 콘텐츠 변경 이력 관리 및 복구 용이.
*   **무료 배포/호스팅:** Hugo/GitHub Pages 활용. (cf.[정식 Published site](https://publish.obsidian.md/help-ko/%ED%99%88))  

**6. 사용자 Vault 활용 방식의 단점 (일반 Obsidian 사용 비교):**

*   **지식 연결 기능 활용 제한:** 웹사이트 발행 목적에 치중하여 개인 지식 연결/탐색 기능 활용 저하 가능성.
*   **민감 정보 관리 주의:** 공개될 수 있는 GitHub 저장소 특성상 비공개 정보 관리에 주의 필요 (`.gitignore` 등).
*   **동기화 복잡성:** Git 기반 동기화 시 충돌 해결 및 모바일 사용 불편 가능성.
*   **Obsidian 고유 기능 활용 저하:** 웹사이트 관리 위주로 플러그인 활용이 제한될 수 있음.
*   **Template** : 배포를 위해 Hugo front matter 과 Themes format 을 유지해야 함.

**7. 더 생각해 볼것:**

Obsidian의 핵심인 **개인 지식 연결 기능 활용을 제한**할 수 있고,  **Git 동기화 및 민감 정보 관리**에 신경 써야 하는 단점이 있다.

따라서, obsidian/github/hugo 간 구조을 잘 설정해야 한다. 

## 구성방식

- git, Obsidian, Hugo 가 모두 한 폴더에 설정, 
```bash
. my_project            # git, Obsidian vault, Hugo project
├── .git 
├── .obsidian 
├── hugo.yml 
├── content/posts             # publish folder
├── no_publish_folder 
└── no_sync_folder            #.gitignore
```

- git 과 Obsidian Vault 가 설정된 하위 폴더로 hugo project (publish 대상 폴더) 와 no_publish 폴더를 구분하여 hugo project 는 hugo 에서 정의한 방식으로  폴더를 구성하고, no_publish 는 일반적인 obsidian 폴더를 구성
```bash
. my_project                # git, Obsidian vault
├── .git 
├── .obsidian 
├── publish_folder/         # Hugo Project
│   ├── hugo.yml 
│   └── content/posts 
├── no_publish_folder 
└── no_sync_folder          #.gitignore
```

- Obsidain 하위에 sync/publish 할 메모 대상으로 만 git 설정 
```bash
. my_project                 # Obsidian vault
├── .obsidian 
├── sync_publish_folder/     # git, Hugo project
│   ├── .git 
│   ├── hugo.yml 
│   └── content/posts 
└── no_sync_publish_folder
//
. my_project                           # Obsidian vault
├── .obsidian 
├── sync_publish_folder/               # git project
│   ├── .git 
│   ├── publish_folder/                # Hugo project
│   │  ├── hugo.yml 
│   │  └── content/posts 
│   └── no_publish_folder 
└── no_sync_folderr 
```

- git 하위에 Obsidian 과 Hugo 을 구성하여, Publish 을 위해  Hugo 구성할때 VSCode 을 사용하여 obsidian vault 에 있는 메모를 content/posts 으로 복사한다.
```bash
. my_project                     # git project
└── .git/ 
├── Obsidian_Valut/                    # Obsidian Vault
│   ├── .obsidian 
│   ├── syn_folder 
│   └── no_syn_folder (.gitignore) 
└── Hugo_project /                     # Hugo project
    ├── hugo.yml 
    └── content/posts
```

### 사용하고 있는 구조
```bash
. smjune.github.io               # git, Obsidian vault
├── .git 
├── .obsidian 
├── Hugo/                        # Hugo Project
│   ├── hugo.yml 
│   └── content                  # published 
│        ├── docs 
│        └── posts 
├── Source                       # sync but not yet publish
└── Local                        #.gitignore
```
- 주의할 점 :   
1. Hugo 관련 명령어는 Hugo 폴더로 이동하여 수행한다. (gh-pages.yml(workflow) 에서 주의할것)   
2. Hugo 로 이동하는 md 는 Hugo themes 에 맞는 front matter 을 갖추어야 한다.
   이를 위해 사전에 template 을 정의 하고, obsidian 의 insert template 을 사용한다. 
```yml
---
title: "{{Title}}" 
description: 
date: "{{date:YYYY-MM-DD}}T{{time:HH:mm:ss}}+09:00" 
draft: true
---
```

## [Community Plug-In](https://obsidian.md/plugins)

> 활용법: AI Plug-In 인 SmartComposer 로 gemini-20-flash-thinking 으로 관련 내용을 생성 

**SmartComposer output (gemini-20-flash-thinking)**
- **Git:** Obsidian Vault를 Git 저장소로 만들어 버전 관리 및 GitHub 등과의 동기화를 가능하게 합니다. `.git` 폴더를 Obsidian Vault 안에 생성하여 Git 명령어를 Obsidian 내에서 실행하거나 외부 Git 도구와 연동할 수 있습니다. 이를 통해 노트 변경 이력 관리, 협업, 백업 등에 유용하게 활용됩니다.
- **Templater:** 템플릿 기능을 제공하여, 노트 작성 시 미리 정의된 템플릿을 불러와 빠르게 내용을 채울 수 있게 합니다. 날짜, 제목, 사용자 정의 변수 등을 템플릿에 활용하여 생산성을 높이고, 반복적인 문서 양식을 효율적으로 관리할 수 있습니다. 코드 스니펫, frontmatter, 정형화된 보고서 등에 유용합니다.
- **Copilot:** OpenAI Codex 모델 기반으로 코드 및 텍스트 자동 완성 기능을 제공합니다. Obsidian에서 글을 쓸 때 문맥을 파악하여 자연스러운 문장 완성을 돕고, 코드 작성 시에도 자동 완성 및 추천 기능을 제공하여 생산성을 향상시킵니다. 아이디어 구상, 초안 작성, 코드 작성 등 다양한 상황에서 활용 가능합니다.
- **Smart Composer:** 노트 작성을 위한 다양한 편집 기능을 제공합니다. 문장 병합, 분할, 순서 변경, 스타일 변경 등 고급 편집 기능을 통해 글쓰기 흐름을 개선하고 효율적인 문서 작성을 지원합니다. 긴 문서를 다듬거나, 아이디어를 구조화하고 재구성할 때 유용합니다.

> Cursor 결과와 비교 

**Cursor output (sequential thinking, brave-search)**
- **Git:**
    - Obsidian 노트 저장소를 Git으로 버전 관리합니다.
    - 자동 커밋 및 동기화 기능을 제공하여 백업 및 협업을 용이하게 합니다.
    - 변경 이력을 추적하고 이전 버전으로 복구할 수 있습니다.
    - GitHub, GitLab 등 다양한 Git 호스팅 서비스와 연동 가능합니다.
- **Templater:**
    - 노트 작성을 자동화하는 강력한 템플릿 플러그인입니다.
    - 변수, 함수, JavaScript 코드를 사용하여 동적인 템플릿을 만들 수 있습니다.
    - 반복적인 작업을 줄이고 일관된 형식의 노트를 생성하는 데 유용합니다.
    - 날짜, 시간, 파일 정보 등 다양한 내장 변수와 함수를 제공합니다.
- **Copilot:**
    - AI 기반 글쓰기 보조 플러그인입니다.
    - 노트 내용 요약, 아이디어 생성, 문장 완성 등 다양한 AI 기능을 제공합니다.
    - OpenAI 등 여러 LLM 모델을 지원하며, Vault 내 노트를 기반으로 답변을 생성할 수 있습니다. (Vault QA 모드)
    - 개인 정보 보호에 중점을 둔 AI 어시스턴트입니다.
- **Smart Composer:**
    - AI 기반의 맥락 인식 글쓰기 보조 플러그인입니다.
    - Cursor AI와 유사하게, Vault 내 특정 파일이나 폴더를 참조하여 대화하고 편집 제안을 받습니다.
    - AI가 제안한 내용을 클릭 한 번으로 적용할 수 있습니다.
    - Vault 내용 기반 대화, 시맨틱 검색, 로컬 모델 지원 등의 기능을 제공합니다.
    - 최근 Gemini 모델 및 이미지 지원이 추가되었습니다.