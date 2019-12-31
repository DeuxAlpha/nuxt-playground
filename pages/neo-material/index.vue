<template>
  <section class="container flex flex-col">
    <NeoButton>A Button</NeoButton>
    <NeoSelect>A Select</NeoSelect>
  </section>
</template>

<script lang="ts">
  import {Vue, Component} from 'vue-property-decorator';
  import NeoButton from "~/components/neo-material/NeoButton.vue";
  import NeoSelect from "~/components/neo-material/NeoSelect.vue";

  @Component({
    components: {NeoSelect, NeoButton}
  })
  export default class NeoMaterialIndexPage extends Vue {
  }
</script>

<style scoped lang="scss">
  .container {
    margin: 2rem;
  }

  .flex {
    display: flex;
  }

  .flex-col {
    flex-direction: column;
  }
</style>
