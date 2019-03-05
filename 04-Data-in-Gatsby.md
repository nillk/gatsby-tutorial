# [4. Data in Gatsby](https://www.gatsbyjs.org/tutorial/part-four/)

네번째 파트에 온 것을 환영! 🤗 절반 왔음! 편안하게 느끼기 시작했길 바래!

## Recap of first half of the tutorial

지금까지, React.js를 어떻게 사용하는지를 배웠다. 웹사이트를 위한 사용자 정의 building blocks같은 당신 *자신만의* component를 만들 수 있다는 게 얼마나 강력한지!

그리고 또 CSS Modules로 component를 꾸미는 방법도 알아봤다.

### What's in this tutorial?

튜토리얼의 이 다음 네 개의 파트(현재 파트를 포함)에서는 Markdown, WordPress, headless CMSs, 그리고 어떤 다른 데이터 소스에서든 쉽게 사이트를 구성할 수 있게 해주는 Gatsby의 강력한 기능, data layer를 파볼 것!

**NOTE**: Gatsby의 data layer는 GraphQL을 기반으로 움직인다. GraphQL에 대한 더 깊이있는 튜토리얼을 원한다면, [How to GraphQL](https://www.howtographql.com/)을 추천

## Data in Gatsby

웹사이트는 HTML, CSS, JS 그리고 Data 네 개의 부분을 가진다. 튜토리얼의 앞의 반절은 앞의 세 부분에 중점을 뒀다. 이제, Gatsby 사이트에서 Data를 어떻게 사용하는지 배워보장

*What is data?*

컴퓨터 사이언스적인 대답은 아마: 데이터는 `"strings"`, integers(`42`), objects(`{pizza: true}`), 등등 같은 것이다.

Gatsby에서 사용하기 위한 목적으로는, *"React component 외부에 사는 모든 것"*이 더 유용한 대답일 것이다.

지금까지, 당신은 components에 *직접* 글을 쓰고, 이미지를 추가했다. 그건 많은 웹사이트를 만드는 *훌륭한* 방법이다. 하지만 종종 데이터를 component 밖에 저장하거나 필요할 때 데이터를 component 안으로 가져오고 싶을 것이다.

만약 WordPress(다른 기여자들이 컨텐츠를 추가하고 유지하기 위한 좋은 인터페이스를 가지게 되겠지!)와 Gatsby를 이용해 사이트를 만든다면, 사이트를 위한 데이터(pages and posts)는 WordPress에 있을 것이고, 당신은 필요에 따라 데이터를 당신의 component로 *pull*할 것이다.

데이터는 Markdown, CSV, 그외 등등 파일에도 있을 수 있다. 데이터베이스들과 모든 종류의 APIs이 그러하듯이

**Gatsby의 data layer는 이것들(그리고 어떤 다른 source들)로부터 데이터를 당신의 component로 바로 당겨올 수 있게 해준다** - 당신이 원하는 형태로

## Using Unstructured Data vs GraphQL

### 데이터를 Gatsby 사이트로 당겨오기 위해 꼭 GraphQL과 source plugin을 사용해야 할까?

물론 아님! GraphQL의 data layer를 통하지 않더라도, node의 `createPages` API를 사용해 비정형 데이터를 Gatsby 페이지로 바로 가져올 수 있다. 이건 작은 사이트들에 굉장히 좋은 선택이고, GraphQL과 souce plugin은 더 복잡한 사이트에서 시간을 아끼도록 도와줄 수 있다.

[GraphQL없이 Gatsby 사용하기](https://www.gatsbyjs.org/docs/using-gatsby-without-graphql/) 가이드를 보면 어떻게 node `createPages` API를 이용해 데이터를 Gatsby 사이트로 불러오는 지를 배울 수 있고 예제 사이트도 확인할 수 있다!

### 비정형 데이터 vs GraphQL 언제 사용해야 할까?

만약 작은 사이트를 만든다면, 그걸 만드는 하나의 효과적인 방법은 이 가이드에 설명된대로 `createPages` API를 이용해 비정형 데이터를 당겨오는 것이고, 만약 사이트가 후에 점점 더 복잡해지거나, 당신이 복잡한 사이트를 만들게 됐다거나, 당신의 데이터를 옮기고 싶어지면 아래의 단계를 따라해:

1. [Plugin Library](https://www.gatsbyjs.org/plugins/)에서 당신이 원하는 source plugins 그리고/혹은 transformer plugins이 있는지 확인
2. 만약 없다면, [Plugin Authoring](https://www.gatsbyjs.org/docs/plugin-authoring/) 가이드를 읽고 당신이 스스로 만드는 걸 고려해봐! 🤯

### Gatsby의 data layer가 데이터를 component로 가져오기 위해 어떻게 GraphQL을 사용하지

React components에 데이터를 적재하는 많은 옵션이 있다. 가장 유명하고 강력한 하나는 GraphQL이라고 불리는 기술이다.

GraphQL은 Facebook에서 제품 개발자가 필요한 데이터를 component로 당기는 것을 돕기 위해 만들어졌다.

Graph**QL**은 **q**uery **l**anguage이다. 만약 당신이 SQL에 익숙하다면, 그건 매우 유사한 방식으로 동작할 것이다. 특별한 문법을 사용해서 component에 있길 원하는 데이터를 묘사하면 데이터는 당신에게 주어질 것이다.

Gatsby는 components가 그들에게 필요한 데이터를 선언할 수 있도록 만들기 위해 GraphQL을 사용한다.

## Create a new example site

이 파트에서의 튜토리얼을 위해 또다른 새 사이트를 만들자. 당신은 "Pandas Eating Lots"라는 마크다운 블로그를 만들게 될 것이다. 그건 판다들이 많은 음식을 먹는 사진과 비디오를 뽐내는 데 블로그인데, 그러면서 당신은 GraphQL과 Gatsby의 마크다운 서포트에 발을 담그게 될 것이다.

새로운 터미널을 열고 *tutorial-part-four* 디렉터리에 새로운 Gatsby 사이트를 만들기 위해 아래 명령어를 치자. 그리고 새로운 디렉터리로 옮기자:

```bash
npx gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

그리고 프로젝트의 최상위 디렉터리에 또 다른 필요한 디펜던시들을 설치하자. Typography 테마 "Kirkham"을 사용할 것이고, CSS-in-JS library "[Emotion](https://emotion.sh/)"을 시도해볼 것이다.

```bash
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```

세번째 파트에서 만들었던 것과 비슷한 사이트를 세팅한다. 이 사이트는 layout component와 두 개의 page component를 가질 것이다:

*src/components/layout.js*
```javascript
import React from "react"
import { css } from "@emotion/core"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
    <div
        css={css`
            margin: 0 auto;
            max-width: 700px;
            padding: ${rhythm(2)};
            padding-top: ${rhythm(1.5)};
        `}>
        <Link to={`/`}>
            <h3
            css={css`
                margin-bottom: ${rhythm(2)};
                display: inline-block;
                font-style: normal;
            `}>
            Pandas Eating Lots
            </h3>
        </Link>
        <Link
            to={`/about/`}
            css={css` float: right; `}>
            About
        </Link>
        {children}
    </div>
)
```

*src/pages/index.js*

```javascript
import React from "react"
import Layout from "../components/layout"

export default () => (
    <Layout>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
        <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
        />
    </div>
    </Layout>
)
```

*src/pages/about.js*

```javascript
import React from "react"
import Layout from "../components/layout"

export default () => (
    <Layout>
        <h1>About Pandas Eating Lots</h1>
        <p>
            We're the only site running on your computer dedicated to showing the best
            photos and videos of pandas eating lots of food.
        </p>
    </Layout>
)
```

*src/utils/typography.js*

```javascript
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

*gatsby-config.js* (프로젝트의 최상위 디렉터리)

```javascript
module.exports = {
    plugins: [
        `gatsby-plugin-emotion`,
        {
            resolve: `gatsby-plugin-typography`,
            options: {
                pathToConfigModule: `src/utils/typography`,
            },
        },
    ],
}
```

위의 파일들을 추가하고 `npm run develop`로 실행해보자, 평소와 같이 아래 같은 것을 볼 수 있어야 한다:

[사이트 캡처]

레이아웃과 두 페이지로 이루어진 또 다른 작은 사이트를 만들었다.

이제 querying을 시작할 수 있다 😋

## Your first GraphQL query

사이트를 만들 때, 아마도 일반적인 데이터들을 재사용하고 싶을 것이다 - 예를 들어 사이트 제목 같은 것. */about/* 페이지를 보자.  *Pandas Eating Lots*라는 사이트 제목은 layout component(사이트 제목) 및 *about.js* 페이지의 `<h1 />`(페이지 제목) 모두에 있는 것을 알 수 있다.

만약 나중에 당신이 사이트 제목을 변경하고 싶다면? 당신은 모든 components에서 제목을 찾아내고 각각을 편집해야 한다. 이건 복잡하고 불편하며 오류가 발생하기도 쉽다. 크고 복잡한 사이트에서는 더더욱. 대신 제목을 한 곳에 저장하고 다른 파일들에선 그 위치를 참조할 수 있다; 제목은 한 곳에서 변경하고, Gatsby는 변경된 제목을 가져다 그걸 참조하는 파일들에 넣을 것이다.

이런 일반적인 데이터의 위치는 *gatsby-config.js*파일의 `siteMetadata` object이다. 사이트 제목을 *gatsby-config.js* 파일에 넣자:

```javascript
module.exports = {
    siteMetadata: {
        title: `Title from siteMetadata`,
    },
    plugins: [
        `gatsby-plugin-emotion`,
        {
            resolve: `gatsby-plugin-typography`,
            options: {
                pathToConfigModule: `src/utils/typography`,
            },
        },
    ],
}
```

개발 서버를 재시작하자

### Use a page query

이제 사이트 제목을 query할 수 있다; [page query](https://www.gatsbyjs.org/docs/page-query)를 이용해서 *about.js* 파일에 넣자:

```javascript
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => (
    <Layout>
        <h1>About {data.site.siteMetadata.title}</h1>
        <p>
            We're the only site running on your computer dedicated to showing the best
            photos and videos of pandas eating lots of food.
        </p>
    </Layout>
)

export const query = graphql`
    query {
        site {
            siteMetadata {
                title
            }
        }
    }
`
```

작동한다! 🎉

위에서 제목을 우리의 *about.js*로 받아와 변경하는 기본 GraphQL 쿼리:

```graphql
{
    site {
        siteMetadata {
            title
        }
    }
}
```

💡 [다섯번째 파트](https://www.gatsbyjs.org/tutorial/part-five/#introducing-graphiql)에서는 우리가 GraphQL을 통해 이용할 수 있는 데이터를 대화식으로 탐색하고, 위와 같은 쿼리를 작성할 수 있게 도와주는 도구를 알게 될 것이다.

페이지 쿼리는 페이지 component 파일의 가장 끝에 위치하는 관례에 따라 component 정의의 외부에 있다. 그리고 오직 페이지 component에서만 사용할 수 있다.

### Use a StaticQuery

[StaticQuery](https://www.gatsbyjs.org/docs/static-query/)는 Gatsby v2에서 소개된 새로운 API로 (우리의 *layout.js* component처럼) non-page components가 GraphQL 쿼리들을 통해 데이터를 받아올 수 있게 한다.

먼저 `<StaticQuery />`를 *src/components/layout.js*파일에 추가하고, `{data.site.siteMetadata.title}` 참조를 이 데이터를 사용하는 곳에 추가하자. 다 하면 아래와 같을 것:

```javascript
import React from "react"
import { css } from "@emotion/core"
import { StaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
    <StaticQuery
        query={graphql`
            query {
                site {
                    siteMetadata {
                        title
                    }
                }
            }
        `}

        render={data => (
            <div
                css={css`
                    margin: 0 auto;
                    max-width: 700px;
                    padding: ${rhythm(2)};
                    padding-top: ${rhythm(1.5)};
                    `}>
                <Link to={`/`}>
                    <h3
                        css={css`
                            margin-bottom: ${rhythm(2)};
                            display: inline-block;
                            font-style: normal;
                            `}>
                        {data.site.siteMetadata.title}
                    </h3>
                </Link>
                <Link
                    to={`/about/`}
                    css={css` float: right; `}>
                About
                </Link>
                {children}
            </div>
        )}
    />
)
```

꺅! 🎉

왜 여기서 두 개의 다른 쿼리를 사용했을까? 이 예제들은 query 유형들, query들이 어떻게 format되는지, 어디서 사용될 수 있는지 대한 빠른 소개였다. 우선은 페이지만이 페이지 쿼리들을 사용할 수 있다고 기억하자. Layout같은 non-page components는 StaticQuery를 사용할 수 있다. 튜토리얼의 [일곱번째 파트](https://www.gatsbyjs.org/tutorial/part-seven/)에서 이것들을 더 깊게 설명한다.

실제 제목을 되살리자!

Gatsby의 핵심 원칙 중 하나는 *창작자들이 그들이 만들고 있는 것에 즉시 연결되어야 한다*는 것이다. ([hat tip to Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/)) 다른 말로, 코드에 어떤 변경을 했을 경우 즉시 변경의 영향을 확인할 수 있어야 한다. Gatsby의 입력을 조작하면, 새로운 출력이 화면에 나타나는 것을 볼 수 있다.

그래서 거의 모든 곳에서, 당신이 만든 변화는 즉시 효력을 발휘한다. *gatsby-config.js* 파일을 다시 편집하자. 이번엔 `title`을 다시 "Pandas Eating Lots"로 되돌리자. 변화는 당신의 사이트에서 매우 빠르게 보여져야 한다.