# Vue Clock
전체화면 하면 이뻐요

크롬 말고 동작되는지 모름

### 실행법
```
$ git clone https://github.com/hw0k/vue-clock
$ npm i
$ npm start
```

### 라이트 모드와 다크 모드 전환
`src/App.vue` 파일을 열어서 여기를 수정해주세요
```js
  data() {
    return {
      blink: false,
      clockText: "00:00:00",
      timerFunc: null,
      dark: false // 여기 true나 false로 바꿔주면 됨
    };
  },
```

### 스샷
라이트 모드

![light](light.png)

다크 모드

![dark](dark.png)