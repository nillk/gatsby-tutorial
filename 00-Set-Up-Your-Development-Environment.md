# [0. Set Up Your Development Environment](https://www.gatsbyjs.org/tutorial/part-zero/)

첫번째 Gatsby 사이트를 만들기 전에 몇 가지 핵심적인 웹 기술들과 스스로 익숙해질 필요가 있고, 필요한 소프트웨어들이 설치되어 있어야 한다.

## Overview of core technologies

벌써 이것들에 대해 전문가일 필요는 없다 - 만약 아니라면, 걱정 마! 이 튜토리얼 시리즈를 통해 많은 것을 알게 될 것이다. 이것들은 개츠비 사이트를 만들 때 사용할 몇 가지 주요 웹 기술들이다:

- HTML: 모든 웹 브라우저가 이해할 수 있는 마크업 언어로 HyperText Markup Language를 나타낸다. HTML은 웹 컨텐트에 제목, 문단, 그리고 그 밖에 것들을 정의하는 보편적인 정보 구조를 제공한다.
- CSS: 웹 컨텐트의 모양(폰트, 색상, 레이아웃 등등)을 스타일링하는 데 사용되는 표현적인 언어로 Cascading Style Sheets를 나타낸다.
- JavaScript: 웹을 동적이고 상호작용하게 만들 수 있도록 도와주는 프로그래밍 언어
- React: UI를 구성하기 위해 JS로 만들어진 library로 Gatsby가 page들과 구조화된 content를 만들기 위해 사용
- GraphQL: 쿼리 언어. 데이터를 사이트로 끌어오게 해주는 프로그래밍 언어. Gatsby가 site data를 관리하기 위해 사용하는 인터페이스

