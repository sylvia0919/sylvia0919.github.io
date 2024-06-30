---
title: "[React] useSearchParams vs useParams"
date: 2024-06-30 00:00 +0300
categories: [Project, Study, React]
tags: [github-pages, Study, React, useSearchParams, useParams]
author: sylvia0919
---

오늘은 React hook 함수 중에서 헷갈리는 useSearchParams와 useParams를 정리해보고자 한다.

![Desktop View](assets/img/posts/2024-06-30-React-useSearchParams-vs-useParams/3.gif){: width="400"}

우선 미리 정리해두면 좋을 개념이 있는데, Path Parameter와 Query Parameter이다.

&nbsp;&nbsp;

### Path Parameter
- ex> https://www.sample.co.kr/:country 에서 country에 해당하는 부분
- 유일값 식별할때 사용
- GET, POST, PATCH, DELETE에서 사용할 수 있다   
 - resource는 같지만, 데이터가 다를때 restful하게 api구성 가능
- react에서 useParams으로 사용



### Query Parameter
- ex> https://www.sample.co.kr?id=1 에서 id에 해당하는 부분
- 옵션줄때 사용 
 - 필터링, 정렬, 페이지네이션, 검색 등
- GET, DELETE에서 사용할 수 있다
- react에서 useSearchParams으로 사용

&nbsp;&nbsp;

### useParams 사용법 

//index.js
```
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import { BrowserRouter } from "react-router-dom";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

// App.js
```
import { Route, Routes } from "react-router-dom";
import Test from "./Test";

function App() {
  return (
    <>
      <Routes>
        <Route path="/:country" element={<Test />} />
      </Routes>
    </>
  );
}

export default App;
```

//Test.js
```
import { useParams } from "react-router-dom";

function Test() {
  const { country } = useParams();

  return (
    <>
      <div>parameter 값은 {country}입니다.</div>
    </>
  );
}

export default Test;
```

![Desktop View](assets/img/posts/2024-06-30-React-useSearchParams-vs-useParams/2.png){: width="700"}

### useSearchParams 사용법

// App.js   
```
import { useSearchParams } from "react-router-dom";

function App() {
  const [searchParams, setSearchParams] = useSearchParams();
  const id = searchParams.get("id");

  return <div>query값은 {id}입니다.</div>;
}

export default App;
```

![Desktop View](assets/img/posts/2024-06-30-React-useSearchParams-vs-useParams/1.png){: width="700"}

&nbsp;&nbsp;

### 참고
 - <https://velog.io/@juno97/API-Path-parameter-VS-Query-Parameter-%EA%B8%B0%EB%A1%9D%EC%9A%A9>

 - <https://velog.io/@liljoon/React-useSearchParams-%EA%B3%BC-useParams-%EC%B4%88%EA%B0%84%EB%8B%A8-%EC%82%AC%EC%9A%A9%EB%B2%95>