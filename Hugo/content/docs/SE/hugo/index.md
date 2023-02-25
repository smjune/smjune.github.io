---
title: "Hugo Tips"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
bookComments: false
# bookSearchExclude: false
---
## hugo.yml (config.toml)
v0.110.0 이상에서 지원, 하위 호환을 위해 기존 config.toml 도 사용 가능  
theme 의 가이드에 따라 설정값들을 사용해야 한다.
> :bulb: **Tip** [hugo-book 샘플 hugo.yml](https://github.com/alex-shpak/hugo-book/blob/master/exampleSite/config.yaml)

* 지금 사이트 설정 (yml, toml, json 지원)
```yaml
baseURL: https://smjune.github.io/
title: MyoungJune Sung says Hello Wrold
theme: hugo-book

# Book configuration
disablePathToLower: true
enableGitInfo: true

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
```

## Bundles

전체 글 구조를 잡을때, 가장 중요하게 생각해 하는 부분이 hugo 의 bundle 개념이다.  
Leaf 와 Branch 로 나눠 지는대, 말 그대로 leaf bundle 은 말단 말뭉치 (?) 이므로,  
하위로 다른 구성요소를 갖을수 없다.  
반면 Branch bundle의 경우 하위로 다른 branch bundle 과 leaf bundle을 갖을 수 있다.  

자세한 차이점은 아래 표를 참고 하자
> index.md vs _index.md 으로 구분하여 보면 된다.  

https://gohugo.io/content-management/page-bundles/   

|  	| Leaf Bundle 	| Branch Bundle 	|
|:---:	|:---:	|:---:	|
| Usage 	| Collection of content and attachments for single pages 	| Collection of attachments for section pages (home page, section, taxonomy terms, taxonomy list) 	|
| Index filename 	| index.md 1 	| _index.md 1 	|
| Allowed Resources 	| Page and non-page (like images, PDF, etc.) types 	| Only non-page (like images, PDF, etc.) types 	|
| Where can the Resources live? 	| At any directory level within the leaf bundle directory. 	| Only in the directory level of the branch bundle directory i.e. the directory containing the _index.md [(ref)](https://discourse.gohugo.io/t/question-about-content-folder-structure/11822/4?u=kaushalmodi). 	|
| Layout type 	| single 	| list 	|
| Nesting 	| Does not allow nesting of more bundles under it 	| Allows nesting of leaf or branch bundles under it 	|
| Example 	| content/posts/my-post/index.md 	| content/posts/_index.md 	|
| Content from non-index page files… 	| Accessed only as page resources 	| Accessed only as regular pages 	|

### Menu

1. posts 항목에 book과 novel 이라는 페이지가 생성된다.
```
content
 └─posts
    ├─_index.md    # posts 가 리스트가 되기 위해 필요
    ├─book.md      # http://~/posts/book
    └─novel.md     # http://~/posts/novel
```
*content 하위로 posts 와 docs 페이지가 생성된다.*
```
content
 ├─posts           # http://~/posts
 │  ├─_index.md   
 │  ├─book.md   
 │  └─novel.md
 ├─docs.md         # http://~/doc
 └─_index.md       # content 가 list 가 되기 위해 필요
 ```

2. posts 항목에 book 페이지 만 생성 된다. 
```
contents
 └─posts
    └─book
       ├─index.md   # http://posts/book/
       └─novel.md   # is not rendered.
```
*book 은 index.md 으로 leaf bundle 정의되어 하위 페이지를 갖을 수 없어 novel 은 표시되지 않는다.*  

3. posts 항목에 book 페이지 와 book 하위로 novel 페이지 가 생성된다.
```
contents
 └─posts
    └─book
       ├─_index.md     
       └─novel.md     # http://~/posts/book/novel
```
4. posts 항목에 book 페이지 가 만들어 지고, 하위로 novel, essay 페이지가 만들어 진다.
```
contents
 └─posts
    └─book
       ├─_index.md
       ├─novel        # http://~/posts/book/novel
       │  └─index.md
       └─essay.md     # httP://~posts/book/essay
```


### Lacal Image

Leaf bundle 은 하위로 images 폴더를 만들어 해당 페이지 에서 사용하는 이미지를 따로 저장하자.   
branch bundle 은 _index.md 와 동일한 folder 위치에 이미지를 저장해야 한다.

```
contents
 └─posts
    └─book
       ├─_index.md         # ![이미지](./book.png)
       ├─book.png          # book 이미지 
       ├─novel
       │  ├─index.md       # ![이미지](./images/novel.png)
       │  └─images
       │     └─novel.png   # novel 이미지
       └─essay
          ├─index.md       # # ![이미지](./images/essay.png)
          └─images
             └─essay.png   # essay 이미지
```

>[참고](https://discourse.gohugo.io/t/question-about-content-folder-structure/11822/4?u=kaushalmodi)

## comment (utterances)

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