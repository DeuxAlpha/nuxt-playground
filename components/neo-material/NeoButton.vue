<template>
  <div>
    <slot/>
  </div>
</template>

<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';

  @Component
  export default class NeoButton extends Vue {
  }
</script>

<style scoped lang="scss">

</style>
