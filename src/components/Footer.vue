<template>
<footer>
  <div class="content has-text-right is-size-7">
      &copy; 2020 UNTIL &amp; LTO Network
  </div>
</footer>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Navbar extends Vue {
}
</script>

<style scoped lang="scss">
.content {
  margin-top: 20px;
  margin-right: 10px
}
</style>
