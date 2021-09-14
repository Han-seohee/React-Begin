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
