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

2005년 부터 약 10년간 SW개발에 참여하지 않았기에 branch 와 git 을 2016년 다시 SW개발 조직에 되돌아 와서야 접하게 되었다. 개인적으로 그 10년을 그대로 SW개발 업무를 계속했었더라면 현재 나의 위치가 지금과 많이 달라졌을찌 종종 생각하게 된다.  빠르게 발전하고 매년 새로운 기술이 나온는 SW 분야에서 10년의 외도는 그야 말로 나를 신입사원으로 만들게 충분한 시간이였다. 그 나마 대학 전공과 취업 후 6년을 시간들을 되 집어보면서 '그때 그랬는데' 라는 생각이 어느정도 도움이 되는 부분도 있었고, '어 아직도 이렇게 하고 있네?' 하는 부분은 적잖이 있어 놀라기도 했다.  

예를 들자면, 막 초기 피처폰이 활성화 되기 시작할 때 떠났던 사람이 스마트폰이 주류가 되었을 때 되돌아 온것이니, 많은 것이 달라져 있었고, 처음부터 다시 배워야 할것 들이 너무 많았으며, 당장 내가 할 수 있는 일은 많지 않다.  

지금부터 할 이야기는 나의 그 공백의 시간에 일어 났던 일들이다.  

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