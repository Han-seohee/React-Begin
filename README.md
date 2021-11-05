# React-Begin 리액트 입문
2021.09.15
### :blue_heart:나의 첫번째 리액트 컴포넌트

:file_folder: App.js

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

```js
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

---
### :blue_heart: useRef로 useRef로 컴포넌트 안의 변수 만들기

>리렌더링 돼도 특정 변수를 기억하고 싶을 때 (컴포넌트에 리렌더링 되진 않음)

:file_folder:App.js

```js
import React, { useRef } from 'react';
import UserList from './UserList';


function App() {
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

const nextId = useRef(4);

const onCreate = () => {

  console.log(nextId.current); // 4
  nextId.current += 1;
}

  return (
    <UserList users={users}/>
  )
}

export default App;

```

:file_folder:UserList.js

```js
import React from 'react';

function User({ user }) {
    return (
        <div>
            <b>{user.username}</b> <span>({user.email})</span>
        </div>
    );
}

function UserList({ users }) {

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

---
### :blue_heart: 배열에 항목 추가하기

:file_folder:App.js

```js
import React, { useDebugValue, useRef, useState } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';


function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }
  const [users, setUsers] = useState ([
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
]);

const nextId = useRef(4);

const onCreate = () => {
  setInputs({
    username: '',
    email: ''
  });
  console.log(nextId.current); // 4
  nextId.current += 1;
}

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users}/>
    </>
  )
}

export default App;
```

:file_folder:CreateUser.js

```js
import React from 'react';

function CreateUser({ username, email, onChange, onCreate }) {
    return (
        <div>
            <input
            name="username"
            placeholder="계정명"
            onChange={onChange}
            value={username}
            />
            <input
            name="email"
            placeholder="이메일"
            onChange={onChange}
            value={email} />
            <button onClick={onCreate}>등록</button>
        </div>
    );
}

export default CreateUser;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133455038-f578abfb-20e9-4f6a-a821-fcb92db984ff.png>

:point_down: 항목 추가하기

1. spread

:file_folder:App.js

```js
import React, { useDebugValue, useRef, useState } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';


function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }
  const [users, setUsers] = useState ([
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
]);

const nextId = useRef(4);

const onCreate = () => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers([...users, user]);
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
}

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users}/>
    </>
  )
}

export default App;
```
:mag:

<img src=https://user-images.githubusercontent.com/86407453/133455615-debf332b-71b5-44e3-a5b0-55b663a5b341.png>

2. concat

:file_folder:App.js

```js
import React, { useDebugValue, useRef, useState } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';


function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }
  const [users, setUsers] = useState ([
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
]);

const nextId = useRef(4);

const onCreate = () => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers(users.concat(user));
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
}

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users}/>
    </>
  )
}

export default App;
```

---
2021.09.16
### :blue_heart: 배열에 항목 제거하기 filter

:file_folder:App.js

```js
import React, { useDebugValue, useRef, useState } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';


function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }
  const [users, setUsers] = useState ([
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
]);

const nextId = useRef(4);

const onCreate = () => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers(users.concat(user));
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
};

const onRemove = id => {
  setUsers(users.filter(user => user.id !== id));
};

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} />
    </>
  )
}

export default App;
```

:file_folder:UserList.js

```js
import React from 'react';

function User({ user, onRemove }) {
    const { username, email, id } = user;
    return (
        <div>
            <b>{username}</b> <span>({email})</span>
            <button onClick={() => onRemove(id)}>삭제</button>
        </div>
    );
}

function UserList({ users, onRemove }) {

    return (
        <div>
            {
                users.map(
                    (user, index) => (
                    <User 
                    user={user} 
                    key={user.id} 
                    onRemove={onRemove} 
                    />
                    )
                )
            }
        </div>
    );
}

export default UserList;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133459015-a0e77287-dfaf-40e0-b1b4-c17f4605ccf0.png>

---
### :blue_heart: 배열에 항목 수정하기 map

:file_folder:App.js

```js
import React, { useDebugValue, useRef, useState } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';


function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }
  const [users, setUsers] = useState ([
    {
        id: 1,
        username: 'seohee',
        email: 'a67114585a@gmail.com',
        active: true,
    },
    {
        id: 2,
        username: 'tester',
        email: 'tester@example.com',
        active: false,
    },
    {
        id: 3,
        username: 'liz',
        email: 'liz@example.com',
        active: false,
    }
]);

const nextId = useRef(4);

const onCreate = () => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers(users.concat(user));
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
};

const onRemove = id => {
  setUsers(users.filter(user => user.id !== id));
};

const onToggle = id => {
  setUsers(users.map(
    user => user.id === id
    ? { ...user, active: !user.active }
    : user
  ));
};

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
    </>
  )
}

export default App;
```

:file_folder: UserList.js

