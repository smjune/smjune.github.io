---
title: "Hello"
date: 2023-02-05T10:22:18+09:00

---

# github 에서 블로그 만들기 

해당 github pages 을 만든 이력정리 **(아래 관련 지식 보유 가정)**
> 기본 적인 SSG (Static Site Generator) 관련 정보  
> brew, git, github, hugo 설치 및 사용 방법 (Hugo 는 windows 지원)

hugo 로컬 빌드를 해서 public 을 submodule 으로 다른 repo 에 push 하는 방식 대신
github action 을 이용하여 1개 repo에서 main 을 빌드 후 gh-pages 브랜치로 deploy 하는 방식 사용  
>Project Settings | Pages | Build and Deploy | branches : gh-pages  
>로컬에서는 'hugo server' 을 이용하여 확인 후 push 함  


## Hugo (SSG)



## github pages 만들기 

### github pages 종류
~~~
 1. 개인 github Page
 2. 프로젝트 github Page
~~~
### 1. 개인 Page (Blog) : UserAccont.github.io

* Base URL : https://UserAccount.github.io/
* Repo 주소 : https://github.com/UserAcount/UserAccount.github.io.git
    * 해당 repo 는 pages 을 위한 repo 이므로 git project = hugo project 으로 생성한다. 

### 2. 프로젝트 Page (Blog) UserAccont.github.io/Project

* Base URL : https://UserAccount.github.io/Project
* Repo 주소 : https://github.com/UserAcount/Project.git
    * 해당 repo 는 git 프로젝트 안에 source code 와 hugo 을 포함한다.
    
* project 구조

>  프로젝트의 main branch 기본구조는 아래와 같이 구성한다. 
>  프로젝트는 source code folder와 hugo 폴더를 갖는다.
>  pages 을 deploy 하는 github action 은 .github/workflows/gh-pages.yml 이다.
>  hugo folder 는 ' $ hugo new site hug ' 로 생성한다.
>  theme 는 ' $ git submodule add [submoduel.git] themes/[theme name] '
>  각 page 는 ' $ hugo new xxx/xxx.md ' 로 생성한다.

```text
project folder
    .git
    .github
        workflows
            gh-pages.yml
    .gitmodules
     Source Code folder
        main.cpp
        ...
    hugo project folder
        congif.toml
        themes
            themes folder
        content
            posts
                main.md
        ...
    readme.md

````
