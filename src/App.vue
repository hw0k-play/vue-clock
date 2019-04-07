<template>
  <div id="app" :class="dark ? 'dark' : ''">
    <div class="centered" :class="dark ? 'dark' : ''">
      {{ clockText }}
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      blink: false,
      clockText: "00:00:00",
      timerFunc: null,
      dark: true
    };
  },
  created() {
    this.timerFunc = setInterval(() => {
      const date = new Date();
      const clock = {
        h: date.getHours(),
        m: date.getMinutes(),
        s: date.getSeconds()
      };

      if (clock.h < 10) {
        clock.h = "0" + clock.h;
      }
      
      if (clock.m < 10) {
        clock.m = "0" + clock.m;
      }
      
      if (clock.s < 10) {
        clock.s = "0" + clock.s;
      }

      this.blink = !this.blink;
      this.clockText = `${clock.h}${this.blink ? ":" : " "}${clock.m}${this.blink ? ":" : " "}${clock.s}`;
    }, 1000);
  },
  destroyed() {
    clearInterval(this.timerFunc);
    this.timerFunc = null;
  }
};
</script>

<style lang="scss">
  $black: #2c3e50;
  $white: #ecf0f1;

  #app {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 100vh;
    background: $white;
    &.dark {
      background: $black !important;
    }
  }
  .centered {
    display: flex;
    font-size: 14rem;
    text-align: center;
    color: $black;
    &.dark {
      color: $white !important;
    }
  }
</style>