```js
import React from 'react';

function User({ user, onRemove, onToggle }) {
    const { username, email, id, active } = user;
    return (
        <div>
            <b
                style={{
                color: active ? 'green' : 'black',
                cursor: 'pointer'
            }}
            onClick={() => onToggle(id)}
            >
            {username}
            </b> 
            &nbsp;
            <span>({email})</span>
            <button onClick={() => onRemove(id)}>삭제</button>
        </div>
    );
}

function UserList({ users, onRemove, onToggle }) {
    return (
        <div>
            {
                users.map(
                    (user) => (
                    <User 
                    user={user} 
                    key={user.id} 
                    onRemove={onRemove} 
                    onToggle={onToggle}
                    />
                    )
                )
            }
        </div>
    );
}

export default UserList;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133461268-5f23b04b-6ed2-47c6-bb66-2e2e1ec7ad6b.png>

---
### :blue_heart: useEffact를 사용하여 마운트언마운트 업데이트시 할 작업 설정하기

>useEffect Hook

:file_folder:UserList.js

```js
import React, { useEffect } from 'react';

function User({ user, onRemove, onToggle }) {
    const { username, email, id, active } = user;
    useEffect(() => {
        console.log('컴포넌트가 화면에 나타남');
        // props -> state
        // REST API
        // D3 Video.js
        // setInterval, setTimeout
        return () => {
            // clearInterval, clearTimeout
            // 라이브러리에 인스턴스 제거
            console.log('컴포넌트가 화면에서 사라짐');
        }
    }, []);
    return (
        <div>
            <b
                style={{
                color: active ? 'green' : 'black',
                cursor: 'pointer'
            }}
            onClick={() => onToggle(id)}
            >
            {username}
            </b> 
            &nbsp;
            <span>({email})</span>
            <button onClick={() => onRemove(id)}>삭제</button>
        </div>
    );
}

function UserList({ users, onRemove, onToggle }) {
    return (
        <div>
            {
                users.map(
                    (user) => (
                    <User 
                    user={user} 
                    key={user.id} 
                    onRemove={onRemove} 
                    onToggle={onToggle}
                    />
                    )
                )
            }
        </div>
    );
}

export default UserList;
```

>user값

:file_folder:UserList.js

```js
import React, { useEffect } from 'react';

function User({ user, onRemove, onToggle }) {
    const { username, email, id, active } = user;
    
    useEffect(() => {
        console.log('user 값이 설정됨');
        console.log(user);
        return () => {
            console.log('user 값이 바뀌기 전');
            console.log(user);
        }
    }, [user]);

    return (
        <div>
            <b
                style={{
                color: active ? 'green' : 'black',
                cursor: 'pointer'
            }}
            onClick={() => onToggle(id)}
            >
            {username}
            </b> 
            &nbsp;
            <span>({email})</span>
            <button onClick={() => onRemove(id)}>삭제</button>
        </div>
    );
}

function UserList({ users, onRemove, onToggle }) {
    return (
        <div>
            {
                users.map(
                    (user) => (
                    <User 
                    user={user} 
                    key={user.id} 
                    onRemove={onRemove} 
                    onToggle={onToggle}
                    />
                    )
                )
            }
        </div>
    );
}

export default UserList;
```

>depth 배열 생략

:file_folder:UserList.js

```js
import React, { useEffect } from 'react';

function User({ user, onRemove, onToggle }) {
    const { username, email, id, active } = user;
    
    useEffect(() => {
        console.log(user);
    });

    return (
        <div>
            <b
                style={{
                color: active ? 'green' : 'black',
                cursor: 'pointer'
            }}
            onClick={() => onToggle(id)}
            >
            {username}
            </b> 
            &nbsp;
            <span>({email})</span>
            <button onClick={() => onRemove(id)}>삭제</button>
        </div>
    );
}

function UserList({ users, onRemove, onToggle }) {
    return (
        <div>
            {
                users.map(
                    (user) => (
                    <User 
                    user={user} 
                    key={user.id} 
                    onRemove={onRemove} 
                    onToggle={onToggle}
                    />
                    )
                )
            }
        </div>
    );
}

export default UserList;
```

---
### :blue_heart:useMemo를 사용하여 연산한 값 재사용하기

:file_folder:App.js

```js
import React, { useRef, useState, useMemo } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';

function CountActiveUsers(users) {
  console.log('활성 사용자 수를 세는중...');
  return users.filter(user => user.active).length;
}
function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }
  const [users, setUsers] = useState ([
    {
        id: 1,
        username: 'seohee',
        email: 'a67114585a@gmail.com',
        active: true,
    },
    {
        id: 2,
        username: 'tester',
        email: 'tester@example.com',
        active: false,
    },
    {
        id: 3,
        username: 'liz',
        email: 'liz@example.com',
        active: false,
    }
]);

const nextId = useRef(4);

const onCreate = () => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers(users.concat(user));
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
};

const onRemove = id => {
  setUsers(users.filter(user => user.id !== id));
};

