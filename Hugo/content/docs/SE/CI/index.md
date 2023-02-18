---
title: "Countinuous Integration"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## History 

## 1. local build  
    - 소스를 VCS 에 업로드 한다.
    - 소스를 받아 로컬에서 빌드 한다.
    - 빌드 결과를 depoly 서버에 업로드 한다.
    - deploy 된 빌드를 download 해서 결과를 확인 한다. 
    - 확인 결과를 게시 한다. 
    - 게시된 빌드 결과에 따라 코드를 수정한다.
    - 수정된 소스를 다시 VCS 에 업로드 (version up) 한다.
    - 수정한 코드를 받아, 다시 빌드 한다. 

## 2. Countinous Integration (Post integration)
    - 소스 코드를 VCS 에 업로드 한다 
    - VCS 로 부터 WebHook 혹은 Polling 을 통해 CI 서버가 빌드 한다. 
    - 빌드 후 자동화된 테스트 를 수행한다. 
    - 결과를 게시 한다. 
    - 게시된 결과에 따라 코드를 수정한다.
    - 수정한 코드를 VCS 에 다시 업로드 한다. (version up)

## 3. Branch (Pre integration : Git-Flow)
    - 각자 정해진 소스 트리 (branch) 에 소스를 업로드 한다.
    - 해당 브랜치로 부터 WebHook 혹은 Polling 을 통해 CI 서버가 빌드 한다.
    - 빌드 후 자동화된 테스트 를 수행한다. 
    - 결과를 게시 한다. 
    - 게시된 결과에 따라 코드를 수정한다.
    - 수정한 코드를 정해진 브랜치에 다시 업로드 한다. (version up)
    - 해당 브랜치로 부터 WebHook 혹은 Polling 을 통해 CI 서버가 빌드 한다.
    - 빌드 후 자동화된 테스트 를 수행한다. 
    - 이상이 없는 경우 Code base 와 해당 브랜치를 merge 한다. 
    - merge된 code base 을 다시 빌드, 테스트 한다.

## 4. Pre/Post-submit (trunk based)
    - code base 의 WIP 기능을 이용하여 소스를 업로드 한다.  
        (refs/for/head, Sheves)
    - WIP 와 연결된 workflow 에 따라 빌드 및 테스트가 수행된다.
    - 결과를 게시한다.
    - 수정한 코드로 WIP 을 업데이트 한다. (patch-set, revision)
    - WIP 와 연결된 workflow 에 따라 빌드 및 테스트가 수행된다.
    - 이상이 없는 경우 Code base 에 submit 한다. (version up)
    - submit 된 change 기준으로 다시 빌드, 테스트 한다.  
        (Postsubmit)

## 5. CD
    - 완료된 binary 을 누구에게 배포할 것인가?  
        . 내부 / 외부  
        . discrete (App) / countinuous (WEB))  


## 6. CI/CD ( DevOps )
    - SW 서비스 


