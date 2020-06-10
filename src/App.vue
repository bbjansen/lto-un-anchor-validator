<template>
  <div id="app">
    <Navbar />
    <main class="content">
        <section class="hero is-primary is-medium">
          <div class="hero-body">
          </div>
        </section>
        <Validator msg=""/>
    </main>
    <Footer />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Navbar from './components/Navbar.vue'
import Validator from './components/Validator.vue'
import Footer from './components/Footer.vue'

@Component({
  components: {
    Navbar,
    Validator,
    Footer
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
body {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

.content {
  flex: 1;
}
</style>
