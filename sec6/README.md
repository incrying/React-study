### State and Lifecycle

**State**

React Component의 변경 가능한 데이터, State는 개발자가 직접 정의

- 렌더링이나 데이터 흐름에 사용되는 값만 State에 포함시켜야 함
- State는 자바스크립트 객체이며, 직접 수정이 불가하다.
  - React State는 Component의 Rendering과 관련이 있기에 직접 수정하는 것은 좋지 않음

```jsx
class LikeButton extends React.Component {
	constructor(props) {
		super(props);

		this.state = { //현재 Component의 State를 정의하는 부분
			liked:flase
		};
	}

	...
}
```

```jsx
//State를 직접 수정 (잘못된 사용법)
this.state = {
  name: "Inje",
};

//setState 함수를 통한 수정 (정상적인 사용법)
this.setState({
  name: "Inje",
});
```

**Lifecycle**

**React Class Component의 생명 주기**

![7](https://github.com/incrying/React-study/assets/114045826/5e441d4e-158d-4662-b49a-0c3efe79d785)

- **Lifecycle Method**: 생명 주기에 따라 호출되는 Class Component의 함수
- Component가 계속 존재하는 것이 아니라, 시간의 흐름에 따라 생성되고 업데이트 되다가 사라진다.
