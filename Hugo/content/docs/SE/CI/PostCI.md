---
title: "Post CI"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

CI 개념이 최로로 나로면서  

submit 된 내용이 CI 툴에 의해 모니터링 되어  (혹은 WebHook 으로 호출)
CI 툴 (서버) 에서 빌드, 테스트 되어 deploy 됨  

Github self-hosted 는 항상 repos 을 listening 하고 있다.  
    bare metal 서버  
    vitural 서버  

    - 소스 코드를 VCS 에 업로드 한다 
    - VCS 로 부터 WebHook 혹은 Polling 을 통해 CI 서버가 빌드 한다. 
    - 빌드 후 자동화된 테스트 를 수행한다. 
    - 결과를 게시 한다. 
    - 게시된 결과에 따라 코드를 수정한다.
    - 수정한 코드를 VCS 에 다시 업로드 한다. (version up)