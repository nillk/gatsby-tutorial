[2. Introduction to styling in Gatsby](https://www.gatsbyjs.org/tutorial/part-two/)

이 파트에선 Gatsby 사이트를 스타일링하기 위한 옵션들과 사이트를 구성하기 위한 React components를 사용하는 방법을 더 깊이 알아볼 것

## Using global styles

모든 사이트는 global style같은 것을 가지고 있는데, 이건 사이트의 typography나 배경색 같은 것을 가진다. 이런 스타일들은 사이트의 전반적인 느낌을 결정한다. 벽의 색과 질감의 방의 전반적인 느낌을 결정하는 것과 유사하게

## Creating global styles with standard css files

사이트의 global style을 추가하는 가장 간단한 방법 중 하나는 global *.css* stylesheet를 사용하는 것이다.

### Create a new Gatsby site

새로 Hello World 스타터를 이용해 Gatsby 사이트를 만들어보자.

### Add styles to a css file

1. *src/styles/global.css* 파일을 생성하자. *styles* 디렉터리는 임의로 정한 것이다.
2. *global.css* 파일에 스타일을 지정해보자

    ```css
    html {
        background-color: lavenderblush;
    }
    ```

### Include the stylesheet in *gatsby-browser.js*

1. 루트 경로에 *gatsby-browser.js* 파일을 생성한다.
*gatsby-browser.js*는 Gatsby가 찾고, 사용하는(만약 있다면) 몇 안 되는 특별한 파일 중 하나이다. 여기서, 파일의 이름이 중요하다. 더 알고 싶다면 [Gatsby Browser APIs](https://www.gatsbyjs.org/docs/browser-apis/)
2. stylesheet 파일을 *gatsby-browser.js* 파일에서 import 한다.

    ```javascript
    import "./src/styles/global.css"
    
    // or
    // require('./src/styles/global.css')
    ```

3. 서버를 재시작해보면 `lavenderblush` 배경색이 지정된 것을 확인할 수 있다.

💡 여기선 Gatsby 사이트를 스타일링하기 위한 빠르고 쉬운 방법(*gatsby-browser.js* 파일을 이용해 CSS파일을 직접 import)을 택했는데, 대부분의 경우 global style을 적용하기 위한 제일 좋은 방법은 shared layout component와 함께 쓰는 것이다. [참고](https://www.gatsbyjs.org/docs/creating-global-styles/#how-to-add-global-styles-in-gatsby-with-standard-css-files)

## Using component-scoped CSS

지금까지, 우리는 표준 css 스타일시트를 사용하는 전통적인 접근법에 대해 얘기했다. 이제 component 중심의 스타일링을 다루기 위해 CSS를 모듈화하는 다양한 방법에 대해 알아보겠다.

## Styling using CSS Modules

[CSS Module 홈페이지](https://github.com/css-modules/css-modules)에서 인용

> A CSS Module is a CSS file in which all class names and animation names are scoped locally by default

CSS Modules은 CSS를 더욱 안전하게 일반적으로 작성할 수 있게 해줘서 몹시 유명. 이 툴은 자동으로 unique한 클래스와 애니메이션 이름을 생성해주기 때문에, selector 이름 충돌을 걱정할 필요가 없다.

Gatsby는 CSS Modules로 즉시 작업한다. 이 접근법은 Gatsby(일반적으로 React)를 처음 사용하는 사람들에게 매우 추천된다.

### Building a new page using CSS Modules

이 섹션에선 새로운 page를 만들고, CSS Module을 이용해 page component를 style할 것이다.

먼저, 새로운 `Container` component를 만들자.

1. *src/components/container.js* 파일을 만들고, 아래 코드를 입력하자.

    ```javascript
    import React from "react"
    import containerStyles from "./container.module.css"
    
    export default ({ children }) => (
        <div className={containerStyles.container}>{children}</div>
    )
    ```

    *container.module.css* 라는 이름의 css module 파일을 import했다는 걸 알 수 있다. 파일을 만들자.

2. *src/components/container.module.css* 파일을 만들고, 아래 코드를 입력하자.

    ```javascript
    .container {
        margin: 3rem auto;
        max-width: 600px;
    }
    ```

    파일이 *.css* 대신 .*module.css* 로 끝나는 것을 볼 수 있는데, 이건 Gatsby에게 CSS Module로 처리되어야 하는 파일이라고 알려주는 것이다.

3. *src/pages/about-css-modules.js* 파일을 생성해서 새로운 페이지를 만들자.

    ```javascript
    import React from "react"
    
    import Container from "../components/container"
    
    export default () => (
        <Container>
        <h1>About CSS Modules</h1>
        <p>CSS Modules are cool</p>
        </Container>
    )
    ```

    이제 [http://localhost:8000/about-css-modules/](http://localhost:8000/about-css-modules/) 로 접속해보자.

### Style a component using CSS Modules

이 섹션에선 이름, 아바타 그리고 짧은 소개로 이루어진 사람의 목록을 만들 것이다. `<User />` component를 만들고, CSS module을 사용해 style 하자.

1. CSS를 위해 *src/pages/about-css-modules.module.css* 파일을 만들자.
2. 아래 코드를 붙여넣자.

    ```css
    .user {
        display: flex;
        align-items: center;
        margin: 0 auto 12px auto;
    }
    
    .user:last-child {
        margin-bottom: 0;
    }
    
    .avatar {
        flex: 0 0 96px;
        width: 96px;
        height: 96px;
        margin: 0;
    }
    
    .description {
        flex: 1;
        margin-left: 18px;
        padding: 12px;
    }
    
    .username {
        margin: 0 0 12px 0;
        padding: 0;
    }
    
    .excerpt {
        margin: 0;
    }
    ```

3. 아래와 같이 윗부분의 몇 줄을 수정해서 새로운 *src/pages/about-css-modules.module.css* 파일을 *about-css-modules.js*파일로 import하자.

    ```javascript
    import React from "react"
    import styles from "./about-css-modules.module.css"
    import Container from "../components/container"
    
    console.log(styles)
    ```

    `console.log(styles)`는 import의 결과를 보여준다. 그래서 당신은 *./about-css-modules.module.css* 파일이 처리된 결과를 개발자 콘솔에서 볼 수 있다.

    [](https://www.notion.so/54abc15d4895426aa671fe937fab47a0#dd9aa36e86ef40c9a4bd60ffa87c5558)

    CSS 파일과 비교해보면, 각각의 클래스가 긴 string을 가리키는 key임을 확인할 수 있다. 즉, `avatar`는 `about-css-modules-module--avatar--2lRF7`를 가리킨다. 이것들은 CSS Modules이 생성한 class 이름이다. 이것들은 전체 사이트를 통틀어 unique함을 보장한다. 그리고 class를 사용하기 위해선 import 해야 하므로, 어떤 CSS가 어디에서 사용되고 있는지에는 의심의 여지가 없다.

4. `User` component를 만들자.

    *about-css-modules.js* page component파일 내부에 `<User />` inline component를 만들자.

    ```javascript
    import React from "react"
    import styles from "./about-css-modules.module.css"
    import Container from "../components/container"

    console.log(styles)

    const User = props => (
        <div className={styles.user}>
        <img src={props.avatar} className={styles.avatar} alt="" />
        <div className={styles.description}>
            <h2 className={styles.username}>{props.username}</h2>
            <p className={styles.excerpt}>{props.excerpt}</p>
        </div>
        </div>
    )

    export default () => (
        <Container>
        <h1>About CSS Modules</h1>
        <p>CSS Modules are cool</p>
        <User
            username="Jane Doe"
            avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
            excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
        />
        <User
            username="Bob Smith"
            avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
            excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
        />
        </Container>
    )
    ```

    일반적으로, component가 사이트의 여러 곳에서 쓰인다면 *components* 디렉터리의 모듈 파일에 작성되어야 하지만, 하나의 파일 내에서 사용된다면 inline으로 생성해도 된다.

## Styling using CSS-in-JS

CSS-in-JS는 component-oriented styling 접근법이다. 가장 일반적으로, [JavaScript를 이용해 CSS를 인라인](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js)으로 구성하는 하나의 패턴이다.

### Using CSS-in-JS with Gatsby

많은 여러가지 CSS-in-JS 라이브러리가 있고, 대부분은 Gatsby plugin을 가지고 있다. 여기서 CSS-in-JS tutorial을 다루진 않을 것이고, 다만 [여기](https://www.gatsbyjs.org/docs/styling/)서 ecosystem이 무엇을 제공하는지 확인해보길 권한다. 특히 [Gramor](https://www.gatsbyjs.org/docs/glamor/)와 [Styled Components](https://www.gatsbyjs.org/docs/styled-components/) 두 라이브러리에 대한 가벼운 tutorial이 있다.

### Suggested reading on CSS-in-JS

If you’re interested in further reading, check out [Christopher “vjeux” Chedeau’s 2014 presentation that sparked this movement](https://speakerdeck.com/vjeux/react-css-in-js) as well as [Mark Dalgleish’s more recent post “A Unified Styling Language”](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

## Other CSS options

Gatsby 는 거의 대부분의 가능한 styling 옵션을 제공한다. (만약, plugin이 아직 없다면 [contribute](https://www.gatsbyjs.org/contributing/how-to-contribute/) 해줘 🤗)

- [Typography.js](https://www.gatsbyjs.org/packages/gatsby-plugin-typography/)
- [Sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/)
- [Emotion](https://www.gatsbyjs.org/packages/gatsby-plugin-emotion/)
- [JSS](https://www.gatsbyjs.org/packages/gatsby-plugin-jss/)
- [Stylus](https://www.gatsbyjs.org/packages/gatsby-plugin-stylus/)

and more!