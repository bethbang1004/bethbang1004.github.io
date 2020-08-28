---
layout: post
title:  "Vue.js store 활용하기"
date:   2020-08-27 14:40:51 +0900
categories: VueJS store data
---

# Vue.js store 활용하기      
Vue에서 데이터를 주고 받을 때, __부모와 자식 관계로 이루어진 형태가 아닌 컴포넌트인데 데이터를 주고 받게 하고 싶은 경우__, 혹은 __라우터가 서로 달라서 데이터를 주고 받을 수가 없는 경우__ Store를 활용하여 데이터를 저장하고 지정된 값으로 설정할 수 있습니다.   
그럼, 방식을 알아볼까요?            

### 어떤 테스트 페이지를 만들까?   
*1. 모바일 환경에서 footer에서 특정 버튼 클릭 시 해당 페이지 이동 예시 화면을 만들 예정*      
*2. 구조*   
- _store   
  - index.js   
  - getters.js   
  - actions.js   
  - mutations.js   
  - state.js   
- layouts   
  - _components   
    - footer.vue      
- _views   
  - test1.vue   
  - test2.vue   
  - test3.vue   
  - test4.vue   
- main.js   
- app.vue   

*3. 참고 Github 링크*   
<https://github.com/bethbang1004/store_footer>      


### 첫번째,  
store 폴더에 가면, index.js 파일이 있습니다.   
main.js 에 보면 __import store from './store'__ 라는 부분에서 store 전체 파일을 불러오고 있습니다.   
아마 기존에는 index.js에서 getters, mutations, state, actions 를 한 번에 작성하였을텐데,   
저는 추후 관리를 생각하여 파일로 분리 후, index.js에서 불러오는 형태로 구성하는 방식을 소개하겠습니다.      

store쪽에 **actions.js, getters.js, mutations.js, state.js** 파일을 생성합니다.   
파일 생성 방법: store 폴더에서 우클릭 > "New File"   

| File | 의미 |
|---|:---:|---:|
| `index.js` | actions, getters,mutations, state 불러오는 페이지 |
| `actions.js` | 비동기 작업이 가능하며, state, commit, dispatch, rootstate 사용 가능하며 주로 dispatch를 사용함(서로 다른 action 호출이 가능) |  
| `getters.js` | 특정 state에 대한 계산이 이루어 지며, view도 함께 업데이트됨(state는 원본으로 유지) |  
| `mutations.js` | state를 변경할 수 있음 (state, payload 순으로 commit을 통해 인자를 받을 수 있음) |
| `state.js` | view와 직접적으로 연결되어 있는 model로 mutations에서 변경이 일어나면 view에도 변경이 일어남 (직접 state에서의 변경 불가능) |        

### 두번째 (main.js),    
현재 Vue.js의 상태관리 라이브러리인 vuex를 import 시켰습니다.   
vuex는 중앙 집중식 저장소 역할로, 부모와 자식 관계에 연연하지 않고, 별도의 저장소에서 데이터를 관리합니다.   
오늘 우리는 부모-자식 관계가 아닌 별도 데이터 저장하여 사용할 것이므로, vuex를 설치합니다.   
vuex 설치는 터미널(cmd)에서
`npm install vuex --save`   

main.js에 아래와 같이 추가하여 줍니다.   
```
import Vuex from 'vuex'
Vue.use(Vuex)
new Vue({
  Vuex,
}).$mount('#app')   
```      

### 세번째(store > index.js),       
**index.js** 파일에 아래와 같이 내용을 넣어줍니다.    
```
import Vue from 'vue'
import Vuex from 'vuex'

import state from './state'
import getters from './getters'
import mutations from './mutations'
import actions from './actions'

Vue.use(Vuex)

export default new Vuex.Store({
  getters,
  mutations,
  state,
  actions,
  modules: {
  },
  strict: process.env.NODE_ENV !== 'production'
})
```     

### 네번째(store > actions.js),   
**actions.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const actions = {
}
export default actions
```

### 다섯번째(store > getters.js),   
**getters.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const getters = {
}
export default actions
```          

### 여섯번째(store > mutations.js),   
**mutations.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const mutations = {
}

export default mutations
```   

### 일곱번째(store > state.js),   
**state.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const state = {
}

export default state
```    

