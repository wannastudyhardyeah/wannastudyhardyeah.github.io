---
title: GitHub Actions에 graphviz 추가하기
author: wannastudyhardyeah
date: 2023-08-10 22:01:30 +0800
categories: [BLOG]
tags: [BLOG, jekyll, workflow]
math: true
mermaid: true

---
이용한 라이브러리는 <a href="https://github.com/ts-graphviz/setup-graphviz" target="_blank">"setup-graphviz"</a>.<br>
``readme.md``에 안내되어 있는 대로 깃허브 액션 환경(GitHub Action environment)에 ``Graphviz``가 setup되도록 추가하면 되는데,<br>
``jekyll`` 테마의 ``chirpy``를 사용하고 있는 나는 이걸 어디에 추가해야 하는지 감이 안 잡혔다.<br>

처음엔 ``pages-deploy.yml.hook``에 추가해봤으나 여전히 ``plantUML`` 다이어그램은 제대로 나오지 않았고,<br>
그 다음으로 ``jekyll.yml``에 추가해보기로 했다.<br>
물론, ``jekyll.yml``은 ``master`` 브랜치에서 직접 수정하는 것이 불가능하다.<br>
새로운 브랜치를 만들거나 이외의 기존 브랜치에서 작업한 것을 본래 브랜치에 PR해주는 식으로 하면 된다.<br>
아무튼, 아래와 같이 추가하였다.<br>

주석 ``#`` 기호로 감싸서 구분해놓은 코드 두 줄이 내가 복붙하여 추가한 부분이다.<br>

```yaml
jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
###################################################
      - name: Setup Graphviz
        uses: ts-graphviz/setup-graphviz@v1        
###################################################
      - name: Setup Ruby
```