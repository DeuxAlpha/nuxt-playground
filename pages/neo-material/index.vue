<template>
  <section>
    <NeoButton>A Button</NeoButton>
  </section>
</template>

<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';
  import NeoButton from "~/components/neo-material/NeoButton.vue";
  @Component({
    components: {NeoButton}
  })
  export default class NeoMaterialIndexPage extends Vue {
  }
</script>

<style scoped lang="scss">

</style>
