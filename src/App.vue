<template>
  <div id="app" :class="dark ? 'dark' : ''">
    <div class="centered text" :class="dark ? 'dark' : ''">
      {{ clockText }}
    </div>
    <br>
    <button class="centered mt-base btn" :class="dark ? 'dark' : ''" @click="dark = !dark">
      {{ dark ? "Light Mode" : "Dark Mode"}}
    </button>
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
      dark: false
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

  @mixin textColor {
    color: $black;
    &.dark {
      color: $white !important;
    }
  }

  #app {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-flow: column wrap;
    width: 100vw;
    height: 100vh;
    background-color: $white;
    &.dark {
      background-color: $black !important;
    }
  }

  .centered {
    display: flex;
    text-align: center;
  }
  
  .mt-base {
    margin-top: 2rem;
  }

  .text {
    @include textColor;

    font-size: 14rem;
  }

  .btn {
    @include textColor;

    font-size: 4rem;
    background: $white;
    padding: 1rem 2rem;
    border: 2px solid $black;
    border-radius: 0.5rem;
    cursor: pointer;
    &:focus {
      outline: 0;
    }
    &.dark {
      border-color: $white;
      background-color: $black;
    }
  }
</style>
