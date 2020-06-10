<template>
  <div id="app">
    <Navbar></Navbar>
    <section class="hero is-primary is-medium">
      <div class="hero-body">
      </div>
    </section>

    <Validator msg=""/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Navbar from './components/Navbar.vue'
import Validator from './components/Validator.vue'

@Component({
  components: {
    Navbar,
    Validator
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {

}
</style>
