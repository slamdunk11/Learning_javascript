# async vs defer

### 1. script를 html head에 포함하는 방식
- parsing html + css 하여 dom으로 바꿔서 보여줌
- 그러다가 script를 만나면 서버에서 main.js를 다운받아
- js를 다운받고 실행한 다음 
- 다시 parsing html로 넘어간다
- parsing html => fetching js => executing js => parsing html => page is ready

=> 많은 시간 소요

### 2. body 제일 끝 부분에 script
- parsing html => page is ready(페이지가 준비된 다음) => fetching js => executing js
- js 파일 받기 전에 사용자가 페이지 볼 수 있다

=> js에 의존적인 홈페이지라면 사용자가 정상적인 페이지를 보기까지 기다려야해

### 3. head 안에 script 쓰되 async 를 사용
- async : boolean 타입의 속성, true로 설정이 된다
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <script async src="main.js"></script>
    <script async src="a.js"></script>
    <script async src="b.js"></script>
    <script async src="c.js"></script>
  </head>
  <body></body>
</html>
```
- parsing html, fetching js(파싱하다가 script 만나면 js 다운 병렬로 실행) => executing js(파싱 잠시 멈추고) => parsing HTML => page is ready

=> 다운 시간 절약, 
=> but, 자바스크립트가 html parsing 되기 전에 실행되기 때문에 js 파일에서 querySelector이용해서 dom요소 조작할 때 아직 html이 정의되지 않았을 경우 위험
=> html parsing하는 동안 js 만나면 실행하기 위해 멈춰야하니까 사용자가 페이지 보는데 여전히 시간이 걸림

- script 정의한대로, 순서대로 진행되지 않음, 다운이 먼저 끝난 순으로 실행됨, a,b,c.js 순서가 중요하다면 문제가 생길 수 있음

### 4. head 안에 script 쓰되 defer 사용(제일 좋은 옵션)
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <script defer src="main.js"></script>
     <script defer src="a.js"></script>
    <script defer src="b.js"></script>
    <script defer src="c.js"></script>
  </head>
  <body></body>
</html>
```
- parsing html 하다가 script 만나면 fetching js 병렬 실행 => parsing html 완료(page is ready)=> executing js
- 다운 다 받아놓은 다음에 실행하므로 a, b, c.js 순서대로 실행된다
