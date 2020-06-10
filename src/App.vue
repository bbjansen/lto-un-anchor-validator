<template>
  <div id="app">
    <Validator msg="test"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Validator from './components/Validator.vue'

@Component({
  components: {
    Validator
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {

}
</style>
