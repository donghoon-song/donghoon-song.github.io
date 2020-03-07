---
title: '[Vue.js] 컴포넌트 간 통신'
date: 2020-03-06 20:51:00
category: Vue.js
draft: false
---

# 뷰 컴포넌트 통신

- 컴포넌트로 화면을 구성하므로 같은 웹페이지라도 데이터를 공유할 수 없다.
- 컴포넌트마다 자체적으로 고유한 유효 범위를 가지기 때문

## 상하위 컴포넌트 관계

- 상위(부모) - 하위(자식) 컴포넌트 간의 데이터 전달
- props로 데이터를 전달한다.
- 하위에서 상위로는 기본적으로 이벤트만 전달가능

## 상위에서 하위로 데이터 전달

```javascript
Vue.component('child-component', {
    props: ['propsName],
});
```

- child-component 컴포넌트 태그에 v-bind 속성을 추가한다.

```javascript
<child-component v-bind:propsName="value"></child-component>
```

## 하위에서 상위로 이벤트 전달

### 이벤트 발생과 수신

이벤트를 발생시켜 (event emit) 상위 컴포넌트에 신호를 보낸다.

```javascript
// 이벤트 발생
this.$emit('eventName')
```

```html
// 이벤트 수신
<child-component v-on:eventName="상위 컴포넌트의 메서드명"></child-component>
```

## 관계 없는 컴포넌트간 통신 - 이벤트 버스

### 이벤트 버스는 개발자가 지정한 2개의 컴포넌트 간에 데이터를 주고받을 수 있는 방법

```html
<div id="app">
  <child-component></child-component>
</div>

<script>
  var eventBus = new Vue()
  Vue.component('child-component', {
    template:
      '<div>하위 컴포넌트 영역.<button v-on:click="showLog">show</button></div>',
    methods: {
      showLog: function() {
        eventBus.$emit('triggerEventBus', 100)
      },
    },
  })

  var app = new Vue({
    el: '#app',
    created: function() {
      eventBus.$on('triggerEventBus', function(value) {
        console.log('이벤트를 전달받음. 값: ', value)
      })
    },
  })
</script>
```

- 보내는 컴포넌트에서는 .$emit()을, 받는 컴포넌트에서는 .$on()을 구현한다.
- 애플리케이션 로직을 담는 인스턴스와 별개로 새 인스턴스 1개 더 생성한 후, 그것을 이용해 이벤트를 보내고 받는다.
- **_컴포넌트가 많아지면 데이터의 from과 to를 관리하기 어렵다 => Vuex(상태 관리 도구) 사용_**

# 참고문서

- <a src="http://www.yes24.com/Product/Goods/58206961">Do it! Vue.js 입문</a>
- <a src="https://kr.vuejs.org/v2/api/#updated">Vue.js 공식문서</a>
