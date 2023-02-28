---
title: "Gitbook"
weight: 6
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---

## Gitbook

{{< hint info>}}
Gitbook 도 생각을 해 봤으나, 2017년 이후로 gitbook-cli 가 업데이트을 지원하지 않음  
Google, MS 등 SW 개발 도규먼트들과 비슷한 형태로 (gitbook 으로 작성된것이라고 들은것 같은데... 확실치 않음.)  
그래도 그나마 눈에 익숙하고, 여러형태의 e-book 으로도 지원했던것 같다.  
사용해 보려고 했으나, 설치 난이도 [참조](https://github.com/GitbookIO/gitbook-cli/issues/110) 와 github actions 지원이 좀 애매하다. [참조](https://github.com/SoftUni/Programming-Basics-Book-JS-EN/blob/master/.github/workflows/gitbook-deploy.yml)

* Known Dependencies  
node : v12.22.1  
npm : v6.14.12  
gitbook-cli : gitbook-cli@2.3.2  
graceful-fs : 4.1.4  

**관련사이트**  
https://github.com/GitbookIO/gitbook-cli  
https://docs.gitbook.com/integrations/github  
https://www.gitbook.com/  
{{< /hint >}}

## install gitbook  
on MacOS (high sierra, 10.13.6)

```bash
# Mac OSX.
$ brew install node
 
# 해당 명령어로 오류가 나서 nvm 을 설치 하여 node 12.22.1 을 설치 
# brew install nvm  이후, 가이드에 따라 설정 
$ nvm -v
0.39.3
# gitbook dependencies 해결 node 버전 설치 
$ nvm install 12.22.1
Downloading and installing node v12.22.1...
Downloading https://nodejs.org/dist/v12.22.1/node-v12.22.1-darwin-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with shasum -a 256
Checksums matched!
Now using node v12.22.1 (npm v6.14.12)
Creating default alias: default -> 12.22.1 (-> v12.22.1)
$ nvm use 12.22.1
Now using node v12.22.1 (npm v6.14.12)
$ node -v
v12.22.1
# https://github.com/GitbookIO/gitbook-cli/issues/110 참조해서 graceful-fs dependecies 해결 후 
$ gitbook init
...
$ gitbook serve
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 7 plugins are installed 
info: loading plugin "livereload"... OK 
info: loading plugin "highlight"... OK 
info: loading plugin "search"... OK 
info: loading plugin "lunr"... OK 
info: loading plugin "sharing"... OK 
info: loading plugin "fontsettings"... OK 
info: loading plugin "theme-default"... OK 
info: found 1 pages 
info: found 0 asset files 
info: >> generation finished with success in 0.7s ! 

Starting server ...
Serving book on http://localhost:4000

# Ubuntu 도 아래 명령어로 오류가 나면, nvm 을 설치해서 사용해야 할듯.
# $ sudo apt-get install nodejs npm
```
