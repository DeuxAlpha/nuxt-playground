<template>
  <transition @enter="OnEnter" @leave="OnLeave">
    <span v-show="show" class="click-target"/>
  </transition>
</template>

<script lang="ts">
  import {Vue, Component, Prop} from 'vue-property-decorator';
  import ClickOrigin from "~/components/neo-material/models/ClickTarget";
  import GSAP from 'gsap';
  import Color from "color";

  @Component
  export default class NeoButtonRipple extends Vue {
    @Prop({type: Object}) readonly origin?: ClickOrigin;
    @Prop({type: Boolean, required: true}) readonly show!: boolean;

    OnEnter(element: HTMLSpanElement, done: Function) {
      if (element.offsetParent) {
        const backgroundColor = getComputedStyle(element.offsetParent).backgroundColor;
      }
      if (!this.origin) return;
      GSAP.fromTo(element, {
        left: this.origin.x,
        top: this.origin.y
      }, {
        left: 0,
        top: 0,
        width: '100%',
        height: '100%',
        duration: 0.5,
        onComplete: () => done()
      });
    }

    OnLeave(element: HTMLSpanElement, done: Function) {
      if (!this.origin) return;
      GSAP.to(element, {
        left: this.origin.x,
        top: this.origin.y,
        width: 0,
        height: 0,
        duration: 0.5,
        onComplete: () => done()
      });
    }
  }
</script>

<style scoped lang="scss">
  .click-target {
    display: block;
    position: absolute;
    background: hsl(0, 0%, 50%);
    border-radius: 30px;
  }
  .click-target-ripple {
    background: #47a7f5 radial-gradient(circle, transparent 1%, #47a7f5 1%) center/15000%;
    display: block;
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    border-radius: 30px;
  }
</style>
