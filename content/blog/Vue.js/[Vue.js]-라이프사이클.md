---
title: [Vue.js] 라이프사이클
date: 2020-03-06 10:51:00
category: Vue.js
draft: false
---

<img src="https://kr.vuejs.org/images/lifecycle.png" alt="Vue.js 라이프사이클">

## beforeCreate

### 인스턴스가 생성되고 나서 가장 처음으로 실행되는 라이프 사이클

- data 속성과 methods 속성 접근 불가
- 돔에도 접근 불가
  > React.js의 constructor과 유사한 거 같습니다.

## created

### beforeCreate 단계 다음에 실행

- data 속성과 methods 속성이 접근 가능
- this.data 또는 this.fetchData()와 같은 로직들을 이용해 data 속성과 methods 속성에 정의된 값에 접근하여 로직 실행가능
- 돔 요소 접근 불가
- Why? **인스턴스가 생성되었지만, 화면요소에 부착되기 전이므로**
- **_서버에 데이터를 요청해 받아오는 로직을 수행하기 좋다._** (vuex에서 actions)
- Why? data 속성과 methods 속성에 접근 가능한 가장 첫 라이프 사이클

> options 속성이나 콜백에 화살표 함수 사용을 지양한다. **화살표 함수들은 부모 컨텍스트에 바인딩**되기 때문에 this 컨텍스트가 Vue 인스턴스를 호출하지 못한다.

## beforeMount

### template 속성에 지정한 마크업 속성을 render() 함수로 변환한 후 el 속성에 지정한 화면 요소에 인스턴스를 부착하기 전 단계

- render() 함수가 호출되기 직전의 로직을 추가하기 좋다.
  > React.js의 componentWillMount()와 유사한 거 같다.

## mounted

### el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 호출되는 단계

- template 속성의 돔 요소에 접근 가능
- 돔에 인스턴스가 부착되자마자 바로 호출되므로 하위 컴포넌트나 외부 라이브러리에 의해 추가된 화면 요소들이 최종 HTML 코드로 변환되는 시점과 다를 수 있다.

## beforeUpdate

### 인스턴스가 부착되고 나면 인스턴스에 정의한 속성들이 화면에 치환된다.

### 치환된 값은 뷰의 반응성(Reactivity)을 제공하기 위해 \$watch 속성으로 감시한다.

- 관찰하고 있는 데이터가 변경되면 가상 돔으로 화면을 다시 그리기 전에 호출되는 단계
- 변경 예정인 새 데이터에 접근할 수 있어 변경 예정 데이터의 값과 관련된 로직을 넣을 수 있다.

> React.js의 componentWillUpdate(nextProps, nextState)와 유사한 거 같다.

## updated

### 데이터가 변경되고 나서 가상 돔으로 다시 화면을 그리고 나면 실행되는 단계

- 데이터 변경으로 인한 화면 요소 변경까지 완료된 시점
- **데이터 변경 후 화면 요소 제어와 관련된 로직을 추가하기 위해 좋음**
- **데이터 값을 갱신하는 로직은 가급적 beforeUpdate에 추가하고, updated에서는 변경 데이터의 화면 요소와 관련되 로직을 추가하는 것이 좋다.**

## beforeDestroy

### 뷰 인스턴스가 파기되기 직전에 호출되는 단계

- 아직 인스턴스에 접근할 수 있다.
- 뷰 인스턴스의 데이터를 삭제하기 좋은 단계
- ex) removeEventListener 호출

```javascript
var app = new Vue({
  el: '#app',
  created() {
    document.body.addEventListener('click', funcion)
  },
  beforeDestroy() {
    document.body.removeEventListener('click', funcion)
  },
})
```

beforeDestoy 단계에서 이벤트를 해제시켜주지 않으면, document.body에는 계속해서 해당 event가 바인딩되어 실행된다.

## destroyed

### 뷰 인스턴스가 파괴되고 나서 호출되는 단계

- 뷰 인스턴스에 정의한 모든 속성이 제거되고 하위에 선언한 인스턴스들 또한 모두 파괴

# 참고문서

- <a src="http://www.yes24.com/Product/Goods/58206961">Do it! Vue.js 입문</a>
- <a src="https://blog.martinwork.co.kr/vuejs/2018/02/05/vue-lifecycle-hooks.html">Vue의 Lifecycle</a>
- <a src="https://kr.vuejs.org/v2/api/#updated">Vue.js 공식문서</a>
