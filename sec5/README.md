### **Components and Props**

**Components**

React는 Component 기반의 구조.

- **component 반복적으로 사용**함으로써 코드의 양을 줄이고, 개발 전반에 있어 효율을 높임

![4.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/7536f4be-19c3-444f-9c8b-180127bfe490/8cc8a876-92b5-439c-80e2-480860d67854/4.jpg)

- React component는 어떠한 속성들을 입력으로 받아 **그에 맞는 Element 생성하여 반환**

**Props**

![5.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/7536f4be-19c3-444f-9c8b-180127bfe490/61974027-2368-4e48-b3c2-8d7e848b106f/5.jpg)

property. **Component에 전달할 다양한 정보를 담고 있는 자바스크립트 객체**

- 속성이 다르면 **같은 모양의 Component 속에서도 다른 Element 생성**함
- **Read-only.** 다른 props의 값으로 Element 생성하고자 한다면, 새로운 값을 Component 전달

```jsx
function sum(a, b) {
  return a + b;
} //pure
```

```jsx
function withdraw(account, amount) {
  account.total -= amount;
} //inpure
```

- 모든 React Component는 props 직접 바꿀 수 없고, **같은 props에 대해서는 항상 같은 결과를 보여주어야 함. (=pure)**

```jsx
function App(props) {
	return (
		<profile
			name="소플"
			introduction="안녕하세요, 소플입니다."
			viewCount={1500}
		/>
	);
}

//output
{
	name: "소플",
	introduction: "안녕하세요, 소플입니다.",
	viewCount: 1500
}
```

```jsx
function App(props) {
  return (
    <Layout
      width={2500}
      height={1440}
      header={<Header title="소플의 블로그입니다." />}
      footer={<Footer />}
    />
  );
}
```

### Component

Component는 Fuction Component와 Class Component로 나뉨.

- **Fuction Component**
  - 간단한 코드가 장점

```jsx
fuction Welcom(props) {
	return <h1>안녕, {props.name}</h1>;
}
```

- **Class Component**
  - React.Component 상속 받아 생성

```jsx
Class Welcome extends React.Component {
	render() {
		return <h1>안녕, {this.props.name}</h1>;
	}
}
```

- **Component 이름은 항상 대문자**로 시작할 것

```jsx
const element = <div />; //HTML div 태그로 인식
```

```jsx
const element = <Welcome name="인제" />; //Welcome이라는 React Component로 인식
//만약 소문자로 입력하면 DOM 태그로 인식한다.
```

**Component Rendering**

```jsx
function Welcome(props) {
  return <h1>안녕, {props.name}</h1>;
}

const element = <Welcome name="인제" />;
ReactDOM.render(element, document.getElementById("root"));

const element = <div />; //DOM 태그를 사용한 element
const element = <Welcome name="인제" />; //사용자 정의 Component 사용한 element
```

**Component 합성**

Component 안에 또 다른 Component의 작성이 가능하므로, 복잡한 화면을 여러 개의 Component로 나눠 구현이 가능.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App(props) {
  return (
    <div>
      <Welcome name="Mike" />
      <Welcome name="Steve" />
      <Welcome name="Jane" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

**Component 추출**

Component의 일부를 가져와 새로운 Component 만드는 것. 코드의 재사용성 높임

```jsx
function Comment(props) {
	return (
		<div className="commnet">
			<div className="user-info">
				<img className="avatar"
					src={props.another.avatarUrl}
					alt={props.another.name}
				/>
				<div className="user-info-name">
					{props.author.name}
				</div>
			</div>

			<div className="comment-next">
				{props.text}
			</div>

			<div className="comment-date">
				{formatDate(props.date)}
			</div>
	);
}

//output
props = {
	author: {
		name: "소플",
		avatarUrl: "https://...",
	},
	text: "댓글입니다.",
	date: Date.now(),
}
```

- **avatar img 추출하기**

```jsx
function Avatar(props) {
  return (
    <img className="avatar" src={props.user.avatarUrl} alt={props.user.name} />
  );
}
```

```jsx
function Comment(props) {
	return (
		<div className="commnet">
			<div className="user-info">
				<Avatar user={props.author} />
				<div className="user-info-name">
					{props.author.name}
				</div>
			</div>

			<div className="comment-next">
				{props.text}
			</div>

			<div className="comment-date">
				{formatDate(props.date)}
			</div>
	);
}
```

- **user-info 추출하기**

```jsx
function UserInfo(props) {
  return (
    <div className="user-info">
      <Avatar user={props.user} />
      <div className="user-info-name">{props.user.name}</div>
    </div>
  );
}
```

```jsx
function Comment(props) {
	return (
		<div className="commnet">
			<UserInfo user={props.author} />
			<div className="comment-next">
				{props.text}
			</div>

			<div className="comment-date">
				{formatDate(props.date)}
			</div>
	);
}
```

<aside>
❗ 재사용이 가능한 Component 많이 가지고 있을수록, 개발 속도가 빨라짐.

</aside>
