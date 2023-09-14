### **Hooks**

**hooks**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7536f4be-19c3-444f-9c8b-180127bfe490/5da5ba8c-46ab-4264-a019-005f5dd2325d/Untitled.png)

- 함수형 Component는 Class Component와 같이 State와 Class Component의 생명 주기에 맞춰 코드가 실행되도록 할 수 없었기에, Hook 통해 기능을 보완.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7536f4be-19c3-444f-9c8b-180127bfe490/eb8ccc9b-4202-4430-b227-12f497cf5823/Untitled.png)

- 원하는 기능을 원하는 때에 사용할 수 있도록 함.

**UseState**

State 사용하기 위한 Hook

- 함수 Component의 경우, `useState`통해 값이 rerandering 되도록 한다.

```jsx
//해당 함수에 대한 rendering만 담당
import React, { useState } from "react";

function Counter(props) {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>총 {count}번 클릭했습니다.</p>
      <button onclick={() => count++}>클릭</button>
    </div>
  );
}
```

```jsx
//전체 코드에 대한 rendering 담
import React, { useState } from "react";

function Counter(props) {
  var count = 0;

  return (
    <div>
      <p>총 {count}번 클릭했습니다.</p>
      <button onclick={() => count++}>클릭</button>
    </div>
  );
}
```

```jsx
//useState의 사용법
const [변수명, set함수명] = useState(초기값);
```

**sideEffect**

Side Effect(효과) 실행하기 위한 Hook

- 생명 주기 함수 (`componentDidUpdate`, `componentDidMount`, `componentWillUnmount`)와 동일한 기능을 하나로 통합해 제공

```jsx
//useEffect 사용법
useEffect(이펙트 함수, 의존성 배열);
//의존성 배열: Effect가 의존하고 있는 배열, 배열 값이 하나라도 변경되면 실행
```

- Effect function이 mount, unmount 시에 단 한 번씩만 실행

```jsx
useEffect(이펙트 함수, []);
```

- 의존성 배열 생략시, component업데이트 마다 호출

```jsx
useEffect(이펙트 함수);
```

```jsx
import React, { useState, useEffect } from "react";

function Counter(props) {
  const [count, setCount] = useState(0);

  //componentDidMount, componentDidUpdate와 비슷하게 작동
  useEffect(() => {
    //브라우저 API를 이용해서 document의 title을 업데이트
    document.title = `You clicked ${count} times`;
  });
  return (
    <div>
      <p> 총 {count}번 클릭했습니다</p>
      <button onClick={() => setCount(count + 1)}>클릭</button>
    </div>
  );
}
```

```jsx
import React, { useState, useEffect } from "react";

function UserStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    SeverAPI.subscribeUserStatus(props.user.id, handleStatusChange);
    return () => {
      //component가 unmount 될 떄 호
      SeverAPI.unsubscribeUserStatus(props.user.id, handlerStatusChange);
    };
  });

  if (isOnline === null) {
    return "대기 중...";
  }
  return isOnline ? "온라인" : "오프라인";
}
```

```jsx
function UserStatusWithCounter(props) {
	const [count,setCount] = useState(0);
	useEffect(() = > {
		document.title = `총 ${count}번 클릭했습니다.`;
	});

	const [isOnline, setIsOnline] = useState(null);
	useEffect(() => {
		ServerAPI.unsubscribeUserStatus(props.user.id,handleStatusChange);
		return() => {
			ServerAPI.unsubscribeUserStatus(props.user.id, handleStatusChange);
		};
	});

	function handleStatusChange(status) {
		setIsOnline(status.isOnline);
	}

//...
```

**useEffect 사용법 정리**

```jsx
useEffect(() => {
	//컴포넌트가 마운트 된 이후,
	//의존성 배열에 있는 변수들 중 하나라도 값이 변경되었을 때 실행됨
	//의존성 배열에 빈 배열([])을 넣으면 마운트와 언마운트시에 단 한 번씩만 실행됨
	//의존성 배열 생략 시 컴포넌트 업데이트 시마다 실행됨
	...

	return () => {
		//컴포넌트가 마운트 해제되기 전에 실행됨
		...
	}
}, [의존성 변수1, 의존성 변수2, ...]);
```
