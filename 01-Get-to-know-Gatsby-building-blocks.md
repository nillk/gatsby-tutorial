# [1. Get to know Gatsby building blocks](https://www.gatsbyjs.org/tutorial/part-one/)

Gatsby starter를 기반으로 한 새로운 Gatsby 사이트를 생성하기 위해 아래 커맨드를 사용할 수 있다.

```bash
npx gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]
```

## Familiarizing with Gatsby pages

*src/pages/index.js* 파일을 열어보면, 하나의 `div` 안에 `Hello world!`텍스트를 포함하는 component를 생성하는 코드가 있다.

### Make changes to the "Hello World" homepage

1. `Hello world!`를 변경하고 저장하면 거의 바로 브라우저의 Hello world가 다른 내용으로 바뀌는 것을 확인할 수 있다.

    💡 Gatsby는 개발 작업을 빠르게 하기 위해 **hot reloading**을 사용한다. Gatsby development server를 실행하면 Gatsby 사이트 파일은 background에서 *watched*되기 때문에 언제든 파일을 저장하면 변경 내용이 브라우저에 바로 반영된다.

2. *src/pages/index.js*의 코드를 아래 있는 코드로 변경하고 저장해보자. 큰 보라색의 텍스트를 확인할 수 있을 것이다. styling에 대한 더 자세한 내용은 part two에서!

    ```javascript
    import React from "react"
    
    export default () => (
        <div style={{ color: `purple`, fontSize: `72px`}}>Hello Gatsby!</div>
    )
    ```

3. 글씨 크기 설정을 빼고, `Hello Gatsby!`를 level-one header로 변경하고, header 아래에 paragraph를 추가하자.

    ```javascript
    import React from "react"
    
    export default () => (
        <div style={{ color: `purple` }}>
        <h1>Hello Gatsby!</h1>
        <p>What a world.</p>
        </div>
    )
    ```

4. Image를 넣자.

    ```javascript
    import React from "react"
    
    export default () => (
        <div style={{ color: `purple` }}>
        <h1>Hello Gatsby!</h1>
        <p>What a world.</p>
        <img src="https://source.unsplash.com/random/400x200" alt="" />
        </div>
    )
    ```

## Building with components

방금 전까지 편집했던 홈페이지는 *page component*를 정의함으로써 만들어졌다. 그럼 **component**가 정확하게 뭘까?

넓은 의미로 component는 사이트를 위한 building block이다. 그건은 한 구역의 UI를 설명하는 자체 코드(self-contained) 조각이다.

Gatsby는 React위에서 만들어졌다. 우리가 **component**를 사용하고 정의하는 것에 대해 얘기할 때, 그것은 **React components**에 대해 얘기하는 것이다. (대개의 경우 JSX로 작성된) 입력을 받아들이거나, 한 구역의 UI를 설명하는 React elements를 반환하는 독립적인 코드 조각

만약 당신이 개발자라면, components를 이용할 때 하나의 큰 생각 변화가 필요하다. 이제 CSS, HTML, JavaScript는 긴밀하게 coupled되어 있고, 종종 한 파일 내부에 작성된다. 

겉보기에는 단순한 변화지만, 이건 어떻게 웹사이트를 만드는지에 대한 생각에 엄청난 영향을 미친다.

custom 버튼을 만드는 예제를 보자. 과거에는 custom 스타일의 CSS 클래스를 만들고, 적용하길 원할 때마다 아래와 같이 했을 것이다.

```html
<button class="primary-button">Click me</button>
```

components의 세계에서는 대신 style과 함께 `PrimaryButton` component를 만들고, 아래와 같이 사용한다.

```javascript
<PrimaryButton>Click me<PrimaryButton>
```

Components는 웹사이트의 base building blocks이 된다. 브라우저가 제공하는 building block(`<button />`같은 것)으로 제한되는 대신에, 프로젝트의 요구를 우아하게 충족시키는 새로운 building block을 쉽게 만들 수 있다.

