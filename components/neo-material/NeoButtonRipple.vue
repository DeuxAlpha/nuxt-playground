<template>
  <transition @enter="OnEnter" @leave="OnLeave">
    <span v-if="show" class="click-target"/>
  </transition>
</template>

<script lang="ts">
  import {Vue, Component, Prop} from 'vue-property-decorator';
  import ClickOrigin from "~/components/neo-material/models/ClickTarget";
  import GSAP from 'gsap';

  @Component
  export default class NeoButtonRipple extends Vue {
    @Prop({type: Object}) readonly origin?: ClickOrigin;
    @Prop({type: Boolean, required: true}) readonly show!: boolean;

    OnEnter(element: HTMLSpanElement, done: Function) {
      if (!this.origin) return;
      console.dir(this.origin);
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
      console.dir(this.origin);
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
</style>
