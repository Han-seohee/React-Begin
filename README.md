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
