<template>
  <button @click="onClick">
    <span>
      <span>
        <slot/>
      </span>
    </span>
  </button>
</template>

<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';

  @Component
  export default class NeoSelect extends Vue {
    onClick() {

    }
  }
</script>

<style scoped lang="scss">

</style>
