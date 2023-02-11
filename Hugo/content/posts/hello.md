---
title: "Hello GitHub"
date: 2023-02-05T10:22:18+09:00

---

# github 에서 블로그 만들기 

hugo 로컬 빌드를 해서 public 을 submodule 으로 다른 repo 에 push 하는 방식 대신
github action 을 이용하여 1개 repo에서 main 을 빌드 후 gh-pages 브랜치로 deploy 하는 방식 사용  



- Project Settings | Pages | Build and Deploy | branches : gh-pages 설정  
- 로컬에서는 'hugo server' 을 이용하여 확인 후 push 함 

해당 github pages 을 만든 이력정리 **(아래 관련 지식 보유 가정)**  
```
* 기본 적인 SSG (Static Site Generator) 관련 정보  
* brew, git, github, hugo 설치 및 사용 방법 (Hugo 는 windows 지원)  
```  
---  

## Hugo (SSG)  
* [https://gohugo.io/documentation/](https://gohugo.io/documentation/)  

    1. $ hugo new site [hugo project name] 으로 프로젝트 생성.  
    2. config.toml : baseURL, Title 과 Theme 을 수정.  
    3. themes : 사용할 Web theme 을 설치. ( git submodule 사용 )  
    4. content : 폴더/파일.md 형태로 글 작성 및 구성. ( $ hugo new posts/hello.md )  
    5. hugo server 으로 로컬 호스트 페이지 확인 ( md 파일에 draft : true 인 경우 -D 옵션 필요)
    6. hugo server 가 실행 중이면, 저장하는 수정 내용이 바로 로컬 호스트 페이지에 반영됨

## github pages 만들기 
https://docs.github.com/en/pages/  

### github pages 종류
~~~
 1. 개인 github Pages
 2. 프로젝트 github Pages
~~~

---

### 1. 개인 Page (Blog) : UserAccont.github.io

* Base URL : https://UserAccount.github.io/
* Repo 주소 : https://github.com/UserAccount/UserAccount.github.io.git
    * 해당 repo 는 pages 을 위한 repo 이므로 hugo project = git project 으로 생성한다. 

    ```bash
    $ hugo new site hugo_project
    $ cd hugo_project
    $ git init
    $ git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
    $ echo "theme = 'ananke'" >> config.toml
       // edit BaseURL and title
    $ hugo new posts/sample.md
       // edit sample.md
    $ hugo server
       // Be sure it works. if not, correct it
    $ git remote add origin https://github.com/UserAccount/UserAccount.github.io.git
    $ git add .
    $ git commit -m 'initiate project'
    $ git push origin master
    // browse https://UserAccount.github.io/  
    ```


* 폴더 구조  

> hugo project 을 git (github) 로 관리한다고 생각하면 된다.  
> project root 에서 hugo 와 git 명령어를 사용할 수 있다.  
```text
project folder (git, hugo)
 ├─.git
 ├─.gitmodules
 ├─.github
 │  └─workflows
 │     └─gh-pages.yml
 ├─congif.toml
 ├─themes
 │  └─themes folder (submodule)
 ├─content
 │  ├─posts
 │  │  ├─main.md
 │  │  └─...
 │  └─...
 ├─...
 └─readme.md

```  
*Created from https://arthursonzogni.com/Diagon/#Tree*  

---  

### 2. 프로젝트 Page (Blog) UserAccont.github.io/Project

* Base URL : https://UserAccount.github.io/Project
* Repo 주소 : https://github.com/UserAcount/Project.git
    * 해당 repo 는 git 프로젝트 안에 source code 와 hugo 을 포함한다.  


    ```bash
    // 기존 git project 에서 
    $ hugo new site hugo
    $ cd hugo_project
    $ git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
    $ echo "theme = 'ananke'" >> config.toml
       // edit BaseURL and title
    $ hugo new posts/sample.md
       // edit sample.md
    $ hugo server
       // Be sure it works. if not, correct it
    $ cd ..
    $ git add .
    $ git commit -m 'initiate project'
    $ git push origin master
    // browse https://UserAccount.github.io/Project
    ```  

* 폴더 구조

>  프로젝트의 main branch 기본구조는 아래와 같이 구성된다.  
>  프로젝트는 source code folder와 hugo 폴더를 갖는다.  
>  따라서 git 명령어는 project root 에서, hugo 명령어는 hugo 폴더로 이동후 사용한다.  
>  pages 을 deploy 하는 github action 은 .github/workflows/gh-pages.yml 이다.  
>  hugo folder 는 ' $ hugo new site hugo ' 로 생성한다.  
>  theme 는 ' $ git submodule add [submoduel.git] themes/[theme name] '  
>  각 page 는 ' $ hugo new xxx/xxx.md ' 로 생성한다.  
>  프로젝트 gh-pages 브랜치는 hugo 가 빌드된 Web Site (html) 만 존재한다.


```text
project folder (git)
 ├─.git
 ├─.gitmodules
 ├─.github
 │  └─workflows
 │     └─gh-pages.yml
 ├─Source Code folder
 │  ├─lib
 │  │  ├─utillib.lib
 │  │  └─...
 │  ├─build
 │  │  ├─.buildscript
 │  │  └─...
 │  ├─main.cpp
 │  └─...
 ├─hugo project folder (hugo)
 │  ├─congif.toml
 │  ├─themes
 │  │  └─themes folder (submodule)
 │  ├─content
 │  │  ├─posts
 │  │  │  ├─main.md
 │  │  │  └─...
 │  │  └─...
 │  └─...
 ├─...
 └─readme.md

```  
*Created from https://arthursonzogni.com/Diagon/#Tree*  

** _branch 으로 구분하는 방법도 생각해 보았으나, (main, hugo, gh-pages)_  
    _- main branch : soure code 파일 만 존재_  
    _- hugo branch : hugo project 파일만 존재_  
    _- gh-pasges branch : hugo build 결과 (html) 파일만 존재_  
    _동일한 수정에 대한 commit 을 main 브랜치 (source code 수정) 와_  
_hugo 브랜치 (page 수정 ) 에 각각 1번씩 총 2번을 수행해야 하므로 보류_  


---  
### 3. GitHub Actions to build and deploy the hugo project  

* .github/workflows/gh-pages.yml 생성

https://github.com/peaceiris/actions-gh-pages

- 여기서 주의 할 점  
> project page 인 경우  
    > hugo 프로젝트 가 하위로 설정 되어 있으므로 
    
    ...
    - name: Build
        run: |
          cd hugo_project                           // hugo 프로젝트로 이동
          hugo --minify
    - name: Deploy
        uses: peaceiris/actions-gh-pages@v.
        if: ${{ github.ref == 'refs/heads/main' }}  // branch 확인
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./hugu_project/public        // hugo project 하위 public 폴더 사용
    ...

---  

### 4. local branch and remote 

```bash
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ git branch -avv
  labmain                 bcb809a [gitlab/main] change name of .gitlab-ci
* main                    bcb809a [github/main] change name of .gitlab-ci
  remotes/github/gh-pages 309c2bd deploy: 41dfa412c2cd0ebdfd7675d7bd4604b8a07761bb
  remotes/github/main     bcb809a change name of .gitlab-ci
  remotes/gitlab/labmain  bcb809a change name of .gitlab-ci
  remotes/gitlab/main     bcb809a change name of .gitlab-ci
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ _
```  
*/labmain 과 gitlab/labmain 은 삭제/*

- main 은 remote 로 github (github.com/smjune/smjung.github.io) 의 main 브랜치를 트랙킹  
   - git push github main
- remote 로 gitlab (gitlab.com/smjune/smjune.gitlab.io) main 도 등록되어 있으므로  
   - git push gitlab main

```bash
myoungjune-sung-ui-iMac:hugo myoungjunesung$ git status
On branch main
Your branch is up to date with 'github/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   content/posts/gitlab.md

no changes added to commit (use "git add" and/or "git commit -a")
```
```bash
myoungjune-sung-ui-iMac:hugo myoungjunesung$ git add .
myoungjune-sung-ui-iMac:hugo myoungjunesung$ git commit -m 'update way to push'
[main d7c0db2] update way to push
 Committer: myoungjune sung <myoungjunesung@myoungjune-sung-ui-iMac.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 26 insertions(+), 1 deletion(-)
 ```
 ```bash
myoungjune-sung-ui-iMac:hugo myoungjunesung$ git push github main
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 2 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 1.11 KiB | 1.11 MiB/s, done.
Total 6 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To https://github.com/smjune/smjune.github.io.git
   2b0d320..d7c0db2  main -> main
```
```bash
myoungjune-sung-ui-iMac:hugo myoungjunesung$ git push gitlab main
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 2 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 1.11 KiB | 1.11 MiB/s, done.
Total 6 (delta 3), reused 0 (delta 0), pack-reused 0
To https://gitlab.com/smjune/smjune.gitlab.io.git
   2b0d320..d7c0db2  main -> main
```
```bash
myoungjune-sung-ui-iMac:hugo myoungjunesung$ git branch -avv
  labmain                 2b0d320 [gitlab/main: behind 1] add how to update github and gitlab
* main                    d7c0db2 [github/main] update way to push
  remotes/github/gh-pages 309c2bd deploy: 41dfa412c2cd0ebdfd7675d7bd4604b8a07761bb
  remotes/github/main     d7c0db2 update way to push
  remotes/gitlab/labmain  bcb809a change name of .gitlab-ci
  remotes/gitlab/main     d7c0db2 update way to push
myoungjune-sung-ui-iMac:hugo myoungjunesung$ 
``` 
