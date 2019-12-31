<template>
  <button @click="onClick" class="neo-select-outer" :state="state">
    <span class="neo-select-inner">
      <span>
        <slot/>
      </span>
      <span class="neo-select-inner-shadow"/>
    </span>
  </button>
</template>

<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';

  @Component
  export default class NeoSelect extends Vue {
    state: string = 'Unset';

    onClick() {
      switch (this.state) {
        case 'Unset':
          this.state = 'Set';
          break;
        case 'Set':
          this.state = 'Unset';
          break;
        default: throw new Error();
      }
    }
  }
</script>

<style scoped lang="scss">
  button {
    outline: 0;
  }

  .neo-select-outer {
    padding: 0.5rem;
    background: hsl(0, 0%, 75%);
    box-shadow: -5px -5px 10px hsla(0, 0%, 100%, 0.25), 5px 5px 10px hsla(0, 0%, 0%, 0.25);
    border-radius: 30px;
    transition: border-radius .5s;
    &[state="Set"] {
      border-radius: 0;
    }

    .neo-select-inner {
      display: block;
      padding: 0.75rem;
      background: hsl(0, 0%, 75%);
      border-radius: 30px;
      transition: box-shadow .5s;
      position: relative;
    }

    .neo-select-inner-shadow {
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
      .neo-select-inner-shadow {
        box-shadow: inset -5px -5px 10px hsla(0, 0%, 100%, 0.25), inset 5px 5px 10px hsla(0, 0%, 0%, 0.25);
      }
    }
  }
</style>