### 여덟번째,   
이렇게 하면, store 를 사용할 수 있는 최소 구성이 완료되었습니다!   
이제 화면을 볼 수 있는 테스트 페이지를 만들겠습니다 (github 코드를 참고하시면 됩니다).   
**Path: /src/layouts/components/footer.vue**   
```
<template>
.
.
.
      <div class="locate" @click="test1()" v-if="footerBtnStatus == 0">
        <vs-button class="buttonStyle">test1_on</vs-button>
      </div>
      <div class="locate" @click="test1()" v-if="footerBtnStatus != 0">
        <vs-button color="dark" class="buttonStyle">test1_off</vs-button>
      </div>
      <div class="locate" @click="test2()" v-if="footerBtnStatus == 1">
        <vs-button class="buttonStyle">test2_on</vs-button>
      </div>
      <div class="locate" @click="test2()" v-if="footerBtnStatus != 1">
        <vs-button color="dark" class="buttonStyle">test2_off</vs-button>
      </div>
      <div class="locate" @click="test3()" v-if="footerBtnStatus == 2">
        <vs-button class="buttonStyle">test3_on</vs-button>
      </div>
      <div class="locate" @click="test3()" v-if="footerBtnStatus != 2">
        <vs-button color="dark" class="buttonStyle">test3_off</vs-button>
      </div>
      <div class="locate" @click="test4()" v-if="footerBtnStatus == 3">
        <vs-button class="buttonStyle">test4_on</vs-button>
      </div>
      <div class="locate" @click="test4()" v-if="footerBtnStatus != 3">
        <vs-button color="dark" class="buttonStyle">test4_off</vs-button>
      </div>
.
.
.

<script>
export default {
  computed: {
    footerBtnStatus () {
    }
  },
  methods: {
    test1 () {
    },
    test2 () {
    },
    test3 () {
    },
    test4 () {
    }
  }
}
</script>

.
.
.
```   

#### footer.vue 틀에 대한 간략한 코드리뷰   
페이지에서 사용자에게 보이는 버튼은 총 4개 입니다. 코드 상에서는 버튼의 on, off를 위해 총 8개를 두었습니다.   
푸터에 있는 버튼들의 위치는 고정되며, 특정 버튼을 클릭하면 클릭한 버튼이 가리키는 페이지로 이동할 수 있도록 만들며 해당 버튼은 on, 나머지 버튼은 off 상태로 됩니다.    
사용자에게 보여지는 버튼 4개를 배열로 보면, [0,1,2,3] 입니다.   
footerBtnStatus라고 정의하여 버튼을 왼쪽부터 0 > 1 > 2 > 3 으로 값을 줍니다.   
버튼 상태가 on 인 경우: footerBtnStatus == 0   
버튼 상태가 off인 경우: footerBtnStatus != 0   

그리고 script에서 computed에 footerBtnStatus()를 추가합니다.   

### 아홉번재,   
아래 코드를 추가합니다.   
**Path: /src/store/state.js**   
```  
  footerBtnStatus: 0  
```  

#### state.js 간략한 코드리뷰   
footerBtnStatus의 값을 처음 가져올 값이 0이므로 0으로 셋팅합니다.   


### 열번재,
아래 코드를 추가합니다.   
**Path: /src/store/mutations.js**   
```  
SET_FOOTER_STATUS (state, payload) {
  state.footerBtnStatus = payload
}   
```  

#### mutations.js 간략한 코드리뷰   
SET_FOOTER_STATUS 라는 이름으로 정의하고, state.footerBtnStatus의 값을 payload로 가져옵니다.   

### 열한번째,   
아래 코드로 script 부분을 추가하여 줍니다.   
**Path: /src/layouts/components/footer.vue**   
```    
<script>
export default {
  computed: {
    footerBtnStatus () {
      return this.$store.state.footerBtnStatus
    }
  },
  methods: {
    test1 () {
      this.$store.commit('SET_FOOTER_STATUS', 0)
    },
    test2 () {
      this.$store.commit('SET_FOOTER_STATUS', 1)
    },
    test3 () {
      this.$store.commit('SET_FOOTER_STATUS', 2)
    },
    test4 () {
      this.$store.commit('SET_FOOTER_STATUS', 3)
    }
  }   
```   
#### footer.vue 간략한 코드리뷰(store 추가)   
computed에 정의한 footerBtnStatus()에 store.state 값을 가져옵니다.   
그리고 methods에서 각 버튼(test1, test2 ...)의 클릭 이벤트로 걸어둔 함수에   
this.$store.commit('SET_FOOTER_STATUS', 0) 와 같이 버튼 별 payload 값을 지정하여 줍니다.   

### 열두번째,   
버튼마다 클릭 이벤트(@click)를 넣어두었는데, 클릭하였을 경우, 해당 페이지로 이동하도록 페이지들을 만듭니다.   
**Path: /src/views/**
하위로 test1.vue, test2.vue, test3.vue, test4.vue를 만듭니다.      
- views   
  - test1.vue
  - test2.vue
  - test3.vue
  - test4.vue   

```    
<template>
  <div class="box" style="margin:20px; color:red;">
    test1 페이지 입니다.
  </div>
</template>

<style>
.box{
  width: 300px;
  height: 50px;
  border:1px solid;
  border-color: #fff;
  border-radius: 10px;
  background-color:#f2f2f2;
  text-align:center;
  padding: 15px;
}
</style>   
```    

### 열세번째,   
만든 페이지를 클릭 이벤트로 불러와서 지정된 url로 보이게끔 router 연결이 필요합니다.   
Router 연결은 아래 포스팅 내용을 참고 하여 주세요.   
연결해서 보아야, 현재 store에 대한 프로젝트도 완성이 됩니다.   

이로써, store에 대한 정리는 마무리 되었습니다 :)      
