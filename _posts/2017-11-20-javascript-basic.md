---
layout: post
title: javascript study
description: "javascript study basic"
modified: 2017-11-20
tags: [javascript]
categories: [javascript, etc]
---

# Javascript 

>동적으로 컨텐츠를 바꿀때 사용한다. 
웹페이지를 보다 보면 주기적으로 바뀌는 화면 또는 능동적인 지도나 2D/3D 그래픽, 동영상 등 웹 페이지상에 볼 수 있는 정보들을 좀 더 복잡하고 더 알맞게 표시되도록 하는 것이 자바스크립트이다.  


- **HTML** 은 웹 페이지상에서 문단, 제목, 표, 이미지, 동영상등을 정의하고 그 구조와 의미를 부여하는 마크업 언어이다.

- **CSS** 는 배경색, 폰트, 컨텐츠의 레이아웃등을 지정하여, HTML 컨텐츠를 꾸며주는 스타일 규칙 언어이다.

- **JavaScript** 는 동적으로 컨텐츠를 바꾸고, 멀티미디어를 다루고, 움직이는 이미지등 웹 페이지를 꾸며주도록 하는 프로그래밍 언어이다. 물론, 전부는 아니지만 몇 줄만의 자바스크립트 코드만으로 꽤나 훌륭한 작품을 만들 수 있다.

## 자바스크립트 실행 순서

```javascript
var para = document.querySelector('p');

para.addEventListener('click', updateName);

function updateName() {
  var name = prompt('Enter a new name');
  para.textContent = 'Player 1: ' + name;
}
```
1. 먼저 글문단을 선택한다(1번줄)
2. event listener를 붙여(3번줄) 그 문단이 클릭되었을 때 updateName()코드 블록(중괄호로 묶여있는 부분)이 (5-8번줄) 실행되도록 한다.
3. updateName() 코드 블록(이렇게 계속적으로 사용할 수 있는 코드 블럭을 함수라고 한다.)
4. 사용자로 하여금 새로운 이름을 입력받기를 요청하고, 사용자가 이름을 입력하면 화면에 출력하게 된다.

>자바스크립트는 해석형 언어이다. 따라서 코드가 위에서 아래로 순차적으로 실행되고 그 즉시 결과가 반환된다. 브라우저에서 동작하기 전에 다른 방식으로 코드를 변환할 필요가 없다는 것이다.
>


## 웹페이지에 어떻게 자바스크립트를 넣을까?

**자바스크립트**는 **CSS**와 같은 방식으로 **HTML** 페이지에 적용된다. **CSS**는 외부의 스타일시트를 적용하기 위해 `<link>` 요소를 사용하거나 내부의 스타일시트를 적용하기 위해`<style>` 요소를 사용하는 반면, 자바스크립트는 **HTML** 상에서 오직 `<script>` 태크만으로 사용이 가능하다. 

```javascript
<script>

  // JavaScript goes here

</script>
```
###  1. HTML 내부의 자바스크립트

```javascript
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
<html lang="en">
<head>
  <title>Apply JavaScript example</title>
</head>
<body>
  <button>Click me</button>

  <script>
    function createParagraph() {
      var para = document.createElement('p');
      para.textContent = 'You clicked the button!';
      document.body.appendChild(para);
    }
    var buttons = document.querySelectorAll('button');
    for(var i = 0; i < buttons.length ; i++) {
      buttons[i].addEventListener('click', createParagraph);
    }
  </script>
</body>
</html>
```

### 2. 외부의 자바스크립트 

`apply-javascript-external.html`

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
<html lang="en">
<head>
  <title>Apply JavaScript example</title>
</head>
<body>
  <button>Click me</button>

  <script src="script.js"></script>
</body>
</html>
```
`script.js`

```javascript
function createParagraph() {
  var para = document.createElement('p');
  para.textContent = 'You clicked the button!';
  document.body.appendChild(para);
}

var buttons = document.querySelectorAll('button');

for(var i = 0; i < buttons.length ; i++) {
  buttons[i].addEventListener('click', createParagraph);
}
```

## 주석문

주석문은 브라우저 실행때는 무시되어 넘어가고 다른 개발자로 하여금 어떻게 구성되고 작동되는지 설명해주는 역할을 한다. 물론 자신의 훗날 코드를 다시 보았을 때 빨리 기억하고, 이해할 수 있게끔 도와주기도 한다. 

- 두개의 슬래시(//)를 통해 한 줄의 주석이 가능하다.

```javascript
// I am a comment
```
- /* 와 */를 사용하여 그 사이에 여러 줄의 주석문의 구성이 가능하다.

```javascript
/*
  I am also
  a comment
*/
```
