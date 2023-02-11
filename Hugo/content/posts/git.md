---
title: "Git command 정리"
date: 2023-02-11T10:04:43+09:00

---

## 연습 Site   

http://learngitbranching.js.org/  
https://backlogtool.com/git-guide/kr/  
```
$ level                       - 연습문제 초기 화면 (문제선택)  
$ sandbox                     - 빈 연습  
$ show solution               - 해당보기  
$ reset                       - 해당 level 처음부터 다시  
$ undo                        - 1개 명령 취소  
$ git fakeTeamwork 1          - origin 에 1개 커밋 넣기  
```


### Set up 
```bash
$ git clone -b [브랜치 | tag] [REPO URL]  
$ git remote add orgin [REPO URL]      // origin 으로 REPO URL 등록
$ git remote rm orgin                  // origin 삭제
$ git submodule add [REPO RUL] [Folder Path]
$ git submodule update 
```


### branch 
```bash
$ git branch -f bugfix HEAD~1                       
: bugfix 브랜치를 HEAD [혹은 브랜치 명] 1개 전 commit으로 이동  

$ git branch -u origin/maser [Branch A]          
: 이미 있는 local Branch A (생략하면 현재 checkout branch) 가 origin/master 을 track함 --> git checkout --track 과 비교  

$ git branch -d Branch A  
: local 에서만 Branch A 삭제  
```
### checkout
```bash
$ git checkout branch A                               
: Remote에 있는 branch A 에 대해 local 에 branch A 와 origin/branch A만들고, checkout.  
-> 로컬 branch A가 없고, 유일한 Remote에 branch A가 있다면 ("remotes/origin/branch A"가 있어야 함)  

$ git checkout HEAD~1                                  
: HEAD [혹은 브랜치 명] 을 1개 commit 앞으로 이동, checkout  

$ git checkout origin/master                         
: origin/master 가 있던 commit에서 HEAD을 만들고 checkout (Detached state)  

$ git checkout -b [Branch A] origin/master       
: Branch A을 만들고 origin/master을 tracking 함.  

$ git checkout --track origin/master               
: Local에 master(remote와 같은 이름의 브랜치)을 만들고 checkout 한 후 origin/master (Remote 브랜치)을 tracking 함. --> git branch -u 와 비교  
```   
### Others
```bash
$ git cherry-pick [commit-ID1] [commit-ID2] …  
: 현재 checkout된 브랜치에 C1, C2 을 넣어라  

$ git rebase [Branch A] [Branch B]                  
:  branch A 아래로 Branch B (checkout) 를 옮긴다. (FF 가능하면 FF)  

$ git rebase [Branch A]                                 
: branch A 아래로 HEAD (checkout한 branch)를 옮긴다. (FF 가능하면 FF)  

$ git rebase -i HEAD~[몇 개 상위?]                
: X 개 뒤 Commit 들을 선택하여 새롭게 다시 지금 branch을 재구성한다.  

$ git pull --rebase origin/master                    
: origin/master (생략시 현재 branch가 track 하는 remote 브랜치) fetch 하고 현재 checkout 된 branch 을 그 아래로 이동 = $ git fetch origin master + git rebase origin/master  

$ git reset HEAD~[몇 개 상위?]                      
: HEAD가 있는 branch 을 ~ X개 뒤 commit으로 옮긴다.  

$ git revert HEAD                                      
:  HEAD commit 을 다시 만든다 (commit --amend ?? 와 비슷?)  
```

### Merge
```bash 
Merge [ branch A]   : checkout 된 branch 에  branch A 와 합쳐진 commit을 만든다.     
```

### Fetch/Pull/Push
```bash   
Fetch/Pull/Push                                             
Fetch/Pull/Push [Remote]  
Fetch/Pull/Push [Remote] [source branch]          // 여기까지만 사용하는것을 권장  
Fetch/Pull/Push [Remote] [source]:[tartget]  
 
$ git fetch origin master~1:branchA  
: origin (Remote) master보다 1개 앞선 commit을 local에 branchA 브랜치로 만든다. (checkout 하지 않는다.)  

$ git fetch origin master               
: origin (Remote) 에 있는 master 을 local에 (origin/master) 업데이트 한다. (없으면 만든다. Checkout 하지 않는다.)  

$ git fetch origin :side                  
: origin (Remote) 에 없는 side 브랜치를 Local에만 만든다 -> = *$ git branch side  

$ git fetch                                 
: 현재 checkout 된 브랜치의 origin (Remote) 업데이트  
 
$ git pull origin master:branchA  
: origin (Remote) master 을 local에 branchA로 만들고 checkout된 브랜치가 branchA를 merge.  
= git fetch origin master:branchA + git merge branchA  

$ git pull origin master            
: origin (Remote) master 을 local에 Fetch하고 (origin/master 만들거나, 업데이트), checkout된 브랜치가 origin/maser를 Merge  
= fetch origin master + merge origin/master  
   * $ git pull --rebase origin/master = $ git fetch origin master + git rebase origin/master    

$ git pull                              
: 현재 checkout된 브랜치가 tracking하는 origin (Remote)을 업데이트하고, checkout된 브랜치가 tracking branch를 Merge  
= fetch origin [the checkouted branch] + merge origin/[the checkouted branch]  
 
$ git push origin HEAD:refs/for/main  
:  현재 HEAD 브랜치를 gerrit main 브랜치(를만들고)로 push 한후 (submit type에 따라 merge, rebase, cherry-pick 등을 함)   
-> HEAD가 있는 commit 위치로 origin/main 을 progress 시키겠다.  

$ git push origin HEAD^:master       
: local HEAD보다 1개 앞선 commit을 origin (Remote) 에 master 브랜치로 push (trancking을 만들지는 않음)  
-> HEAD 보다 1개 앞선 commit 으로 origin/master 을 progress 시키겠다.  

$ git push origin BranchA               
: origin (Remote) 에 로컬브랜치 BranchA 을 push 하고 track 함 (없으면 origin/BranchA도 만듬, checkout과 상관없음)  
-> BranchA 가  progress 한 만큼 서버 상태도 progress 한다.  

$ git push origin :side                    
: origin (Remote) 에서 side 브랜치를 삭제한다.  

$ git push                                   
: 현재 checkout된 브랜치가 tracking 하는 origin 으로 (없으면 origin/~~을 만듦) 현재 checkout된 브랜치를 push   
= push origin [the checkouted branch]:origin/[the checkouted branch]  
```

- checkout 된 브랜치가 어떤 a branch(을) 와 Merge 해옴  
 
- 모든 Remote 에 모든 tracing 하는 브랜치 와 … Fetch/Pull/Push  
- 언급한 Remote 에 모든 tracing 하는 브랜치 와 …Fetch/Pull/Push  
- 언급한 Remote 에서/에서/으로 소스 브랜치를  …Fetch/Pull/Push  
-  소스 브랜치 : 타겟 브랜치     -->  gerrit 사용시 : $ git push origin [source]:refs/for/[target]  

