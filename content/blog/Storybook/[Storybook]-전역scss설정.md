---
title: '[Storybook] Storybook + 전역 scss 설정'
date: 2020-07-28 00:08:00
category: Storybook
draft: false
---

# Storybook에서 전역 scss파일 불러오기

Storybook을 이용해 디자인 시스템을 만들기 위해 세팅하고 있었습니다.<br/>
주로 쓰일 색상 변수들을 color.scss에 모아두고, @assets/style/base 폴더에 넣어두고 쓰려고 했는데 그냥 불러와지진 않더라구요.

```scss
// @assets/style/base/color.scss
$primary: #00C850;
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
main.js는 다음과 같이 기본 scss 설정만 되어있었습니다.

```js
// ./storybook/main.js
const path = require('path');

// Export a function. Accept the base config as the only param.
module.exports = {
    webpackFinal: async (config, { configType }) => {
        // `configType` has a value of 'DEVELOPMENT' or 'PRODUCTION'
        // You can change the configuration based on that.
        // 'PRODUCTION' is used when building the static version of storybook.

        // Make whatever fine-grained changes you need
        config.module.rules.push({
            test: /\.scss$/,
            use: ['style-loader', 'css-loader', 'sass-loader'],
            include: path.resolve(__dirname, '../'),
        });

        // Return the altered config
        return config;
    },
};
```

```bash
yarn run storybook
```
storybook을 실행하면 다음과 같은 에러가 뜹니다.
![image](https://user-images.githubusercontent.com/32301380/88559627-0490dc00-d068-11ea-88fd-48f01985745a.png)

변수를 찾을 수 없답니다! 그래서 이 친구를 찾게 도와주는 세팅을 해야됩니다.
아까 봤던 ./storybook/main.js을 다음과 같이 수정합니다.
```js
const path = require('path');

// Export a function. Accept the base config as the only param.
module.exports = {
    webpackFinal: async (config, { configType }) => {
        // `configType` has a value of 'DEVELOPMENT' or 'PRODUCTION'
        // You can change the configuration based on that.
        // 'PRODUCTION' is used when building the static version of storybook.

        // Make whatever fine-grained changes you need
        config.module.rules.push({
            test: /\.scss$/,
            use: ['style-loader', 'css-loader', {
                loader: 'sass-loader',
                options: {
                    additionalData: `
						@import "assets/style/base/color.scss";
					`
                }
            }],
            include: path.resolve(__dirname, '../'),
        });

        // Return the altered config
        return config;
    },
};
```
그러고나서 다시 Storybook을 실행하면, 정상적으로 작동합니다! vue파일이 scoped임에도 불구하고, 전역 scss 변수를 사용할 수 있으니, 정말 큰 메리트가 있다고 생각합니다! 이 설정을 적용하지 않는다면, vue파일마다 사용할 변수를 style태그안에 매번 작성해줘야 합니다.

https://webpack.js.org/loaders/sass-loader/#additionaldata
<br/>참고로 우리가 사용한 sass-loader의 options의 additionalData 속성은, sass/scss 파일을 entry file앞에 붙여준다고 합니다.