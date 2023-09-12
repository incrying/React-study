**Elements?**

리액트 앱을 구성하는 가장 작은 블록들. 화면에서 보이는 것들을 기술함

<aside>
❗ React Element와 DOM Element의 차이

![1](https://github.com/incrying/React-study/assets/114045826/3fad2cf2-674c-4394-87e5-7a8f2868c99f)

DOM element의 가상 표현이 React element임.

</aside>

**React Element의 생김새**

자바스크립트 객체 형태로 존재. 한번 생성되면 바꿀 수 없는 불변성을 지님.

```jsx
{
	type: 'button',
	props: {
			className: 'bg-green',
			children: {
				type: 'b',
				props: {
					children: 'Hello, element!'
				}
			}
	}
}
```

```jsx
//위 코드 rendering 시,
<button class="bg-green">
  <b>Hello, element!</b>
</button>
```

```jsx
{ //React의 component element code
	type:Button,
	props: {
		color: 'green',
		children: 'Hello, element!'
	}
}
```

**React.createElement 구성**

![2](https://github.com/incrying/React-study/assets/114045826/98879e9f-155f-4cce-a027-3ee77d92c4b4)

- **type:** HTML 태그 이름이 문자열로 들어가거나 또 다른 React component가 들어감.
  - 하나의 component는 여러 개의 component 가질 수 있음
- **props:** Element의 속성을 지정
- **children:** 해당 Element의 자식 Element가 들어감
- **type이 React component라면?**
  - ConfirmDialog의 children 중, 두 번째 children이 React component이므로, createElement 통해 Element 생성

```jsx
function Button(props) {
  return (
    <button className={`bg-${props.color}`}>
      <b>{props.children}</b>
    </button>
  );
}

function ConfirmDialog(props) {
  return (
    <div>
      <p>내용을 확인하셨으면 확인 버튼을 눌러주세요.</p>
      <Button color="green">확인</Button>
    </div>
  );
}
```

```jsx
{
	type: 'div',
	props: {
			children: [
				{
					type:'p',
					props: {
						children: '내용을 확인하셨으면 확인 버튼을 눌러주세요.'
					}
				},
				{
					type: 'button',
					props: {
						className: 'bg-green',
						children: {
							type: 'b',
							props: {
								children: '확인'
							}
						}
					}
				}
			]
	}
}
```

**Element의 특징**

React element는 불변성을 지니므로, element 생성 후에는 children이나 attributes 바꿀 수 없음

<aside>
❗ 변동 사항이 생길 때 마다 element 계속 생성하는 것.  개발 시 이를 고려하면 성능 개선에 도움 줄 수 있음.

</aside>

**Element rendering**

React로만 만들어진 모든 웹사이트는 단 하나의 root DOM node 지님.

기존의 웹사이트에 react 추가하면, 여러 개의 root DOM node를 가질 수도 있음.

```jsx
const element = <h1> 안녕, 리액트! </h1>;
ReactDOM.render(element, document.getElementBtId("root"));
```

- **Rendering Elements update**

Elements는 불변성을 지니기 때문에 Element update 위해서는 다시 생성해야 함

```jsx
function tick() {
  const element = (
    <div>
      <h1>안녕, 리액트!</h1>
      <h2>현재 시간: {new Date().toLocaleTimeString()}</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById("root"));
}

setInterval(tick, 1000);
```

`setInterval` 통해 매 초 새로운 Element가 생성되는 것을 볼 수 있음.
