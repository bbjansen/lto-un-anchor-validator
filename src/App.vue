<template>
  <div id="app">
    <Header />
    <main class="container">
      <div class="columns">
        <div class="column is-half is-offset-one-quarter">
          <Validator msg=""/>
          <p class="is-size-7 has-text-centered" style="margin-top: 10px;">
            <a href="https://lto.network" class="has-text-primary"> Learn more about LTO Network </a>
          </p>
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Header from './components/Header.vue'
import Validator from './components/Validator.vue'
import Footer from './components/Footer.vue'

@Component({
  components: {
    Header,
    Validator,
    Footer
  }
})
export default class App extends Vue {}
</script>
