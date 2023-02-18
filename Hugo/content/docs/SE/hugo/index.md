---
title: "Hugo Tips"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

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
       └─essay.md
          └─images
             └─essay.png   # essay 이미지
```

* 참고
https://discourse.gohugo.io/t/question-about-content-folder-structure/11822/4?u=kaushalmodi