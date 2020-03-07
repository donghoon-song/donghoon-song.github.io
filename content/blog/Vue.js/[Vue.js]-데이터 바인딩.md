---
title: '[Vue.js] 데이터 바인딩'
date: 2020-03-06 21:34:00
category: Vue.js
draft: false
---

# 데이터 바인딩

데이터 바인딩은 HTML 화면 요소를 뷰 인스턴스의 데이터와 연결하는 것

## {{}} - 콧수염 괄호

### 뷰 인스턴스의 데이터를 HTML 태그에 연결하는 가장 기본적인 텍스트 삽입 방식, 템플릿 문법

- **data의 text 속성이 바뀌면 뷰 반응성에 의해 화면이 자동으로 갱신된다.**

```html
<div id="app">
  {{text}}
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      text: 'Hello World!',
    },
  })
</script>
```

- **뷰 데이터가 변경되어도 값을 유지하고 싶다면 v-once 속성을 사용한다.**

```html
<div id="app" v-once>
  {{ text }}
</div>
```

## v-bind 

# 참고문서

- <a src="http://www.yes24.com/Product/Goods/58206961">Do it! Vue.js 입문</a>
- <a src="https://kr.vuejs.org/v2/api/#updated">Vue.js 공식문서</a>
