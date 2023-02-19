---
title: "Delivery & Deployment"
weight: 5
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

SW 제품도 점차 서비스화 되면서 발전(?)하게 된 분야이다.  

기준에 package SW (shrinkwrap license) 에서 WEB 을 기반으로 한 서비스로 SW 제품의 성격이 변경되었다.  

기존에 박스를 사서 자시의 PC 에 설치하는 사용하는 것이 이제는 NW에 접속하여 온라인으로 사용하는 것이다.  

RTM (release to manufacturing) 이라고 해서 CD 로 구울 최후 SW 버전의 개념은, 기껏 HW 와 밀접하게 연관되어 있는 SW 로 한정되어 이제는 몇 남지 않아 보인다.  

* shrinkwrap contract (license) :  the seller considers to have been accepted by the buyer once the package is opened or the product used.

deploy 을 어느 user 수준까지 제공하는냐.  
    - 완료된 binary 을 누구에게 배포할 것인가?  
        . 내부 / 외부  
        .  discrete (App) / countinuous (WEB))

. 내부 user (tester, QA)  
. 외부 
      canary  
      A/B  
      단계적  

. DevOps 