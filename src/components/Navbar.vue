<template>
    <b-navbar class="is-primary">
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                <img
                    src="@/assets/img/lto-logo.svg"
                    alt="LTO Network - Hybrid Blockchain"
                >
            </b-navbar-item>
        </template>

        <template slot="end">
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                <img
                    src="@/assets/img/until-logo.svg"
                    alt="UNTIL - United Nations Technology Innovation Labs"
                >
            </b-navbar-item>
        </template>
    </b-navbar>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Navbar extends Vue {
}
</script>
