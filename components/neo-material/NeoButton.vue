<template>
  <button class="neo-button-outer" @click="onClick">
    <span class="neo-button-inner">
      <NeoButtonRipple :origin="clickOrigin" :show="state === 'Set'"/>
      <span class="neo-button-text">
        <slot/>
      </span>
      <span class="neo-button-inner-shadow"/>
    </span>
  </button>
</template>

<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';
  import ClickTarget from "~/components/neo-material/models/ClickTarget";
  import NeoButtonRipple from "~/components/neo-material/NeoButtonRipple.vue";

  @Component({
    components: {NeoButtonRipple}
  })
  export default class NeoButton extends Vue {
    state: string = 'Unset';
    clickOrigin: ClickTarget | null = null;

    onClick(event: MouseEvent) {
      this.clickOrigin = new ClickTarget(event.offsetX, event.offsetY);
      switch (this.state) {
        case 'Unset':
          this.state = 'Set';
          break;
        case 'Set':
          this.state = 'Unset';
          break;
        default:
          throw new Error('Argument out of range');
      }
    }
  }
</script>

<style scoped lang="scss">
  button {
    outline: 0;
  }

  .relative {
    position: relative;
  }

  .neo-button-outer {
    padding: 0.5rem;
    background: hsl(0, 0%, 75%);
    box-shadow: -5px -5px 10px hsla(0, 0%, 100%, 0.25), 5px 5px 10px hsla(0, 0%, 0%, 0.25);
    border-radius: 30px;

    .neo-button-inner {
      display: block;
      padding: 0.75rem;
      background: hsl(0, 0%, 75%);
      border-radius: 30px;
      transition: box-shadow .5s;
      position: relative;
    }

    .neo-button-text {
      text-align: center;
      position: relative;
    }

    .neo-button-inner-shadow {
      display: block;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      position: absolute;
      border-radius: 30px;
      transition: box-shadow .5s;
    }

    &:hover {
      .neo-button-inner-shadow {
        box-shadow: inset -5px -5px 10px hsla(0, 0%, 100%, 0.25), inset 5px 5px 10px hsla(0, 0%, 0%, 0.25);
      }
    }
  }
</style>
