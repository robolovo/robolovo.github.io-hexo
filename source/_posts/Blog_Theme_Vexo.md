---
title: Hexo 블로그에 테마 적용하기
date: 2021-12-21 18:30:23
categories: Develop
---

<br>

시작하기 전에, 마음에 드는 [테마](https://hexo.io/themes/) 를 골라주세요.

저는 깔끔한 디자인이 마음에 들어서 Vexo(Vue.js 기반으로 만들어진)라는 테마를 선택하였습니다. 
그럼 바로 어떻게 적용하는지 알아보도록 하겠습니다. (다른 테마를 선택했을 경우, 해당 테마 깃헙에 README.md를 참고하시면 됩니다.)

<br>
<br>
<br>

1. **_Vexo 테마 적용_**

    테마를 적용하는 방법은 간단합니다. 

    별다른 설정 없이, [Vexo](https://github.com/yanm1ng/hexo-theme-vexo#install) 깃헙 README.md에 작성된 해당 명령어들을 순서대로 따라 하면 됩니다.

    다 하셨으면 `hexo server` 명령어를 통해 서버를 실행시키고, `localhost:4000`에 접속해 봅니다. 

    Vexo 테마가 적용된 블로그 화면을 보실 수 있습니다.

<br>
<br>

2. **_새로운 포스트 작성해보기_**

    다음의 hexo 명령어를 통해서 새로운 포스트를 생성할 수 있습니다. 

    `hexo new post <title>`

    다시 말하지만, hexo는 포스트를 생성할 때 scaffolds의 마크다운 파일을 기반으로 생성합니다. 
    
    `vi source/_posts/<title>.md`
   
    vi 에디터로 파일을 열어 내용을 추가한 후 저장합니다. (IDE를 사용하셔도 됩니다.)

    다시 `localhost:4000`에 접속하면 블로그에 새롭게 추가된 포스트를 볼 수 있습니다.

<br>
<br>

3. **_Vexo 폴더 분석_**

    그대로 사용할 거라면 상관없지만, 테마를 커스터마이징하기 위해서는 어느 정도 Vexo에 대한 이해가 필요합니다.
    그럼, themes/vexo 폴더로 이동해 볼까요?
    
    `cd themes/vexo`
    `ls`
    
    하위 폴더 구조는 다음과 같습니다.

    ```
    LICENSE   README.md   _config.yml   _source   layout   lint.sh   source
    ```
   
    **_config.yml**: 테마의 설정 파일입니다. 설정값들은 ejs파일에서 전역변수(Hexo에 정의된 전역변수가 아닙니다.)로 접근이 가능한 값들입니다.

    **_source**: 마크다운으로 작성된 페이지 템플릿 파일이 위치하는 곳입니다.

    **layout**: ejs(자바스크립트가 내장된 html 파일)파일들이 위치하는 곳입니다. 실제로 렌더링 될 정적 파일들은 이곳에 있는 ejs 파일들을 기반으로 생성이 됩니다. 즉, 페이지의 레이아웃을 변경하고 싶다면 <해당 페이지>.ejs 파일을 손보면 됩니다.   

    **source**: css, js, font등이 위치하는 곳입니다.

<br>
<br>

4. **_디버깅_**

    3번을 통해, Vexo의 폴더 구조에 대해서 알아보았습니다.
    
    이제 이해한 내용을 바탕으로 커스터마이징을 시작하시면 됩니다. Vexo를 사용하신다고 Vue.js를 공부할 필요는 없지만 html, css, js를 작성할 줄은 알아야 합니다.
   
    - layout 폴더 하위에 새로운 ejs 파일을 추가하거나 기존의 ejs 파일을 수정하여 레이아웃을 바꿀 수 있습니다. 
    - source 폴더 하위의 css 파일들을 수정해 주면서 디테일한 스타일을 바꿀 수 도 있습니다.

    그럼 제가 블로그를 만들면서 디버깅할 때 도움이 되었던 참고 자료들을 공유하면서 마치도록 하겠습니다. 감사합니다 :)

    - [Hexo Commands - 공식문서](https://hexo.io/ko/docs/commands)
        Hexo의 명령어들입니다.

    - [Hexo Variables - 공식문서](https://hexo.io/ko/docs/variables) 
        기존에 작성된 ejs파일을 보면 `page.xxx` 를 자주 볼 수 있는데요, 
        이게 갑자기 어디서 튀어나온 변수인지 디버깅을 할 때 꽤나 오랜 시간이 걸렸는데, 알고 보니 Hexo에 정의된 전역 변수였습니다. Hexo Variables는 커스터마이징 할 때도 많이 쓰이기 때문에 참고하시기 바랍니다.
    
    - [Hexo의 Category와 Tag 페이지 생성](https://aciddust.github.io/blog/post/Hexo%EC%9D%98-Category%EC%99%80-Tag-%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%83%9D%EC%84%B1)
        Hexo의 페이지 생성 원리에 대해서 알 수 있습니다.
 