💡(Optional!) 웹사이트가 무엇인지에 대한 개괄적인 소개 - HTML과 CSS에 대한 소개 포함 - 는 [Building your first web page](https://learn.shayhowe.com/html-css/building-your-first-web-page/) 참조. 웹에 대해 학습을 시작하기 좋은 곳이다. 더 많은 [HTML](https://www.codecademy.com/learn/learn-html), [CSS](https://www.codecademy.com/learn/learn-css), [JavaScript](https://www.codecademy.com/learn/introduction-to-javascript)를 *직접 다뤄볼 수 있는* 소개는 Codecademy 튜토리얼을 참조하자. [React](https://reactjs.org/tutorial/tutorial.html) 그리고 [GraphQL](http://graphql.org/graphql-js/) 역시 튜토리얼이 있다.

## Familiarize yourself with the command line

command line은 컴퓨터에서 명령어들을 실행하기 위해 사용되는 텍스트 기반 인터페이스이다. 당신은 또한 종종 그것이 터미널로 지칭되는 것을 볼 것이다. 이 튜토리얼에선 둘 다 번갈아가며 사용할 것이다. 맥에서 Finder를 사용하거나 windows에서 탐색기를 사용하는 것과 매우 유사하다. Finder와 탐색기는 Graphical User Interface (GUI)의 예시이다. command line은 컴퓨터와 상호작용하기 위한 텍스트 기반의 강력한 방법이다.

잠시 시간을 내서 컴퓨터의 command line interface(CLI)를 찾아 열어 보자. 어떤 운영 체제를 사용하느냐에 따라 [instructions for Mac](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/)이나 [instruction for Windows](https://www.quora.com/How-do-I-open-terminal-in-windows)를 보자.

💡command line을 사용하는 데 멋진 소개 [Codecademy's Command Line tutorial](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) (Mac, Linux)을 참고하자. 윈도우 사용자는 [이 튜토리얼](https://www.computerhope.com/issues/chusedos.htm)을 참고하자. 윈도우 사용자라도 Codecademy 튜토리얼의 첫 번째 페이지는 읽어볼만 하다. 단지 Command line를 어떻게 사용하는지에 대해 설명하는 게 아니라 command line이 뭔지 설명한다.

## Install Node.js

Web browser외부에서 JavaScript를 실행할 수 있는 환경으로 Gatsby는 Node.js로 만들어졌다. Gatsby를 시작하고 실행하려면 컴퓨터에 최신 버전이 설치되어 있어야 한다.

Node: Gatsby의 최소 지원 버전은 Node 8이지만 더 최근의 버전을 사용해도 된다.

### Check your Node.js installation

1. 터미널을 연다
2. `node --version` 을 실행하자. (만약 command line이 처음이라면, *명령어 실행*은 `node --version`을 커맨드 프롬프트에 입력하고, Enter 키를 치라는 말이다. 지금부터, 이것이 우리가 말하는 명령어 실행(run command)이다.)
3. `npm --version` 실행

각각의 커맨드들의 출력은 버전 숫자여야 한다. 당신의 버전은 아래 보이는 것과 다를 수 있다! 각각의 커맨드를 입력했는데 버전 정보가 보이지 않는다면, Node.js가 설치되어 있는지 확인해라.

```bash
> node --version
v0.11.3
> npm --version
6.2.0
```

## Familiarize yourself with npm

npm은 JavaScript의 package manager로 package는 프로젝트에 포함시킬 수 있는 코드의 모듈이다. Node.js를 설치하면 npm은 같이 설치되며, npm은 3가지의 구분되는 components를 가지고 있다.

- npm website: 어떤 JavaScript package가 사용 가능한지 npm registry에서 찾아볼 수 있음
- npm registry: npm에서 사용 가능한 JavaScript package의 정보를 가진 큰 데이터 베이스
- npm command line interface: 어떤 package를 사용하려고 마음 먹으면, 다른 CLI 툴처럼, npm CLI를 이용해 프로젝트나 globally하게 설치할 수 있다. npm CLI는 registry와 대화하며 - 당신은 일반적으로 npm 웹 사이트나 npm CLI와만 상호작용 한다.

npm의 소개를 확인해보자. [What is npm?](https://docs.npmjs.com/getting-started/what-is-npm)

## Install Git

Git은 무료이며 오픈 소스이고, 작은 프로젝트부터 아주 큰 프로젝트까지 모든 것을 처리할 수 있도록 고안된 속도와 효율성을 갖춘 분산 버전 관리 시스템이다. Gatsby starter 사이트를 설치하면, Gatsby는 뒤에서 starter에 필요한 파일들을 다운받고 설치하는 데 Git을 사용한다. 첫 번째 Gatsby 사이트를 설치하기 위해 git이 설치할 필요가 있다.

운영체제에 맞는 Git을 다운받고 설치하는 과정은 아래의 가이드를 따르자:

- Install Git on macOS
- Install Git on Windows
- Install Git on Linux

💡이 튜토리얼을 끝내기 위해 Git을 알 필요는 없지만, 그건 매우 유용한 툴이다. 버전 관리, Git 그리고 GitHub에 대해 더 배우고 싶다면 GitHub의 Git Handbook을 참고하자.

## Using the Gatsby CLI

Gatsby CLI는 배포된 npm package로 Gatsby 사이트를 빠르게 생성하고, 개발하기 위한 command를 실행할 수 있게 해준다.

Gatsby CLI는 npm을 통해 사용할 수 있으며, `npm install -g gatsby-cli`를 실행해 global하게 설치되어 있어야 한다.

가능한 명령어를 보려면 `gatsby --help`를 실행하자.

💡 권한 문제 때문에 Gatsby CLI를 성공적으로 실행할 수 없다면, [npm docs on fixing permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions)나 [this guide](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md)를 확인해보자.

## Create a Gatsby site

이제 첫번째 Gatsby 사이트를 만들기 위해 Gatsby CLI툴을 사용할 준비가 됐다. 툴을 사용해, 빠르게 특정 타입의 사이트를 만들 수 있게 도와주는 *스타터* (몇 가지 기본 설정과 함께 부분적으로 구축되어 있는 사이트들)를 다운 받을 수 있다. 여기서 사용할 *Hello World* 스타터는 Gatsby 사이트에 필요한 몇 가지 안되는 핵심적 설정들만 가진 스타터이다.

1. 터미널을 열자
2. `gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world` 를 실행하자. (Note: 다운로드 속도에 따라 걸리는 시간이 다를 것이다.)
3. `cd hello-world` 실행
4. `gatsby develop` 실행

어떤 일이 발생했지?

```bash
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

- `new`는 새로운 Gatsby 프로젝트를 생성하기 위한 gatsby 명령어이다
- `hello-world`는 임의의 제목이다 - 뭐든 선택할 수 있다. CLI 툴은 새로운 사이트를 위한 코드를 *hello-world* 라고 불리는 새로운 폴더에 위치할 것이다.
- 마지막으로, GitHub URL은 사용하고자 하는 스타터 코드를 가지고 있는 코드 저장소를 가리킨다.

```bash
cd hello-world
```

- 이건 '*hello-world* 하위 디렉터리로 디렉터리를 변경(`cd` - change directories)하고 싶다는 얘기'다. 사이트를 위한 어떤 명령어든 실행하고 싶을 때, 사이트 컨텍스트에 위치해 있어야 한다. (터미널이 사이트 코드가 실행되고 있는 디렉터리에 위치해야 한다)

```bash
gatsby develop
```

- 이 명령어는 개발 서버를 시작한다. 개발 환경 - 로컬(당신의 컴퓨터 상에서, 인터넷으로 배포되지 않은) - 에서 새로운 사이트를 보고 상호 작용할 수 있을 것이다.

### View your site locally

브라우저에서 새로운 탭을 열고, [http://localhost:8000](http://localhost:8000) 로 가보자.

축하한다! 당신의 첫번째 Gatsby 사이트의 시작이다! 🎉

개발 서버가 실행되고 있는 동안은 사이트를 로컬에서 [http://localhost:8000](http://localhost:8000) 으로 접속할 수 있다. `gatsby develop` 명령어로 실행으로 시작된 프로세스이다. 실행되고 있는 프로세스를 멈추려면 (실행되고 있는 개발 서버를 멈추려면) 터미널 윈도우로 돌아가서, *control* 키를 누른 상태에서 *c*를 입력하자. (ctrl-c) 다시 시작하려면, `gatsby develop`를 다시 실행하자!

Node: `vagrant`같은 VM 환경을 사용하고 있거나 로컬 IP 주소에서 listen하려면, `gatsby develop -- --host=0.0.0.0`을 실행하자. 이제, 개발 서버는 *localhost*와 로컬 IP 둘 다에서 listen한다.

## Set up a code editor

코드 편집기는 컴퓨터 코드를 편집하기 위해 특별히 고안된 프로그램으로 훌륭한 것들이 많이 있다.

만약 코드 편집기를 사용해본 적이 없다면, [VS Code](https://code.visualstudio.com/)를 추천한다. 단순히 튜토리얼 내내 사용된 캡쳐 화면이 일치하기 때문에 아마 더 따라하기 쉬울 것이기 때문이다.

### Download VS Code

Gatsby 문서는 종종 코드 편집기의 캡쳐 화면을 포함한다; 이런 캡쳐 화면들은 VS Code를 보여주고, 따라서 아직 선호하는 코드 편집기가 없다면, VS Code를 사용하는 것이 당신의 화면이 튜토리얼과 문서의 캡쳐 화면과 동일하게 보이도록 할 것이다. VS Code를 사용하기로 결정했으면, [VS Code site](https://code.visualstudio.com/#alt-downloads)를 방문해 당신의 플랫폼에 맞는 버전을 다운로드 하자.

### Install the Prettier plugin

우리는 [Prettier](https://github.com/prettier/prettier) 역시 사용하기 추천한다. - Prettier는 코드 형식을 일관되게 유지하고 오류를 방지하는 데 도움을 주는 도구이다.

[Prettier VS Code plugin](https://github.com/prettier/prettier-vscode)을 사용해 Prettier를 코드 편집기에서 직접 사용할 수 있다.

1. VS Code에서 extensions view를 연다. (View ⇒ Extensions)
2. "Prettier - Code formatter"를 검색한다.
3. "Install"을 클릭. 설치된 후에는 extension을 활성화하기 위해 VS Code를 재시작 하라는 메시지가 나타날 것이다.

💡 VS Code를 사용하지 않는다면, Prettier 문서의 [install instructions](https://prettier.io/docs/en/install.html)이나 [other editor integrations](https://prettier.io/docs/en/editors.html)를 참고하자.