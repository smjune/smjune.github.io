---
title: "Hugo Tips"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
bookCollapseSection: true
bookComments: false
# bookSearchExclude: false
---
## Hugo (SSG)  
https://gohugo.io/documentation/   

    1. $ hugo new site [hugo project name] 으로 프로젝트 생성.  
    2. config.toml : baseURL, Title 과 Theme 을 수정.  ( 혹은 hugo.yml)
    3. themes : 사용할 Web theme 을 설치. ( git submodule 사용 )  
    4. content : 폴더/파일.md 형태로 글 작성 및 구성. ( $ hugo new posts/hello.md )  
    5. hugo server 으로 로컬 호스트 페이지 확인 ( md 파일에 draft : true 인 경우 -D 옵션 필요)
    6. hugo server 가 실행 중이면, 저장하는 수정 내용이 바로 로컬 호스트 페이지에 반영됨

### hugo.yml (config.toml)
v0.110.0 이상에서 지원, 하위 호환을 위해 기존 config.toml 도 사용 가능  
theme 의 가이드에 따라 설정값들을 사용해야 한다.

```yaml
baseURL: https://smjune.github.io/        # 실제 접속 사이트 주소
title: MyoungJune Sung says Hello Wrold   # 사이트 제목
theme: hugo-book                          # 랜더링 할 theme
```

### hugo server

{{< hint info >}}
-D : draft 까지 랜더링함  
-t [theme] : (config에 theme 미 설정시) 해당 theme로 랜더링함  
{{< /hint >}}

```bash
$ hugo server
Start building sites … 
hugo v0.110.0+extended darwin/amd64 BuildDate=unknown

                   | EN  
-------------------+-----
  Pages            | 95  
  Paginator pages  |  2  
  Non-page files   | 38  
  Static files     | 78  
  Processed images |  0  
  Aliases          | 28  
  Sitemaps         |  1  
  Cleaned          |  0  

Built in 730 ms
Watching for changes in /Users/myoungjunesung/blog/github/Hello_world/Hugo/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Users/myoungjunesung/blog/github/Hello_world/Hugo/hugo.yml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

server 을 계속 실행해 놓고, md 파일을 수정후 저장하면 바로 반영되어 로컬 호스트에서 바로 확인 가능
```bash
Change detected, rebuilding site.
2023-02-26 16:16:18.514 +0900
Source changed WRITE         "/Users/myoungjunesung/blog/github/Hello_world/Hugo/content/docs/SE/hugo/theme.md"
Total in 125 ms
```

## Bundles

전체 글 구조를 잡을때, 가장 중요하게 생각해 하는 부분이 hugo 의 bundle 개념이다.  
**Leaf** 와 **Branch** 로 나눠지는대, 말 그대로 **leaf bundle** 은 말단 말뭉치 (?) 이므로,  
하위로 다른 구성요소를 갖을수 없다.  
반면 **Branch bundle**의 경우 하위로 다른 branch bundle 과 leaf bundle을 갖을 수 있다.  

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

