---
title: "Branches"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---

앞에서 말한 것 처럼 2016년이 되서야 다시 SW개발 업무를 다시 시작하게 되었으므로 나에게 branch 의 개념을 이해하는 것은, 군 제대 후 복학생으로 공업 수학의 미분을 푸는데 갑자기 인수분해가 되지 않았을때 느겼던 괴리감을 다시 한번 느끼게 해 주었다. 


submit 전에 어떻게 사전 검증을 할 것인가에 대하 대답으로  

브랜치 개념이 도입이 됨  

기존 post CI 가 적용된 브랜치를 운영 (dev) 하여  
확인이 완료된 change을 운영 브랜치 (main) 으로 merge  

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