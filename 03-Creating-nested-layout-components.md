# [3. Creating nested layout components](https://www.gatsbyjs.org/tutorial/part-three/)

여기선 Gatsby plugin에 대해 배우고, *layout components*를 만들어볼 것!

Gatsby plugins은 Gatsby 사이트에 기능을 추가할 수 있도록 도와주는 JavaScript package이다. Gatsby는 확장 가능하도록 설계되었고, 다시 말해 plugins은 Gatsby가 할 수 있는 모든 것을 확장하고 수정할 수 있다는 얘기이다.

Layout components는 여러 페이지에서 공유하려는 사이트의 섹션을 위한 것이다. 예를 들어, 사이트는 일반적으로 공유된 header나 footer를 layout component로 가진다. 레이아웃에 추가할 다른 공통적인 것들은 sidebar나 navigation menu가 있다. 예를 들어 이 페이지 상단의 header는 [gatsbyjs.org](http://gatsbyjs.org) layout component의 일부이다.

파트 3 시작! 😎

## Using Gatsby plugins

당신은 아마 plugin이라는 개념에 익숙할 것이다. 많은 소프트웨어 시스템들이 새로운 기능을 추가하거나 심지어 소프트웨어의 핵심적인 동작을 수정할 수 있도록 custom plugin을 추가하는 걸 지원한다. Gatsby plugin도 같은 방식으로 동작한다.

커뮤니티 구성원(당신같은!)은 다른 사람들이 Gatsby 사이트를 만들 때 사용할 수 있도록 plugins(작은 JavaScript 코드)에 기여할 수 있다.

> 이미 수많은 plugins이 있다! Gatsby의 [Plugin Library](https://www.gatsbyjs.org/plugins/)를 살펴봐!

Plugin을 쉽게 설치하고 사용하게 하는 게 우리의 목적이다. 당신이 만드는 거의 모든 Gatsby 사이트의 당신은 plugin을 사용하게 될 것이다. 나머지 튜토리얼을 진행하는 동안 plugin을 설치하고 사용하는 연습을 할 많은 기회가 있을 것이다.

가장 처음으로 plugin을 사용에 대한 소개를 위해, Typography.js를 위한 Gatsby plugin을 설치하고 실행해볼 것이다.

[Typography.js](https://kyleamathews.github.io/typography.js/)는 사이트의 typography를 위한 전역 기반 스타일을 생성하는 JavaScript 라이브러리이다. 이 라이브러리는 Gatsby 사이트에서의 사용을 간소화하기 위해 [대응되는 Gatsby plugin](https://www.gatsbyjs.org/packages/gatsby-plugin-typography/)을 가지고 있다.

### Create a new Gatsby site

두 번째 섹션에서 언급했듯이, 여기선 새로운 Gatsby 프로젝트를 생성해서 사용하자

### Install and configure `gatsby-plugin-typography`

Plugin을 사용하기 위해선 2가지의 주요 단계가 있다: *설치*와 *설정*

1. `gatsby-plugin-typography` npm package를 설치한다.

    ```bash
    npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
    ```

    Note: Typography.js는 몇 가지 추가적인 package들을 요구하기 때문에 명령어에 포함되어 있다. 이처럼 추가적인 요구 사항은 각 plugin의 install 설명에 리스트될 것이다.

2. 프로젝트의 root 디렉터리에 *gatsby-config.js* 파일을 생성하고, 아래 코드를 붙여넣자.

    ```javascript
    module.exports = {
        plugins: [
            {
                resolve: `gatsby-plugin-typography`,
            options: {
                    pathToConfigModule: `src/utils/typography`,
            },
            },
        ],
    }
    ```

    *gatsby-config.js*는 Gatsby가 자동으로 인식하는 또다른 특별한 파일이다. 여기에 plugin이나 다른 site configuration을 추가할 수 있다. [gatsby-config.js 문서](https://www.gatsbyjs.org/docs/gatsby-config/) 확인

3. *src/utils/typography.js* 설정 파일 추가

    Typography.js는 설정 파일을 필요로 한다. 추가하자.

    ```javascript
    import Typography from "typography"
    import fairyGateTheme from "typography-theme-fairy-gates"
    
    const typography = new Typography(fairyGateTheme)
    
    export const { scale, rhythm, options } = typography
    export default typography
    ```

4. 개발 서버 시작

    ```bash
    npm run develop
    ```

    사이트를 로드하고 Chrome 개발자 도구를 이용해 생성된 HTML을 확인하면, typography plugin이 `<head>` element에 생성된 CSS와 함께 `<style>` element를 추가한 것을 볼 수 있을 것이다.

### Make some content and style changes

아래 코드를 *src/pages/index.js*에 붙여넣으면 Typography.js가 생성한 CSS의 효과를 확인할 수 있다.

```javascript
import React from "react"

export default () => (
    <div>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
        What do I like to do? Lots of course but definitely enjoy building
        websites.
    </p>
    </div>
)
```

빨리 개선 해보자. 많은 사이트들은 페이지의 중간에 한 열의 텍스트 블록을 가지고 있다. 이걸 만들기 위해서, 아래 style 코드를 *src/pages/index.js*의 `<div>`에 넣어 보자.

```javascript
import React from "react"

export default () => (
    <div style={{ margin: `3rem auto`, maxWidth: 600}}>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
        What do I like to do? Lots of course but definitely enjoy building
        websites.
    </p>
    </div>
)
```

좋아! 당신은 처음으로 Gatsby plugin을 설치하고 설정했다! 🤓

## Creating layout components

이제 layout components를 배워보자. 이 파트를 준비하기 위해서 프로젝트에 몇 개의 파일을 추가하자: about 페이지와 contact 페이지

*src/pages/about.js*

```javascript
import React from "react"

export default () => (
    <div>
    <h1>About me</h1>
    <p>I'm good enough, I'm smart enough, and gosh darn it, people like me!</p>
    </div>
)
```

*src/pages/contact.js*

```javascript
import React from "react"

export default () => (
    <div>
    <h1>I'd love to talk! Email me at the address below</h1>
    <p>
        <a href="mailto:me@example.com">me@example.com</a>
    </p>
    </div>
)
```

새로운 페이지들이 어떤 모습인지 살펴보자:

음. 두 개의 새로운 페이지의 내용도 *index* 페이지처럼 가운데 있으면 좋을 것 같다. 그리고 방문자들이 쉽게 하위 페이지들을 찾고 방문할 수 있도록 일종의 전역 navigation도 있으면 좋겠다.

당신은 첫 번째 layout component를 만들어서 이런 변경 사항들을 해결할 것이다.

### Create your first layout component

1. 새 디렉터리 *src/components*를 만들자
2. 가장 기본적인 layout component를 *src/components/layout.js*에 만들자

    ```javascript
    import React from "react"
    
    export default ({ children }) => (
        <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
        {children}
        </div>
    )
    ```

3. 새로운 layout component를 *src/pages/index.js* 페이지에 import 하자

    ```javascript
    import React from "react"
    import Layout from "../components/layout"
    
    export default () => (
        <Layout> 
        <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
        <p>
            What do I like to do? Lots of course but definitely enjoy building
            websites.
        </p>
        </Layout>
    )
    ```

    꺅! layout이 작동한다! index 페이지의 내용은 여전히 한 가운데 나타난다.

    하지만 */about/*이나 */contact/*로 이동하면 이 페이지들의 내용은 여전히 가운데에 있지 않다.

4. layout component를 *about.js*와 *contact.js*에 import 하자 (이전 단계에서 *index.js*에 했던 것처럼)

    세 개의 페이지의 내용물이 모두 가운데 나타난다! 이 공유된 단일 layout component에 감사하자! 😇

### Add a site title

1. 아래 한 줄(`<h3>MySweetStie</h3>`)을 layout component에 추가:

    *src/components/layout.js*

    ```javascript
    import React from "react"
    
    export default ({ children }) => (
        <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
        <h3>MySweetSite</h3>
        {children}
        </div>
    )
    ```

    세 개의 페이지 중 아무 것이나 가도 같은 제목이 추가되어 있는 것을 볼 수 있을 것이다.

### Add navigation links between pages

1. 아래 코드를 복사해 *src/components/layout.js* 파일의 layout component에 추가하자

    ```javascript
    import React from "react"
    import { Link } from "gatsby"
    const ListLink = props => (
        <li style={{ display: `inline-block`, marginRight: `1rem` }}>
        <Link to={props.to}>{props.children}</Link>
        </li>
    )
    
    export default ({ children }) => (
        <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
        <header style={{ marginBottom: `1.5rem` }}>
            <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
            <h3 style={{ display: `inline` }}>MySweetSite</h3>
            </Link>
            <ul style={{ listStyle: `none`, float: `right` }}>
            <ListLink to="/">Home</ListLink>
            <ListLink to="/about/">About</ListLink>
            <ListLink to="/contact/">Contact</ListLink>
            </ul>
        </header>
        {children}
        </div>
    )
    ```

    기본적인 전역 navigation을 가진 세 개의 페이지가 생긴 걸 봐!

    *Challenge:* 새로운 *layout component*로 당신의 Gatsby 사이트에 headers, footers, global naviagtion, sidebars 등등을 추가하도록 해보자!