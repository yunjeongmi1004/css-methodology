# CSS 방법론

## 정의

- CSS 방법론은 프론트엔드 개발 내에서 유지보수 및 확장 을 위한 것으로, 구조화된 접근 방식과 규칙의 모음


## 목적

- 원활한 유지보소를 위함
- 코드의 재사용성을 높이기 위함
- 일정한 규칙으로 클래스명 만으로도 무슨 내용인지 예측할 수 있게 함


### OOCSS

- OOCSS(Object Oriented CSS)
  - CSS를 객체로 분해하여 스타일을 정의하는 방법론으로 중복을 최소화 함
  - 공통된 부분을 찾아 재활용 가능
  - 다중 class 사용으로 가독성 떨어짐

1. 구조와 스킨 분리
```bash
<a class="btn"></a>

<a class="btn primary"></a> 
<a class="btn secondary"></a> 

.btn{
    display:inline-block;
    padding:10px;
    border-radius:10px;
    font-size:14px;
    font-weight:bold;
}

.primary{
    background-color:blue;
    color:#fff
}
.secindary{
    background-color:pink;
    color:#fff;
}
```

2. 컨테이너와 컨텐츠 분리
```bash
    <header class="header mx-1024">Header</header>
    <footer class="footer mx-1024">Footer</footer>

    .header{
        position:relative;
        padding-top:20px;
        padding-bottom:20px;
    }
    .footer{
        position:relative;
        padding-top:30px;
        padding-bottom:30px;
    }
    .mx-1024{
        position:relative;
        width:1024px;
        padding-left:16px;
        padding-right:16px;
        margin:0 auto;
        overflow:hidden;
    }
```

### SMACSS

- SMACSS(Scalable and Modular Architecture for CSS)  
   - 기본(base), 레이아웃(layout), 모듈(module), 상태(state), 테마(theme) 다섯가지의 유형으로 분류하도록 권장하는 CSS 아키텍처 방법론

1. 기본(base) : reset.css
```bash
    body,p,h1,h2,h3,h4,h5,h6,ul,ol,li,dl,dt,dd,table,th,td,form,fieldset,legend,input,textarea,button,select{margin:0;padding:0}
    body,input,textarea,select,button,table{font-size:14px;line-height:1.25}
    body{position:relative;background-color:#fff;color:#000}
    img,fieldset{border:0}
    ul,ol{list-style:none}
    table{border-collapse:collapse}
```

2. 레이아웃(layout) : 레이아웃과 관련된 스타일 정의
   - class명에 'l-'을 붙임
```bash
<header class="l-header header"></header>
<section class="l-section section"></section>

.header{
   width:100%;
}
.section{
    width:20%;
    float:right;
}
.l-header .header{
    width:80%;
    margin:0 auto;
}
.l-header .section{
    width:50%;
    float:left;
}
```

3. 모듈(module) : 모듈 관련 스타일
   - 스타일 재 사용을 위해 id와 tagname을 사용하지 않는다.
   - 만약 tagname을 사용해야 한다면 .box > span처럼 child로 사용
```bash
<div class="dotlist">
    <span>리스트</span>
</div>

.dotlist > span{
    padding:10px;

    background:url('image.png');
}
```

4. 상태(state) : hidden / active / hover 
    - class명에 'is-' or 's-' 붙여 사용
```bash
<a href="#" class="btn is-active">버튼</a>
<a href="#" class="btn is-hidden">버튼</a>
<a href="#" class="btn is-disabled">버튼</a>
<a href="#" class="btn is-error">버튼</a>

.btn {
    display: inline-block;
    background:#ddd;
    border-radius:4px;
}
.btn.is-active{
    background:#000;
}
.btn.is-hidden{
    display:none;
}
```

5. 테마(theme) : 사용자가 선택 가능하도록 스타일을 재선언하여 사용

```bash
// main.css
.mod {
	border: 1px solid;
}

// theme.css - main.css 뒤에서 읽도록 적용
.mod {
	border-color:blue
}
```

### BEM(Block Element Modifier)
- block__element--modifier
- 코드를 직관적으로 파악할수 있지만 이름이 길고 복잡해 질수 있다

1. Block : 재사용이 가능한 콘텐츠 영역을 의미함 (만약 네이밍이 길어질 경우 케밥 기법(-)을 이용)
```bash
<div class="login-wrap"></div>
```

2. Element : 블럭 안에 특정 기능을 수행하는 컴포넌트를 말한다. __로 Block 다음 작성
```bash
<div class="login-wrap">
    <div class="login-wrap__header"></div>
</div>
```

3. Modifiers : Block, Element의 외관이나 상태를 변화 시킬 때 사용함 두개의 대쉬 --를 추가하여 표현
```bash
<div class="login-wrap">
    <div class="login-wrap__header">
        <button class="--active"></button>
    </div>
</div>
```

4. 활용예시
```bash

<header class="header">
    <h1 class="header__logo"></h1>
    <nav class="header__navigation">
        <button class="header__navigation--secondary"></button>
    </nav>
</header>

<ul class="card-list">
  <li>
      <div class="card-list__thumb"><img src="" alt=""></div>
      <strong class="card-list__title"></strong>
      <p class="card-list__content"></p>
      <span class="btn-blue"></span>
  </li>
</ul>

<ul class="card-list">
  <li>
      <div class="card-list__thumb"><img src="" alt=""></div>
      <div class="card-list__date"></div>
      <div class="card-list__category"></div>
      <strong class="card-list__title"></strong>
      <p class="card-list__content"></p>
      <div class="profile">
        <img src="" alt="" class="profile__pic">
        <div class="profile__name"></div>
        <div class="profile__position"></div>
      </div>
  </li>
</ul>


<nav>
  <ul class="snb">
    <li class="--active"><a href=""></a></li>
    <li><a href=""></a></li>
    <li><a href=""></a></li>
    <li><a href=""></a></li>
  </ul>
</nav>

```


## Utility-First CSS / Functional CSS

- 위의 3가지 방법론들의 문제점을 극복하기 위한 방법론 위의 방법론들의 문제점
1. css가 html구조와 강하게 결합
2. html에 css가 의존한다.
3. css에 html이 의존한다.
- 전체적으로 inline style과 유사, 일관된 스타일링 가능
- 대표적으로 Tailwind CSS, Tachyons, Atomic CSS


