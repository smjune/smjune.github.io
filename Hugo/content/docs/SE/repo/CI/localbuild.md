---
title: "Local build"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---

지금 하는 이야기는 주로 2000년 초반 처음 SW 개발 일을 시작하면서 겪은 일이다.  
생각해보면, 장비도 비싸고, 사용하는 툴도 MS visual SourceSafe (1994)이거나, 당시 최신 툴인 Subversion (2000)정도여서 그때는 거기까지가 최선이였고, 어쩔수 없이 발생하는 업무 공백들은 많은 사람들이 젊음으로 매우고 있었다. 말 그대로 '라떼는...' 이야기 이다. 

개발자가 로컬빌드를 하거나, 주로 여러 개발자의 소스가 VCS에 다 모아 졌을때, 빌드 담당자가 해당 소스를 빌드 서버로 다운받아 일괄 빌드을 한 후 결과를 게시하게 된다. (빌드서버는 개발자 PC 보다 HW spec이 좋았다. 그당시 workstation 급)  
게시된 결과가 테스터나, QA 담당자에게 전달되면, 이것을 다운로드 하여 확인하게 된다.    
오류가 없는 경우 빌드 결과는 배포 되지만, 오류가 발견되는 경우 (빌드 깨짐) 개발자에게 공지가 되고 개발자는 이를 수정하여 소스를 다시 check-in 해야 한다.  

이런 경우 주로 빌드 시간이 정해져 있다. 개발단계에 따라 최초 빌드 일정을 정하거나, 어느정도 완성이 된 후로는 주기적으로 매주 화요일 오후 몇시 이거나, 어느정도 제품이 런치된 유지보수 단계인 경우는, XP programming 이 유행하던 당시, daily 빌드를 한다고, 매일 오후 3시 까지 모두 check-in 하고, 4시에 빌드해야 하는 룰 도 있었다.  

빌드가 완성이 되면, 그 다음음 빌드를 확인 하는 과정인데, 테스터나, QA 담당자가 진행한다. 앞에서 말했지만 주로 오후 늦게 빌드가 완성이 되고, 일부 개발자들은 바로 퇴근을 하기 때문에 개발자와 테스터의 사이가 좋을 수가 없었다. (The Phoenix project 책에서도 이런 조직내 갈들이 표현되어 있다.)  

간단하게 그 과정을 정리하면, 

```
    - 소스를 VCS 에 업로드 한다.
    - 소스를 받아 로컬에서 빌드 한다.
    - 빌드 결과를 depoly 서버에 업로드 한다.
    - deploy 된 빌드를 download 해서 결과를 확인 한다. 
    - 확인 결과를 게시 한다. 
    - 게시된 빌드 결과에 따라 코드를 수정한다.
    - 수정된 소스를 다시 VCS 에 업로드 (version up) 한다.
    - 수정한 코드를 받아, 다시 빌드 한다.
```

이런 옛날 과정을 요즘 툴로 재연 (시뮬레이션) 해 보기로 했다.  
간단하게 hugo 을 이용해 프로젝트을 진행하고, github 으로 소스 관리를 진행한다. 

```
## create hugo project
$ hugo new site localbuild  
$ cd localbuild  

## git init
localbuild $ git init  

## add theme as a submodule
localbuild $ git submodule add https://github.com/alex-shpak/hugo-book themes/hugo-book  
**update baseURL and theme of config.toml**

## create a page 
localbuild $ cp -R themes/hugo-book/exampleSite/content.en/* ./content  

## push source (hugo project) repo
localbuild $ git remote add origin https://github.com/smjune/localbuild.git  
localbuild $ git add .  
localbuild $ git commit -m 'initiate project'  
localbuild $ git push origin main  

## add submodule to deploy public folder  
localbuild $ git submodule add https://github.com/smjune/Webdoploy.git public  

## build hugo project
localbuild $ hugo

## upload public 
localbuild $ cd public
localbuild/public $ git add .
localbuild/public $ git commit -m 'first deploy'
localbuild/public $ git push 
localbuild/public $ cd ..
localbuild $

## workflow
1. update pages
2. build                         (localbuild)
3. add/commit/push public folder (localbuild/public)
4. add/commit/push hugo project  (localbuild) ( echo 'public/' >> .gitignore )
```

[public submodule 오류](https://stackoverflow.com/questions/12218420/add-a-submodule-which-cant-be-removed-from-the-index/39189599)
