**Elements?**

리액트 앱을 구성하는 가장 작은 블록들. 화면에서 보이는 것들을 기술함

<aside>
❗ **React Element와 DOM Element의 차이**

![KakaoTalk_20230911_231242800.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/7536f4be-19c3-444f-9c8b-180127bfe490/03c62ec5-9068-4e90-8c52-33653b18e020/KakaoTalk_20230911_231242800.jpg)

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

![KakaoTalk_20230911_231457688.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/7536f4be-19c3-444f-9c8b-180127bfe490/4c1e082d-09b2-4d67-b3bc-f568ba6f4f1b/KakaoTalk_20230911_231457688.jpg)

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
❗ 변동 사항이 생길 때 마다 **element 계속 생성**하는 것.  개발 시 이를 고려하면 성능 개선에 도움 줄 수 있음.

</aside>

**Element rendering**

React로만 만들어진 모든 웹사이트는 단 하나의 root DOM node 지님.

기존의 웹사이트에 react 추가하면, 여러 개의 root DOM node를 가질 수도 있음.

```jsx
const element = <h1> 안녕, 리액트! </h1>;
ReactDOM.render(element, document.getElementBtId("root"));
```
