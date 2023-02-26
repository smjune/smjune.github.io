---
title: "Hugo-book Theme"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## 주요 사이트 
기본 사이트 : <https://themes.gohugo.io/themes/hugo-book/>  
sample site : <https://hugo-book-demo.netlify.app/>  
Repository : <https://github.com/alex-shpak/hugo-book>  

{{< hint danger >}}
* docs 폴더의 하위 폴더 기준으로 메뉴구성을 해 준다. 
* 그 외 폴더 (예: Posts) 는 hugo.yml, 혹은 front matter 에 'menu' 로 별도 구성해야 한다. 
{{< /hint >}}

## hugo.yml for hugo-book
[hugo-book 샘플 hugo.yml](https://github.com/alex-shpak/hugo-book/blob/master/exampleSite/config.yaml)

* 지금 사이트 설정 (yml, toml, json 지원)

```yaml
baseURL: https://smjune.github.io/
title: MyoungJune Sung says Hello Wrold
theme: hugo-book

# Book configuration
disablePathToLower: true
enableGitInfo: true       # Set with "BookRepo" to used for 'Last Modified' links.

# Needed for mermaid/katex shortcodes
markup:
  goldmark:
    renderer:
      unsafe: true
  tableOfContents:
    startLevel: 1

menu:
  # before: []
  after:
    - name: "Github Repo"
      url: "https://github.com/smjune/"
      weight: 10
    - name: "Powered by Hugo"
      url: "https://gohugo.io/"
      weight: 20
    - name: "and hugo-book"
      url: "https://themes.gohugo.io/hugo-book//"
      weight: 30

params:
  # (Optional, default light) Sets color theme: light, dark or auto.
  # Theme 'auto' switches between dark and light modes based on browser/os preferences
  BookTheme: "auto"

  # Set source repository location.
  # Used for 'Last Modified' and 'Edit this page' links.
  BookRepo: https://github.com/smjune/smjune.github.io

  # Configure the date format used on the pages
  # - In git information
  # - In blog posts
  BookDateFormat: "January 2, 2006"

# you can add more option here   
```

## Pages Front matter
각 pages (md 파일) 에서 pages 에 대한 설정값을 조정한다.
```yaml
---
title: "Theme"
weight: 1                     # 메뉴에서 표시되는 순서 1 = 최우선
# bookFlatSection: false
# bookToc: true               # Table Of Content 표시 PaperMode에서 주로 사용
# bookHidden: false
# bookCollapseSection: false  # 메뉴에 하위 페이지가 있는 경우, 접힘표시 
# bookComments: false         # 해당 페이지의 comment 활성화 설정 (hugo.yml 설정보다 우선)
# bookSearchExclude: false
---
```

### Categories & Tages
각 페이지에서 해당 페이지에 대한 category 와 Tags 을 설정  

```yaml
Categories: "Posted"
Tags: ["Big Data","한글","Minority",]
```
혹은 
```toml
+++
title = "iMAC, Late 2009 upgrade"
description = "맥 업그레이드 관련 기록 저장, 테스트 페이지"
tags = [
    "iMac",
	"Scrivener",
	"Hi Sierra",
]
date = "2023-02-17T22:02:05+09:00"
categories = [
    "Mac",
]
BookComments=true
+++
```

---

## Shortcode
각 페이지에서 사용할 다양한 문단 효과, 아래와 같은 형식으로 사용한다.  
자세한 내용은 샘플 사이트를 참고 

```md
{{</* "Shortcode name" */>}}
내용 ...
{{</* /"Shortcode name" */>}}
```
### Hint
info/warning/danger 로 색 구분 (파랑/노랑/빨강) 지원  

```md
{{</* hint [ info | warning | danger ] */>}}
내용 ...
{{</* /hint */>}}
```

### Details
확장 되는 문단 표시 (expand 을 사용하는 대신)
open 옵션을 사용할 경우 항상 확장된 형태로 표시 됨

```md
{{</* details [ open ] */>}}
내용 ...
{{</* /details */>}}
```

### Mermaid
hugo.yml 에서 marmain 사용을 위해 "markup" 설정을 해야 한다.  
[Mermaid Docs](https://mermaid.js.org/intro/)  
[Mermaid live](https://mermaid.live)  

hugo 에서 제공하는 방식을 미리 theme에서 수정하였으므로, Theme방식을 따라야 한다.
```md
{{</* mermaid [class="text-center"] */>}}
Mermaid syntex 내용 ...    
{{</* /mermaid */>}}
```
### Section
하위 폴더 내용을 간략하게 표시해 준다.
```md
{{</* section */>}}
```
### columns 
한 페이지에 문단을 나눠서 표시 해둔다.
```html
{{</* columns */>}} <!-- begin columns block -->
# Left Content
Lorem markdownum insigne...

<---> <!-- magic separator, between columns -->

# Mid Content
Lorem markdownum insigne...

<---> <!-- magic separator, between columns -->

# Right Content
Lorem markdownum insigne...
{{</* /columns */>}}
```

### Tabs
하나의 문단을 tab으로 구분하여 표시 해준다.
```tpl
{{</* tabs "uniqueid" */>}}
{{</* tab "MacOS" */>}} # MacOS Content {{</* /tab */>}}
{{</* tab "Linux" */>}} # Linux Content {{</* /tab */>}}
{{</* tab "Windows" */>}} # Windows Content {{</* /tab */>}}
{{</* /tabs */>}}
```
  
---

## partial

### Comments

1. utterances 스크립트 생성  
https://utteranc.es/ 에서 가이하는 작성 방법에 따라 진행   

{{< hint info >}}
repo 는 자신의 블로그 repo (yourAcount/yourAccount.github.io) 을 사용해도 되고, 별도 프로젝트 repo (yourAccount/yourRepo) 을 사용해도 된다.  
해당 repo 에 utterances app 을 설치 하지 않아도 보이긴함, 그러나 작동은 안됨 (ChatGPT 가 틀린듯)
{{< /hint >}}

```html
<script src="https://utteranc.es/client.js"
        repo="smjune/smjune.github.io"
        issue-term="pathname"
        label="Comment"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
```
{{< hint danger >}}
utterances app 을 설치하지 않으면, 아래와 같은 에러가 발생함  
Error: utterances is not installed on smjune/smjune.github.io. If you own this repo, install the app. Read more about this change in the PR. 
{{< /hint >}}

2. utterances 스크립을 넣을 layouts 파일 
일반적으로 theme 을 사용하기 때문에 theme 에서 사용하는 commnet layout 을 overriding 하여야 한다. 
hugo-book (theme) 의 경우 theme/hugo-book/layouts/docs/comments.html 을 사용하여 hugo internal comment (Disque) 을 사용하게 되는데.
layouts/partials/docs/comments.html 을 만들어 hugo-hook 에 있는것 보다 먼저 사용하게 해야 한다. 

{{< hint warning >}}
theme 을 customizing 할때 theme 의 파일을 수정하는 것보다, 이렇게 hugo root 에서 부터 동일한 파일을 만들어 수정해야 한다. 로컬이나, github action 에 theme 을 업데이트 할때 수정한 파일이 원복되지 않게 하기 위해서 이다.
{{< /hint >}}

```
hugo
 ├─layouts
 │  └─partials
 │     └─docs
 │        └─comments.html        // theme 을 사용하지 않고 이 파일을 사용
 └─themes
    └─hugo-book
       └─layouts
          └─partials
             └─docs
                └─comments.html  // theme comment 
```

> hugo-book theme comment 는 bookComments: true 가 디폴트 이며, 따라서 모든 page 에 자동으로 적용된다. 따라서, 각 페이지에서 "bookComments: false" 을 설정하여 comment 을 OFF 하여야 한다. 

> theme 가 없는 경우 utterance 스크립을 /layouts/partials/utterances.html 에 넣고, 각 pages (xxx.md) 에서 {{ partial "utterances.html" . }} 을 직접 호출하여야 한다.

