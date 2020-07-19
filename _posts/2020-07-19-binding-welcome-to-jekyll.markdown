---
layout: post
title:  "Vue.js 양방향 데이터 바인딩(Two-way Data Binding)이란 무엇인가요?"
date:   2020-07-19 00:12:51 +0900
categories: VueJS Vue.js 양방향_데이터_바인딩
---
***
### 목차
[Vue JS란 무엇인가요?][id1]
[id1]:https://bethbang1004.github.io/vuejs/vue.js/%EA%B0%9C%EC%9A%94/2020/07/16/welcome-to-jekyll.html   
[Vue.js 양방향 데이터 바인딩(Two-way Data Binding)이란 무엇인가요?][id2]
*[id2]:https://bethbang1004.github.io/vuejs/vue.js/%EC%96%91%EB%B0%A9%ED%96%A5_%EB%8D%B0%EC%9D%B4%ED%84%B0_%EB%B0%94%EC%9D%B8%EB%94%A9/2020/07/18/binding-welcome-to-jekyll.html*   
***

우리가 Vue JS를 처음 공부하면서 초반에 공부하던 방식은 단방향 데이터 바인딩 방식일거에요.      
그래서 이번에는 v-model을 사용하여 양방향 데이터 바인딩을 활용해 보겠습니다.   
v-model은 ```<input>, <textarea>, <select>```와 같은 폼에 관련된 태그에서 사용할 수 있습니다.   
그 중 Vue의 input tag로 양방향 데이터 바인딩 예시를 들어볼게요.  

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