const onToggle = id => {
  setUsers(users.map(
    user => user.id === id
    ? { ...user, active: !user.active }
    : user
  ));
};

  const count = useMemo(() => CountActiveUsers(users), [users]);

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
      <div>활성 사용자 수 : {count}</div>
    </>
  )
}

export default App;
```

:mag:

<img src=https://user-images.githubusercontent.com/86407453/133531681-b4b4fa9f-9e39-4dbe-b205-be39e5a970fd.png>

---
### :blue_heart: useCallback 를 사용하여 함수 재사용하기

:file_folder:App.js

```js
import React, { useRef, useState, useMemo, useCallback } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';

function CountActiveUsers(users) {
  console.log('활성 사용자 수를 세는중...');
  return users.filter(user => user.active).length;
}
function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = useCallback(e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }, [inputs]);
  const [users, setUsers] = useState ([
    {
        id: 1,
        username: 'seohee',
        email: 'a67114585a@gmail.com',
        active: true,
    },
    {
        id: 2,
        username: 'tester',
        email: 'tester@example.com',
        active: false,
    },
    {
        id: 3,
        username: 'liz',
        email: 'liz@example.com',
        active: false,
    }
]);

const nextId = useRef(4);

const onCreate = useCallback(() => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers(users.concat(user));
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
}, [username, email, users]);

const onRemove = useCallback(id => {
  setUsers(users.filter(user => user.id !== id));
}, [users]);

const onToggle = useCallback(id => {
  setUsers(users.map(
    user => user.id === id
    ? { ...user, active: !user.active }
    : user
  ));
},[users]); 

  const count = useMemo(() => CountActiveUsers(users), [users]);

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
      <div>활성 사용자 수 : {count}</div>
    </>
  )
}

export default App;
```

---
### :blue_heart: React.memo를 사용한 컴포넌트 리렌더링 방지
>컴포넌트의 리렌더링 성능을 최적화 할 수 있음

:file_folder:App.js

```js
import React, { useRef, useState, useMemo, useCallback } from 'react';
import CreateUser from './CreateUser';
import UserList from './UserList';

function CountActiveUsers(users) {
  console.log('활성 사용자 수를 세는중...');
  return users.filter(user => user.active).length;
}
function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = useCallback(e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  }, [inputs]);
  const [users, setUsers] = useState ([
    {
        id: 1,
        username: 'seohee',
        email: 'a67114585a@gmail.com',
        active: true,
    },
    {
        id: 2,
        username: 'tester',
        email: 'tester@example.com',
        active: false,
    },
    {
        id: 3,
        username: 'liz',
        email: 'liz@example.com',
        active: false,
    }
]);

const nextId = useRef(4);

const onCreate = useCallback(() => {
  const user = {
    id: nextId.current,
    username,
    email,
  };
  setUsers(users => users.concat(user));
  setInputs({
    username: '',
    email: ''
  });
  nextId.current += 1;
}, [username, email]);

const onRemove = useCallback(id => {
  setUsers(users => users.filter(user => user.id !== id));
}, []);

const onToggle = useCallback(id => {
  setUsers(users => users.map(
    user => user.id === id
    ? { ...user, active: !user.active }
    : user
  ));
},[]); 

  const count = useMemo(() => CountActiveUsers(users), [users]);

  return (
    <>
      <CreateUser 
      username={username} 
      email={email} 
      onChange={onChange}
      onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
      <div>활성 사용자 수 : {count}</div>
    </>
  )
}

export default App;
```

:file_folder:UserList.js

```js
import React, { useEffect } from 'react';

const User = React.memo(function User({ user, onRemove, onToggle }) {
    const { username, email, id, active } = user;
    
    useEffect(() => {
        console.log(user);
    });

    return (
        <div>
            <b
                style={{
                color: active ? 'green' : 'black',
                cursor: 'pointer'
            }}
            onClick={() => onToggle(id)}
            >
            {username}
            </b> 
            &nbsp;
            <span>({email})</span>
            <button onClick={() => onRemove(id)}>삭제</button>
        </div>
    );
});

function UserList({ users, onRemove, onToggle }) {
    return (
        <div>
            {
                users.map(
                    (user) => (
                    <User 
                    user={user} 
                    key={user.id} 
                    onRemove={onRemove} 
                    onToggle={onToggle}
                    />
                    )
                )
            }
        </div>
    );
}

export default React.memo(
    UserList, (prevProps, nextProps) => nextProps.users === prevProps.users
    );
```

:file_folder:CreateUser.js

```js
import React from 'react';

function CreateUser({ username, email, onChange, onCreate }) {
    console.log('CreateUser');
    return (
        <div>
            <input
            name="username"
            placeholder="계정명"
            onChange={onChange}
            value={username}
            />
            <input
            name="email"
            placeholder="이메일"
            onChange={onChange}
            value={email} />
            <button onClick={onCreate}>등록</button>
        </div>
    );
}

export default React.memo(CreateUser);
```
