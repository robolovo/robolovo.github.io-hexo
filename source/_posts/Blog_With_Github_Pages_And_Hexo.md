---
title: Github 블로그 만들기 With Hexo
date: 2021-12-21 11:30:33
categories: Develop
---

<br>

첫 포스트에서는 Github Pages와 Hexo로 블로그를 만드는 방법에 대해서 알아보겠습니다.

**Github Pages**는 Github에서 제공하는 정적 웹사이트 호스팅 서비스로 자신의 레포지토리에서 웹 페이지를 구동할 수 있게 해줍니다. 

**Hexo**는 Markdown을 사용하여 작성된 포스트에 테마를 가미해서 정적 파일을 생성해 주는 역할을 합니다. 또한,  Hexo에서 제공하는 몇가지 커맨드를 이용하면 쉽고 빠르게 테마 설정, 제너레이팅, 배포등을 할 수 있다는 장점이 있습니다. 쉽게 말해서, 블로그를 쉽게 만들수 있도록 도와주는 프레임워크라고 보면 될 것 같습니다.

<br>
<br>

1. **_Github repo 만들기_**

    <자신의 깃헙 아이디>.github.io 이름으로 public 레포지토리를 생성합니다.

<br>
<br>

2. **_Hexo 설치_**

    Hexo는 Node.js기반으로 만들어졌기 때문에 npm을 통해 설치할 수 있습니다. (요구되는 Node.js버전은 [공식문서](https://hexo.io/ko/docs/#Minimum-required-Node-js-version) 를 참고하시길 바랍니다.)

    `npm install -g hexo-cli`

<br>
<br>

3. **_Hexo 프로젝트 생성_**
    
    Hexo 프로젝트를 생성하고 초기화하기위해 다음 명령어를 입력합니다.

     `hexo init <folder>`
     `cd <folder>`
     `npm install`

    결과로 <folder> 하위에 다음과 같은 구조를 가진 폴더들이 생성됩니다.

    ```
    .
    ├── _config.yml
    ├── package.json
    ├── scaffolds
    ├── source
    |   ├── _drafts
    |   └── _posts
    └── themes
    ```

    **_config.yml**: 설정 파일입니다. 이 파일의 설정값들은 [공식문서](https://hexo.io/ko/docs/configuration) 를 참고하여 작성하면 됩니다.
    
    **package.json**: npm으로 설치된 패키지의 버전 정보를 명시하는 파일입니다.

    **scaffolds**: 새로운 포스트를 생성할 때, Hexo는 scaffold를 기준으로 새 파일을 생성합니다. 쉽게 말해서, 템플릿같은 개념입니다. 그대로 사용하거나, 자신이 원하는 대로 수정하면 될 것 같습니다.
          
    **source**: 웹 사이트 컨텐츠들을 위치시키는 곳입니다. 렌더링이 가능한 파일들은 처리된 후 public 폴더로 들어가게 됩니다. _posts는 `hexo new post <포스트 이름>` 명령어로 생성된 마크다운 파일들이 위치하는 곳입니다.

    **themes**: 테마 폴더입니다. Hexo는 해당 테마를 가미하여 정적 파일들을 생성합니다.

    **public**: 초기화 당시에는 존재하지 않는 폴더이지만, `hexo generate` 명령어를 통해 생성이 되는 폴더입니다. 실제로 배포되어 렌더링 될 정적 파일들이 복사되어 위치하는 곳입니다.

<br>
<br>

4. **_Hexo server 실행_**
    
    hexo 프로젝트 폴더로 이동한 후에 다음 명령어를 실행합니다.

    `hexo server`
    
    이제, `localhost:4000`에 접속하면 블로그 화면을 볼 수 있습니다.

<br>
<br>

5. **_Github Pages와 연동_**

    Hexo의 _config.yml 파일을 열어 최하단 부분의 deploy 설정을 추가한 후 저장해 줍니다.

    ```
    deploy:
      type: git
      repo: https://github.com/<깃헙 아이디>/<깃헙 아이디>.github.io.git
      branch: master
    ```
   
    설정이 완료되었으면, 다음 명령어를 실행합니다.
      
    `hexo generate`
    `hexo deploy`

    빌드하고 배포하는 시간(30초 ~ 1분)을 기다린 후에, `<깃헙 아이디>.github.io`에 접속하면 `localhost:4000`에 접속하여 확인했던 블로그와 동일한 화면을 볼 수 있습니다. 

