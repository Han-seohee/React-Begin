# React-Begin 리액트 입문
2021.09.15
### :blue_heart:나의 첫번째 리액트 컴포넌트

:file_folder: App.js

```
import React from 'react';
import Hello from './Hello';

function App() {
  return (
      <div>
        <Hello />
        <Hello />
        <Hello />
      </div>
  );
}

export default App;

```

:file_folder: Hello.js

```
import React from 'react';

function Hello() {
    return <div>안녕하세요</div>;
}

export default Hello;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133306659-df4e4c02-e59a-46b5-bd7a-61285dfd3e4d.PNG>

---
### :blue_heart:JSX의 기본 규칙 알아보기

```
1. <div>태그는 꼭 닫혀야 한다.</div>
   <Hello />

2. <>
   <div>두개 이상의</div>
   <p>태그는 감싸자</p>
   </>

3. const name = '이렇게';
   return <div>JavaScript 값 보여줄 땐, {name}</div>

4. 스타일 적용 - 객체
    const style = {
    background: 'gray',
    }
    return (
     <div style={style}>
      <div className="my-style">
        style 과 className
      </div>
     </div>
   )

5. 주석
   return (
    <div>
     {/*주석은 이렇게*/}
     <input
       // 또는 이렇게
     />
    </div>
```

---
### :blue_heart:props를 통해 컴포넌트에게 값 전달하기

:file_folder:App.js

```
import React from 'react';
import Hello from './Hello';

function App() {
  return (
      <Hello name="react" />
  );
}

export default App;

```

:file_folder:Hello.js

```
import React from 'react';

function Hello(props) {
    console.log(props);
    return <div>안녕하세요{props.name}</div>;
}

export default Hello;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133419404-403e7b99-fa04-4e01-bee7-0122e5f62ab2.png>

>style color="red"

:file_folder:App.js

```
import React from 'react';
import Hello from './Hello';

function App() {
  return (
      <Hello name="react" color="red" />
  );
}

export default App;

```

:file_folder:Hello.js

```
import React from 'react';

function Hello(props) {
    console.log(props);
    return <div style={{
        color: props.color
    }}>안녕하세요{props.name}</div>;
}

export default Hello;
```

:point_down: 비구조화 할당, 구조분해

:file_folder:Hello.js

```
import React from 'react';

function Hello({ color, name }) {
    return <div style={{
        color
    }}>안녕하세요 {name}</div>;
}

export default Hello;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133420329-e6ac277d-10da-46dd-af89-84b0699927d5.png>

>defaultProps : 특정 값을 빠트렸을 때 기본적으로 사용할 값
>>props를 지정하지 않았을 때 기본적으로 사용할 값을 설정하기

:file_folder:App.js

```
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <>
      <Hello name="react" color="red" />
      <Hello color="pink" />
    </>
  );
}

export default App;

```

:file_folder:Hello.js

```
import React from 'react';

function Hello({ color, name }) {
    return <div style={{
        color
    }}>안녕하세요 {name}</div>;
}

Hello.defaultProps = {
    name: '이름없음'
};

export default Hello;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133421681-455e7487-cdf1-4da9-8666-98df7d176355.png>

>propsChildren : <wrapper>사이의 내용 children</wrapper>

:file_folder:App.js

```
import React from 'react';
import Hello from './Hello';
import Wrapper from './Wrapper';
// import Counter from './Counter';


function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" />
      <Hello color="pink" />
    </Wrapper>
  );
}

export default App;

```

:file_folder:Hello.js

```
import React from 'react';

function Hello({ color, name }) {
    return <div style={{
        color
    }}>안녕하세요 {name}</div>;
}

Hello.defaultProps = {
    name: '이름없음'
};

export default Hello;
```

:file_folder:Wrapper.js

```
import React from 'react';

function Wrapper( { children } ) {
    const style = {
        border: '2px solid black',
        padding: 16
    };

    return <div style={style}>{children}</div>
}

export default Wrapper;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133423456-255c5a68-491d-42f7-843f-3e8cc2a3d1ce.png>

---
### :blue_heart:조건부 렌더링

특정 조건이 참인지 거짓인지에 따라 다른 결과를 보여줌

>삼항연산자 (내용이 바뀌어야 할 때)

:file_folder:App.js

```
import React from 'react';
import Hello from './Hello';
import Wrapper from './Wrapper';
// import Counter from './Counter';


function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" isSpecial={true} />   {/*{true} 생략 가능. 생략하면 true로 간주*/}
      <Hello color="pink" />
    </Wrapper>
  );
}

export default App;

```

:file_folder:Hello.js

```
import React from 'react';

function Hello({ color, name, isSpecial }) {
    return (
    <div style={{
        color
    }}>
        {isSpecial ? <b>*</b> : null }
        안녕하세요 {name}
    </div>
    );
}

Hello.defaultProps = {
    name: '이름없음'
};

export default Hello;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133430864-bdfaadb5-0e42-4cd8-9231-065a7e91d7ec.png>

:point_down:

>&&연산자 (단순히 숨기고 보여주고)

:file_folder:Hello.js

