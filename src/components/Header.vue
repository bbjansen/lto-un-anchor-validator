<template>
  <div id="header" class="is-half has-background-primary">
    <b-navbar class="is-primary">
        <template slot="brand">
            <b-navbar-item href="https://lto.network">
                <img
                    src="@/assets/img/lto-logo.svg"
                    alt="LTO Network - Hybrid Blockchain"
                >
            </b-navbar-item>
        </template>

        <template slot="end">
            <b-navbar-item href="https://until.un.org">
                <img
                    src="@/assets/img/until-logo.svg"
                    alt="UNTIL - United Nations Technology Innovation Labs"
                >
            </b-navbar-item>
        </template>
    </b-navbar>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Navbar extends Vue {
}
</script>

<style scoped lang="scss">
.is-half {
  height: 40vh;
}
</style>
