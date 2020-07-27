---
title: '[Nuxt.js] Nuxt.js에서 global scss 설정 '
date: 2020-07-28 00:40:00
category: Nuxt.js
draft: false
---

# Nuxt.js에서 global scss 설정
Nuxt.js 프레임워크를 사용해 개발하려고 세팅중에 global scss 변수를 사용하고 싶었습니다.
자주 사용하는 변수들을 한데 모아놓고, 꺼내서 사용하려는데 잘 불러와지지 않아서 그 해결과정을 공유합니다.

```scss
// @/assets/style/base/color.scss
$primary : #00C850;
```

```html
// Color.vue
<template>
	<div class="color">컬러</div>
</template>

<script>
export default {
	name: 'Color',
};
</script>

<style scoped lang="scss">
.color {
	background-color: $primary;
}
</style>
```
<br/>
Nuxt를 실행하면, 에러가 뜹니다. 이를 해결하기 위해 module을 설치해야 합니다.

```bash
npm i --save-dev @nuxtjs/style-resources
yarn add -dev @nuxtjs/style-resources
```

그리고 나서 nuxt.config.js에서 세팅해줍니다.
module.exports 안에 다음 속성을 추가해줍니다.
```js
styleResources: {
		scss: ['@/assets/style/base/color.scss'],
  },
modules: [@nuxtjs/style-resources'],
```
그러면, styleResources안에 들어있는 scss 파일들이 전역으로 적용됩니다!