💡 [Building with Components](https://www.gatsbyjs.org/docs/building-with-components/) 참고

### Using page components

*src/pages/*.js* 에 정의된 React component는 page가 된다. 우리는 이미 Hello World 페이지를 가지고 있는데, about 페이지를 만들어보자.

1. *src/pages/about.js* 파일을 만들고, 아래 코드를 입력하고 저장하자.

    ```javascript
    import React from "react"
    
    export default () => (
        <div style={{ color: `teal` }}>
        <h1>About Gatsby</h1>
        <p>Such wow. Very React.</p>
        </div>
    )
    ```

2. [http://localhost:8000/about/](http://localhost:8000/about/) 페이지에 들어가보자.

*src/pages/about.js* 파일에 React component를 넣은 것만으로, */about* 으로 접근 가능한 페이지를 얻었다.

### Using sub-components

홈페이지와 about 페이지가 꽤 커지면 많은 코드를 다시 써야 하는데, 그럴 때 UI를 재사용 가능한 조각으로 쪼개주는 *sub-components*를 사용할 수 있다. 두 페이지 모두 `<h1>` 헤더를 가지고 있으니 `Header`를 나타내는 component를 만들어보자.

1. *src/components* 디렉터리를 만들고, *header.js* 파일을 생성하자.
2. 아래의 코드를 *src/components/header.js* 파일에 입력하자.

    ```javascript
    import React from "react"
    
    export default () => <h1>This is a header.</h1>
    ```

3. Header component를 import하게 *about.js* 파일을 수정하고, `h1` 마크업을
    `<Header />`로 변경하자.

    ```javascript
    import React from "react"
    import Header from "../components/header"
    
    export default () => (
        <div style={{ color: `teal` }}>
        <Header />
        <p>Such wow. Very React.</p>
        </div>
    )
    ```

    브라우저에서 *About Gatsby* 텍스트가 *This is a header.*로 변경되었을 것이다. 하지만 당신은 about페이지에 *This is a header.*가 아니라, *About Gatsby*가 표시되길 원할 것이다.

4. *src/components/header.js* 파일로 돌아가서, 아래와 같이 변경하자.

    ```javascript
    import React from "react"
    
    export default props => <h1>{props.headerText}</h1>
    ```

5. *src/pages/about.js* 파일로 돌아가서, 아래와 같이 변경하자.

    ```javascript
    import React from "react"
    import Header from "../components/header"
    
    export default () => (
        <div style={{ color: `teal` }}>
        <Header headerText="About Gatsby" /> 
        <p>Such wow. Very React.</p>
        </div>
    )
    ```

    이제 About Gatsby 헤더가 다시 보일 것!

### What are "props"?

이전에 React components를 UI를 설명하는 재사용 가능한 코드 조각으로 정의했다. 이런 재사용 가능한 조각을 동적으로 만들기 위해서는 다른 데이터를 제공할 수 있어야 한다. 이걸 *props*라고 불리는 입력을 통해 할 수 있다. Props는 React component에 공급되는 속성이다.

*about.js*에서 `headerText` prop를 `About Gatsby`라는 값과 함께 imported된 `Header` sub-component에 넘겼다.

*header.js*에서 `Header` component는 `headerText`라는 prop를 받을 걸 예상하고 있으므로, `props.headerText`로 접근할 수 있다.

💡 JSX에선 어떤 JavaScript 표현식도 `{}`로 싸서 집어넣을 수 있다. `props` 오브젝트에서 `headerText` 프로퍼티로 접근할 수 있는 이유

만약 `<Header />`에 아래와 같이 또다른 prop를 넘기면, `{props.arbitraryPhrase}`로 `arbitraryPhrase` prop에 접근할 수 있을 것이다.

```javascript
<Header headerText="About Gatsby" arbitraryPhrase="is arbitrary" />
```

이게 어떻게 당신의 components를 재사용 가능하게 하는지 강조하기 위해 추가로 `<Header />` component를 about 페이지에 넣어보자. 아래의 코드를 *src/pages/about.js* 파일에 작성하고 저장하자.

```javascript
import React from "react"
import Header from "../components/header"

export default () => (
    <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" /> 
    <Header headerText="It's pretty cool" /> 
    <p>Such wow. Very React.</p>
    </div>
)
```

이제 그 어떤 코드 재작성 없이 props를 이용해 다른 데이터를 넘겨, 두번째 헤더를 가지게 될 것!

### Using layout components

Layout components는 여러 페이지에서 공유하길 원하는 사이트의 구역을 위한 것이다. 예를 들어 Gatsby 사이트는 일반적으로 layout component로 공유된 header와 footer를 가진다. layout에 추가할 다른 일반적인 component로는 sidebar, navigation menu같은 것들이 있다.

[Creating nested layout components](https://www.gatsbyjs.org/tutorial/part-three/)에서 자세히 알아볼 것

## Linking between pages

종종 pages들을 연결하고 싶을 수도 있다. Gatsby 사이트에서의 routing을 알아보자.

### Using the `<Link />` component

1. *src/pages/index.js* 파일을 열자. Gatsby에서 `<Link />` component를 import 하자. `<Link />` component를 헤더 아래에 넣고, `to` property에 `/contact/`를 pathname으로 입력하자.

    ```javascript
    import React from "react"
    import { Link } from "gatsby"
    import Header from "../components/header"
    
    export default () => (
        <div style={{ color: `purple` }}>
        <Link to="/contact/">Contact</Link> 
        <Header headerText="Hello Gatsby!" />
        <p>What a world.</p>
        <img src="https://source.unsplash.com/random/400x200" alt="" />
        </div>
    )
    ```

    하지만 링크를 클릭해보면 404페이지를 보게 될 것😔 왜? 아직 존재하지 않는 페이지로 연결하려고 했기 때문.

    💡 Gatsby에서의 [404 page](https://www.gatsbyjs.org/docs/add-404-page/)

2. 새로운 Contact 페이지를 위해 *src/pages/contact.js* 파일을 만들자. 그리고 홈페이지로 돌아가는 링크를 넣자.

    ```javascript
    import React from "react"
    import { Link } from "gatsby"
    import Header from "../components/header"
    
    export default () => (
        <div style={{ color: `teal` }}>
        <Link to="/">Home</Link>
        <Header headerText="Contact" />
        <p>Send us a message!</p>
        </div>
    )
    ```

    파일을 저장해보면 홈페이지와 서로 연결된 Contact 페이지를 볼 수 있을 것

Gatsby의 `<Link />`는 사이트 내에서 페이지들을 연결하기 위한 component이다. 외부 링크는 Gatsby가 처리하지 않으므로, HTML의 `<a>` 태그를 사용하자.

💡 Gatsby에서의 routing을 더 알아보고 싶다면 [API doc for Gatsby Link](https://www.gatsbyjs.org/docs/gatsby-link/)

## Deploying a Gatsby site

Gatsby는 *modern site generator*이다. 즉, setup할 서버나 배포해야 할 복잡한 database가 없다는 얘기이다. 대신, Gatsby의 `build` 명령어는 정적 사이트 호스팅 서비스에 배포할 수 있는 static HTML과 JavaScript 파일의 디렉터리를 생성한다.

```bash
npm run build
```

build는 15-30초 정도 걸리며, build가 완료 되면 *public* 디렉터리에서 배포를 위해 생성된 파일들을 확인할 수 있다.