```
import React from 'react';

function Hello({ color, name, isSpecial }) {
    return (
    <div style={{
        color
    }}>
        {isSpecial && <b>*</b> }
        안녕하세요 {name}
    </div>
    );
}

Hello.defaultProps = {
    name: '이름없음'
};

export default Hello;
```

---
### :blue_heart:useState를 통해 컴포넌트에서 바뀌는 값 관리하기

:file_folder:App.js

```
import React from 'react';
import Counter from './Counter';


function App() {
  return (
    <Counter />
  );
}

export default App;

```

:file_folder:Counter.js

```
import React, { useState } from 'react';

function Counter() {
    const [number, setNumber] = useState(0);

    const onIncrease = () => {
        setNumber(prevNumber => prevNumber + 1);   {/*함수형*/}
    }

    const onDecrease = () => {
        setNumber(prevNumber => prevNumber -1);   {/*setNumber(number -1); 로도 쓸수있음*/}
    }
    return (
        <div>
            <h1>{number}</h1>
            <button onClick={onIncrease}>+1</button>
            <button onClick={onDecrease}>-1</button>
        </div>
    )
}

export default Counter;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133435426-a6da2ecd-2b5f-413a-a67b-d9a8f07bba9b.png>

---
### :blue_heart: input상태 관리하기

:file_folder:App.js

```
import React from 'react';
import InputSample from './InputSample';


function App() {
  return (
    <InputSample />
  )
}

export default App;
```

:file_folder:InputSample.js

```
import React, { useState } from 'react';

function InputSample() {
    const [text, setText] = useState('');

    const onChange = (e) => {
        setText(e.target.value);
    };

    const onReset = () => {
        setText('');
    };

    return (
        <div>
            <input onChange={onChange} value={text} />    {/*value={text}가 중요*/}
            <button onClick={onReset}>초기화</button>
            <div>
                <b>값: </b>
                {text}
            </div>
        </div>
    );
}

export default InputSample;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133440217-26b7534a-f6bc-4be7-b916-0d46c3f2c11a.png>

---
### :blue_heart: 여러개의 input상태 관리하기

:file_folder:App.js

```
import React from 'react';
import InputSample from './InputSample';


function App() {
  return (
    <InputSample />
  )
}

export default App;
```

:file_folder:InputSample.js

```
import React, { useState } from 'react';

function InputSample() {
    const [inputs, setInputs] = useState({
        name: '',
        nickname: '',
    });
    const { name, nickname } = inputs;

    const onChange = (e) => {
        const { name, value } = e.target;

        setInputs ({
            ...inputs,
            [name]: value,
        });
    };

    const onReset = () => {
        setInputs({
            name: '',
            nickname: '',
        });
    };

    return (
        <div>
            <input 
            name="name" 
            placeholder="이름"
            onChange={onChange} 
            value={name} 
            />
            <input 
            name="nickname" 
            placeholder="닉네임" 
            onChange={onChange} 
            value={nickname} 
            />
            <button onClick={onReset}>초기화</button>
            <div>
                <b>값: </b>
                {name} ({nickname})
            </div>
        </div>
    );
}

export default InputSample;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133443683-c9010f18-6889-47e3-9f46-f4c1d1b19f59.png>

---
### :blue_heart: useRef로 특정 DOM 선택하기 (초기화 버튼 누르면 focus 변경)

:file_folder: InputSample.js

```
import React, { useState, useRef } from 'react';

function InputSample() {
    const [inputs, setInputs] = useState({
        name: '',
        nickname: '',
    });
    const nameInput = useRef();
    const { name, nickname } = inputs;

    const onChange = (e) => {
        const { name, value } = e.target;

        setInputs ({
            ...inputs,
            [name]: value,
        });
    };

    const onReset = () => {
        setInputs({
            name: '',
            nickname: '',
        });
        nameInput.current.focus();
    };

    return (
        <div>
            <input 
            name="name" 
            placeholder="이름"
            onChange={onChange} 
            value={name} 
            ref={nameInput}
            />
            <input 
            name="nickname" 
            placeholder="닉네임" 
            onChange={onChange} 
            value={nickname} 
            />
            <button onClick={onReset}>초기화</button>
            <div>
                <b>값: </b>
                {name} ({nickname})
            </div>
        </div>
    );
}

export default InputSample;
```

---
### :blue_heart: 배열 렌더링하기

:file_folder:App.js

```
import React from 'react';
import UserList from './UserList';


function App() {
  return (
    <UserList />
  )
}

export default App;
```

:file_folder:UserList.js

```
import React from 'react';

function User({ user }) {
    return (
        <div>
            <b>{user.username}</b> <span>({user.email})</span>
        </div>
    );
}

function UserList() {
    const users = [
        {
            id: 1,
            username: 'seohee',
            email: 'a67114585a@gmail.com'
        },
        {
            id: 2,
            username: 'tester',
            email: 'tester@example.com'
        },
        {
            id: 3,
            username: 'liz',
            email: 'liz@example.com'
        }
    ];

    return (
        <div>
            {
                users.map(
                    (user, index) => (<User user={user} key={user.id} />)
                )
            }
        </div>
    );
}

export default UserList;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133449641-6048566c-7eab-49e1-badc-2d73c2a74fe1.png>
