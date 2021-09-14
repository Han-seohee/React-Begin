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
