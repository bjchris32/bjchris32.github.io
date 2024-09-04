---
layout: post
title:  "react router implementation"
date:   2024-08-27 11:40:34 -0500
categories: rails
---

## Context:
I am implementing the router in reactJS with typescript.
```
const App: React.FC = () => (
    <BrowserRouter basename="/">
      <Router>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/signup" element={<SignUpPage />} />
          <Route path="/login" element={<LoginPage />} />
        </Routes>
      </Router>
    </BrowserRouter>
);
```
But, typescript raised an error on the line `Routes` with message:
```
Type '{ children: Element; }' is missing the following properties from type 'RouterProps': location, navigatorts(2739)
```



## Solution:
I don't know why the following code from chatGPT works. Essentially, how does `BrowserRouter as` work?
```
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import SignUpPage from './pages/SignUpPage';
import HomePage from './pages/HomePage';
import LoginPage from './pages/LogInPage';

function App() {
  return (
    <Routes>
      <Route path="/" element={<HomePage />} />
      <Route path="/signup" element={<SignUpPage />} />
      <Route path="/login" element={<LoginPage />} />
    </Routes>
  );
}
```


## Reference
