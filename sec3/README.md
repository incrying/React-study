**JSX?**

Javascript + XML/HTML 자바스크립트 문법의 확장

**JSX의 역할**

xml/html 코드를 javascript 코드로 변환함.

React는 JSX 코드를 createElement를 사용하는 코드로 변환. 코드 작성 시 createElement를 이용하여 JSX를 사용하지 않아도 되지만, 효율성이 상승하기 때문에 이득.

```jsx
//JSX를 사용한 코드
class Hello extends React.Component {
	render() {
		return <div>Hello {this.props.toWhat}<div>;
	}
}

ReactDOM.render(
	<Hello toWhat="World" />,
	document.getElementById('root')
);
```

```jsx
//JSX를 사용하지 않은 코드
class Hello extends React.Component {
  render() {
    return React.createElement("div", null, `Hello ${(this.props, toWhat)}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, { toWhat: "World" }, null),
  document.getElementById("root")
);
```

**JSX의 장점**

- **코드의 간결성**
- **가독성 향상**

```jsx
<div>Hello, {name}</div> //JSX 사용
```

```jsx
React.createElement("div", null, `Hello, ${name}`); //JSX 미사용
```

- XSS 방어

```jsx
const title = response.potentiallyMaliciousInput;

//이 코드는 안전합니다.
const element = <h1>{title}</h1>;
```

ReactDOM은 렌더링하기 전에 임베딩 값을 문자열로 변환. (명시적으로 선언되지 않은 값은 괄호 사이에 들어갈 수 없기 때문에)

**JSX 사용법**

HTML 코드 사이에 Javascript 문법을 사용하면 그 자체가 JSX.

```jsx
const name = "소플";
const element = <h1>안녕, {name}</h1>;

ReactDOM.render(element, document.getElementById("root"));
```

```jsx
function formatName(user) {
  return user.firstName + " " + user.lastName;
}

const user = {
  firstName: "Inje",
  lastName: "Lee",
};

const element = <h1>Hello, {formatUser(user)}</h1>;

ReactDOM.render(element, document.getElementById("root"));
```

- **사용자 별로 다른 인사말을 출력하게 하려면?**

```jsx
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

```jsx
//태그의 속성에 값을 넣는 방법
//큰 따옴표 사이에 문자열을 넣거나
const element = <div tableIndex="0"></div>;

//중괄호 사이에 자바스크입트 코드를 넣으면 된다.
const element = <img src={user.avatarUrl}></img>;
```

- **자식을 정의하는 방법**

HTML처럼 상위 태그가 하위 태그를 둘러싸도록 하면 정의됨

```jsx
const element = (
  <div>
    <h1>안녕하세요</h1>
    <h2>열심히 리액트를 공부해봅시다</h2>
  </div>
);
```

**JSX 실습**

```jsx
import React from "react";

function Book(props) {
  return (
    <div>
      <h1>{`이 책의 이름은 ${props.name}입니다.`}</h1>
      <h2>{`이 책은 총 ${props.numOfpage}페이지로 이뤄져 있습니다. `}</h2>
    </div>
  );
}

export default Book;
```

```jsx
import React from "react";
import Book from "./book";

function Library(props) {
  return (
    <div>
      <Book name="처음 만난 파이썬" numOfpage={300} />
      <Book name="처음 만난 AWS" numOfpage={400} />
      <Book name="처음 만난 리액트" numOfpage={500} />
    </div>
  );
}

export default Library;
```
