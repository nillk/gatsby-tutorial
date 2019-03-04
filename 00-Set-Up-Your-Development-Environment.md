# [0. Set Up Your Development Environment](https://www.gatsbyjs.org/tutorial/part-zero/)

> Gatsby를 동작하게 하는 코어 기술을 소개하고, 개발 환경 설정을 안내

## Overview of core technologies

- HTML
- CSS
- JavaScript
- React: UI를 구성하기 위해 JS로 만들어진 library로 Gatsby가 page들과 구조화된 content를 만들기 위해 사용
- GraphQL: Gatsby가 site data를 관리하기 위해 사용하는 인터페이스

## Install Node.js

Web browser외부에서 JavaScript를 실행할 수 있는 환경으로 Gatsby는 Node.js로 만들어졌다. Gatsby의 최소 지원 버전은 Node 8.

## Familiarize yourself with npm

npm은 JavaScript의 package manager로 package는 프로젝트에 포함시킬 수 있는 코드의 모듈이다. Node.js를 설치하면 npm은 같이 설치되며, npm은 3가지의 구분되는 components를 가지고 있다.

- npm website: 어떤 JavaScript package가 사용 가능한지 npm registry에서 찾아볼 수 있음
- npm registry: npm에서 사용 가능한 JavaScript package의 정보를 가진 큰 데이터 베이스
- npm command line interface: 어떤 package를 사용하려고 마음 먹으면, npm CLI를 이용해 프로젝트나 globally하게 설치할 수 있다.

## Using the Gatsby CLI

Gatsby CLI는 배포된 npm package로 Gatsby 사이트를 빠르게 생성하고, 개발하기 위한 command를 실행할 수 있게 해준다. Gatsby CLI를 local로 설치하는 대신 npx를 사용해 실행할 수 있다. 실행할 수 있는 커맨드를 보려면 `npx gatsby —-help`를 사용

> npx: an npm package runner
npm 5.2.0 이후 버전을 설치하면 같이 설치되며, 패키지를 설치하지 않고 실행해볼 수 있다.

## Create a Gatsby site

기본 configuration으로 빌드된 starters 프로젝트를 다운받아 빠르게 사이트를 생성해보자. 여기서는 *Hello World* starter를 사용한다.

```bash
npx gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
cd hello-world
npm run develop  # or npm run develop -- --host=0.0.0.0
```

[*http://localhost:8000*](http://localhost:8000에서)에서 Gatsby 사이트를 확인할 수 있다.

개발 환경을 위해 추가로 git과 code editor의 설치도 필요하다.