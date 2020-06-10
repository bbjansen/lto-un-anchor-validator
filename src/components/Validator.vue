<template>
  <div class="validate">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class Validator extends Vue {
  @Prop() private msg!: string;
}
</script>

<style scoped lang="scss">

</style>
