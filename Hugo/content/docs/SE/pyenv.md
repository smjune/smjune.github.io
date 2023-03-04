---
title: "Python with Pyenv"
date: 2023-02-09T18:07:51+09:00
weight: 5
BookComments: false
---

# Pyenv 사용하기 

```bash
$ pyenv versions
* system (set by /home/june.sung/.pyenv/version)
  2.7.17
$ pyenv install --list
$ pyenv install 3.6.9
* system (set by /home/june.sung/.pyenv/version)
  2.7.17
  3.6.9
$ pyenv shell 3.6.9 
$ pyenv which python 
  3.6.9 (set by PYENV_VERSION environment variable)

# $ pyevn [ global > local > shell ] X.X.X
# cat ~/.pyenv/version | cat .pyton-version | echo $PYENV_VERSION
# loacal 은 해당 폴더 아래 (set by ~폴더/.python-version) python 설정  (해당 폴더 나가면 해제)
# Shell 은 해당 터미널 (set by PYENV_VERSION) 에 python 설정 (해당 터미널 나가면 해제)

$ virtualevn -p $(pyenv which python) .venv        # 바로 위 shell 에 설정한 python 을 사용
$ pyenv shell --unset                              # 현재 shell의 python 설정 해제
```
{{< hint danger >}}
:memo:문제는 'global / local /shell' 중 어떤 python 설정을 현재 폴더에 가상환경 ( .venv)으로 만들것인가?  
1. Pyenv 로 python version들을 설치 
2. 현재 python 환경 (local / shell) 설정 
3. python3 -m venv 로 .venv 만든 후, (현재 python 환경이 반영됨)
4. '--unset' 으로 현재 python 설정 해제
5. source .venv/bin/activate 으로 가상환경 실행    
{{< /hint >}}
  
	1.pyenv                         # have to install by using  script  & edit $(Home)/.bashrc
                                          (curl https://pyenv.run  | bash)
	2.virtualenv                    # have to install  with pip
	3.pyenv-virtualenv              # $ pyenv virtualenv XXXX XXXX 을 사용한다면 설치  (pyenv 모듈)
	4.python3  -m  venv                 (higher than 3.4, python3 모듈)


## pyenv 과 virtualenv 별도 사용 
```bash
$ virtualenv py271 --python=python2.7
```

### Shell setup :  
```bash
$ pyenv shell 2.7.1    # 현재 shell 에 2.7.1 적용
$ pyenv which python   # shell 확인
$ virtualenv -p $(pyenv which python) py271     # .venv 
$ pyenv shell  -- unset   # 현재 shell 해제

$ source py271/bin/activate  # .venv/bin/activate
(py271)$
...
(py271)$ pip freeze > requirements.txt
(py271)$ pip install -r requirements.txt
...
(py271)$ deactivate
$
```  

### local setup :  
local path에 적용하기 (해당 폴더를 빠저 나가면 해제)  
:clap: *shell 인 경우 해당 터미널을 빠저 나가면 해제됨*  

```bash
$ python —version
Python 0.0.0 
$ mkdir test
$ cd test
/test$ pyenv local x.x.x
/test$ python —version
Python x.x.x
/test$ pyenv versions
System
* X.X.X (set by /home-mc/june.sung/test/.python-version)
/test$ cd ..
/$python —version
Python 0.0.0       
/$ pyenv versions
* System (set by /home-mc/june.sung/.pyenv/version)
X.X.X 
```
 
## global / local setup  
:clap: pyenv 의 virtualenv 모듈 사용
 
```bash
$ pyenv versions
$ pyenv install --list
$ pyenv install 3.6.9
 
$ pyenv virtualenv -p 3.6.9  py369
$ pyenv versions 
* system (set by /home/june.sung/.pyenv/version)
  2.7.17
  3.6.9
  3.6.9/envs/py369
  py369
 
$ pyenv activate py369         
...
(py369) $ pyenv deactivate     
$  
```

### pyenv local 을 이용한 로컬에 가상환경 구성  
```bash
/test$ pyenv local py369
(py3369)/test$ cd ..
/$
```
 
## Pyenv + python3 의 venv 모듈 사용  
:clap: after Pyhon 3.3  

> pyenv 로 특정하지 않으면, python3 --vesion 에 표시된 버전으로 생성됨   

```bash  
$ pyenv versions           # (set by ??? 표시로 구분)
$ pyenv [global | local | shell ] X.X.X
# $ pyenv which python     # 어느 python 셋팅을 쓸것인가?
$ python3 -m venv .venv    # Python3 module venv 
# $ pyenv [global | local | shell ] -unset
$ source .venv/bin/activate
(.venv) $
...
(.venv) $ deactivate
$  
```  
{{< hint danger >}}
:memo: **결론**  
pyenv local  X.X.X로 해당 로컬폴더만 X.X.X로 셋업해서,  
python3 -m venv .venv 로 가상환경 만들어 사용 하고,   
pyenv virtualenv 나 virtualenv 는 사용하지 말자.  - 너무 많이 알면 헤깔린다.  
{{< /hint >}}

## pip install error  
:office:  proxy setup  
```bash  
$ vi .config/pip/pip.conf
 
[global]
proxy = http://xxx.xxx.xxx.xxx:8080
cert = /path/to/DXXXXXX.crt
trusted-host = pypi.python.org
               pypi.org
               files.pythonhosted.org
```

:computer: CLI  
```bash
$ pip install --prxoy http://xxx.xxx.xxx.xxx:8080 --trusted-host pypi.python.org --cert .\DXXXXXX.crt
```