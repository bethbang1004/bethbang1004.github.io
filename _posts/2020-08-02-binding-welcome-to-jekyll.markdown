---
layout: post
title:  "Vue.js Atom Editor 설치하기"
date:   2020-08-02 21:41:51 +0900
categories: VueJS Atom 설치
---
#### Contents   
[Vue JS란 무엇인가요?](https://bethbang1004.github.io/vuejs/vue.js/%EA%B0%9C%EC%9A%94/2020/07/16/welcome-to-jekyll.html)      
[Vue.js 양방향 데이터 바인딩(Two-way Data Binding)이란 무엇인가요?](https://bethbang1004.github.io/vuejs/vue.js/%EC%96%91%EB%B0%A9%ED%96%A5_%EB%8D%B0%EC%9D%B4%ED%84%B0_%EB%B0%94%EC%9D%B8%EB%94%A9/2020/07/18/binding-welcome-to-jekyll.html)   
* * *

# Vue.js 사용을 위한 Atom 설치   
무료로 사용가능한 Atom Editor를 설치 입니다. (Mac 설치 기준입니다).   

첫번째,      
Chrome 검색창에 Atom을 검색합니다.   
![Alt text](/assets/atom_search.png "atom_검색")   

두번째,   
본인의 OS에 맞는 다운로드를 진행합니다.   


```
<html>
  <head>
    <title>Two-way Data Binding Example</title>
  </head>
  <body>
    <div id="app">
      <h1>Hello, {{ name }}</h1>
      <input type="text" v-model="name"/>
    </div>
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <script>
      new Vue({
        el: '#app',
        data: {
        name: 'Vue.JS'
          }
        });
    </script>
  </body>
</html>

```
최초 결과는 Hello, Vue.JS 가 출력됩니다.   
그리고 사용자는 Input box에 입력을 할 수 있고, 사용자 입력에 따라 출력 결과도 변경됨을 확인 할 수 있습니다.   
![Alt text](/assets/binding_export.gif "two-way data binding example")   

코드를 일일히 정의할 필요없이 v-model 디렉티브로 사용자의 입력값에 따라 바로 적용할 수 있다는 점에서 폼 컨트롤이 정말 유용하겠죠? :)      

#### v-on 디렉티브는 어떨까요?   
