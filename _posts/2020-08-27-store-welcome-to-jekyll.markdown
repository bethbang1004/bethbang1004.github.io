---
layout: post
title:  "Vue.js Store 활용하기"
date:   2020-08-27 14:40:51 +0900
categories: VueJS Store data
---

# Vue.js Store 활용하기      
Vue에서 데이터를 주고 받을 때, __부모와 자식 관계로 이루어진 형태가 아닌 컴포넌트인데 데이터를 주고 받게 하고 싶은 경우__, 혹은 __라우터가 서로 달라서 데이터를 주고 받을 수가 없는 경우__ Store를 활용하여 데이터를 저장하고 지정된 값으로 설정할 수 있습니다.   
그럼, 방식을 알아볼까요?            

### 어떤 테스트 페이지를 만들까?   
- 모바일 환경에서 footer에서 특정 버튼 클릭 시 해당 페이지 이동 예시 화면을 만들 예정.     
- 구조   
├── _store   
│   └── index.js   
│   └── getters.js   
│   └── actions.js   
│   └── mutations.js   
│   └── state.js   
├── _layouts   
│   └── _components   
│       └── footer.vue   
├── _views   
│   └── test1.vue   
│   └── test2.vue   
│   └── test3.vue   
│   └── test4.vue   
├── main.js   
├── app.vue      


#### 첫번째,  
store 폴더에 가면, index.js 파일이 있습니다.   
main.js 에 보면 __import store from './store'__ 라는 부분에서 store 전체 파일을 불러오고 있습니다.   
아마 기존에는 index.js에서 getters, mutations, state, actions 를 한 번에 작성하였을텐데,   
저는 추후 관리를 생각하여 파일로 분리 후, index.js에서 불러오는 형태로 구성하는 방식을 소개하겠습니다.      

store쪽에 **actions.js, getters.js, mutations.js, state.js** 파일을 생성합니다.   
파일 생성 방법: store 폴더에서 우클릭 > "New File"   

| File | 의미 |
|---|:---:|---:|
| `index.js` | actions, getters,mutations, state 불러오는 페이지 |
| `actions.js` | state, commit, dispatch, rootstate 사용 가능하며 주로 dispatch를 사용함(서로 다른 action 호출이 가능) |  
| `getters.js` | 특정 state에 대한 계산이 이루어 지며, view도 함께 업데이트됨(state는 원본으로 유지) |  
| `mutations.js` | state를 변경할 수 있음 (state, payload 순으로 commit을 통해 인자를 받을 수 있음) |
| `state.js` | view와 직접적으로 연결되어 있는 model로 mutations에서 변경이 일어나면 view에도 변경이 일어남 (직접 state에서의 변경 불가능) |        

#### 두번째,    
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

#### 세번째,       
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

#### 네번째,   
**actions.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const actions = {
}
export default actions
```

#### 다섯번째,   
**getters.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const getters = {
}
export default actions
```          

#### 여섯번째,   
**mutations.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const mutations = {
}

export default mutations
```   

#### 일곱번째,   
**state.js** 파일에 아래와 같이 내용을 넣어줍니다.   
```
const state = {
}

export default state
```    

### 여덟번째,   
이렇게 하면, 최소 구성이 완료되었습니다!   
이제 화면을 볼 수 있는 테스트 페이지를 만들겠습니다.   



이로써, 설정이 완료되었습니다 :)   
이제 등록할 App에 대한 설정을 시작하시면 됩니다.   
