---
title: "Presubmit"
weight: 4
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---

branch 와 더불어 presubmit 은 병결로 빼먹은 진도를 따로 따라 잡아야 하는 상황과 비슷했다.  


브랜치가 많아 짐에 따라 브랜치 운영 전략 (Flow) 이 복잡해짐  
이에 바로 main 브랜치에 submit 하는 것을 기본으로  
submit 전 Work In Progress 단계를 제공함  

    - code base 의 WIP 기능을 이용하여 소스를 업로드 한다.  
        (refs/for/head, Sheves)
    - WIP 와 연결된 workflow 에 따라 빌드 및 테스트가 수행된다.
    - 결과를 게시한다.
    - 수정한 코드로 WIP 을 업데이트 한다. (patch-set, revision)
    - WIP 와 연결된 workflow 에 따라 빌드 및 테스트가 수행된다.
    - 이상이 없는 경우 Code base 에 submit 한다. (version up)
    - submit 된 change 기준으로 다시 빌드, 테스트 한다.  
        (Postsubmit)

MR/PR    
shleves    
refs/for/head    