---
title: "Gitlab"
date: 2023-02-06T20:28:27+09:00

---

# GitLab 으로 Deploy 하기  

github 에 deploy 했던 hugo project 을 git remote 만 추가하서 gitlab repo 에 push 하고,  
gitlab CI/CD 을 이용하여 build, deploy 하는 방법  

> 이미 github 에서 main 이라는 브랜치명을 사용했으므로, gitlab 에서는 다른 이름(labmain)을 사용하여야 함.  


## gitlab.com/smjune/smjune.io 만들기  

```bash
$ cd 'exiting git project'
$ git remote add gitlab https://gitlab.com/smjune/smjune.gitlab.io/
# origin 이란 이름 대신 gitlab 이란 이름으로 remote을 설정
$ git branch -M labmain  
$ git push -uf gitlab labmain
# 현재 checkout 한 브랜치를 labmain 으로 변경하고, 이것을 gitlab 리모트와 연결
# 나중에 main 을 다시 github remote 와 연결해주어야 함.
$ git checkout -b main smjune/main     # github 에서 main 이란 브랜치명 사용
$ git branch
  labmain
* main  
```

## gitlab 에서 main 브랜치를 다시 만들기
---

1. gitlab WEB 에서 main (474dbe7)을 삭제, labmain 을 기준으로 main 을 다시 만든다.   
```bash
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ git branch -avv
* labmain                 bcb809a [gitlab/labmain] change name of .gitlab-ci
  main                    bcb809a [github/main] change name of .gitlab-ci
  remotes/gitlab/labmain  bcb809a change name of .gitlab-ci
  remotes/gitlab/main     474dbe7 Initial commit

```
2. 로컬 fetch 후, labmain 을 gitlab/main 과 연결한다.  
```bash
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ git fetch gitlab
From https://gitlab.com/smjune/smjune.gitlab.io
 + 474dbe7...bcb809a main       -> gitlab/main  (forced update)
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ git branch -avv
* labmain                 bcb809a [gitlab/labmain] change name of .gitlab-ci
  main                    bcb809a [github/main] change name of .gitlab-ci
  remotes/gitlab/labmain  bcb809a change name of .gitlab-ci
  remotes/gitlab/main     bcb809a change name of .gitlab-ci
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ git branch -u gitlab/main labmain
branch 'labmain' set up to track 'gitlab/main'.
myoungjune-sung-ui-iMac:Hello_world myoungjunesung$ git branch -avv
* labmain                 bcb809a [gitlab/main] change name of .gitlab-ci
  main                    bcb809a [github/main] change name of .gitlab-ci
  remotes/gitlab/labmain  bcb809a change name of .gitlab-ci
  remotes/gitlab/main     bcb809a change name of .gitlab-ci
```
/* WEB 에서 labmain 도 삭제 */

## NOTE 현재 로컬 상황을 정리하자면, 
---
main 브랜치와 labmain 이 동일하고 (bcb809a), 각각 자신의 리모트에 연결되어 있음   
labmain                 bcb809a [gitlab/main] change name of .gitlab-ci  
main                    bcb809a [github/main] change name of .gitlab-ci  
> labmain,    gitlab/main   # gitlab 용 (gitlab 은 remote 이름, labmain 는 브랜치 이름)  
> main,       github/main   # github 용 (github 는 remote 이름, main 는 브랜치 이름)  

이후 작업 순서는 
1. update main branch 
2. checkout gitlabmain
3. merge main

```bash
$ git checkout labmain
M       Hugo/content/posts/gitlab.md
Switched to branch 'labmain'
Your branch is up to date with 'gitlab/labmain'.
$ git merge main
Updating 5487806..11711a6
Fast-forward
 .github/workflows/gh-pages.yml | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
 ```

## Gitlab CI/CD 구성

1. gilab CI/CD 을 사용하려면 credit card로 인증해야 함.
> Pipeline failing? To keep GitLab spam and abuse free we ask that you verify your identity.  
> Until then, shared runners will be unavailable. Validate your account or use your own runners
.
2. github 용 config.toml 지우고 config_gitlab.toml 을 config.tolml 으로 복사
3. project root 가 아닌 hugo 폴더에 이동 하여 빌드해야 함.
4. hugo/public 을 deploy 해야함.