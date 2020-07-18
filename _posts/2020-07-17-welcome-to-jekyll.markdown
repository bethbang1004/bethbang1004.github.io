---
layout: post
title:  "Vue JS란 무엇인가요?"
date:   2020-07-17 00:12:51 +0900
categories: VueJS Vue.js 개요
---
# Vue.js 란?
사용자 인터페이스를 만들기 위한 프론트엔드 프레임워크(진보한 프레임워크; Progressive framework)입니다.

# 왜 Vue.js를 사용할까?
Angular, React, VueJS는 최근 프론트엔드 프레임워크로 많이 사용하고 있습니다. 
그 중 Vue JS는 요즘 많은 개발자들이 선택하고 있습니다. 그 이유는 무엇일까요?
- Angluar의 양방향 데이터 바인딩 특성과 React의 단방향 데이터 흐름 모두 가능
- React의 가상돔 렌더링 방식 포함하여 빠른 렌더링 가능
- 성능이 빠르고 우수함

# Vue.js 라이브러리
UI 개발 방식 모델 중 하나인 MVVM 패턴의 뷰 모델(View Model)에 해당하는 화면 라이브러리
![Alt text](/assets/vueArch01.png "MVVM View Model")

위의 그림을 예를 들어 보겠습니다.
사용자가 구글에서 Vue를 검색한다고 생각해볼게요.
사용자가 검색하는 행위는 View에서 동작하며, 이를 읽어들이는 부분은 DOM Listener 입니다.
돔 리스너에서 사용자가 무엇을 검색했는지 Model에서 찾아서 데이터를 바인딩합니다.
그리고 그 결과를 사용자에게 보여주게 됩니다.

- 

```javascript
const Razorpay = require('razorpay');

let rzp = Razorpay({
	key_id: 'KEY_ID',
	secret: 'name'
});

// capture request
rzp.capture(payment_id, cost)
	.then(function (data) {
		return 2;
	})
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
