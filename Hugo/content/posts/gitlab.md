---
title: "Gitlab"
date: 2023-02-06T20:28:27+09:00

---

# GitLab 으로 Deploy 하기  

github 에 deploy 했던 hugo project 을 git remote 만 추가하서 gitlab repo 에 push 하고,  
gitlab CI/CD 을 이용하여 build, deploy 하는 방법  

> 이미 github 에서 main 이라는 브랜치명을 사용했으므로, gitlab 에서는 다른 이름을 사용하여야 함.  


## gitlab.com/smjune/smjune.io 만들기  

```bash
$ cd 'exiting git project'
$ git remote add gitlab https://gitlab.com/smjune/smjune.gitlab.io/
$ git branch -M gitlabmain  
$ git push -uf gitlab gitlabmain
# 현재 checkout 한 브랜치를 gitlabmain 으로 변경하고, 이것을 gitlab 리모트와 연결
# 나중에 main 을 다시 github remote 와 연결해주어야 함.
$ git checkout -b main smjune/main     # github 에서 main 이란 브랜치명 사용
$ git branch
  labmain
* main  
```
현재 로컬 상황을 정리하자면,  
main 브랜치와 gitlabmain 이 동일하고, 각각 자신의 리모트에 연결되어 있음  
> gitlabmain, gitlab/gitlabmain   # gitlab 용  
> main, smjune/main               # github 용

작업 순서는 
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
 

## Gitlab CI/CD 구성

