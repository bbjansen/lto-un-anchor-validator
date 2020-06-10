<template>
  <div id="app">
    <Navbar />
    <main class="content">
        <section class="hero is-primary is-half">
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

<style scoped lang="scss">

.is-half {
  height: 40vh;
}
</style>
