<template>
  <div id="validate">
    <div
      id="welcome"
      class="box validation-box has-text-centered"
      v-if="displayWelcome"
      >
      <h1 class="is-size-3 has-text-secondary has-text-weight-bold">Welcome to the Afghanistan Land Registry portal</h1>

      <p class="welcome-text has-text-primary">
        This tool is used to lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </p>

      <b-button type="is-tertiary mt-5" expanded  v-on:click="upload">Check Document</b-button>
    </div>

    <div
      id="upload"
      class="box validation-box has-text-centered"
      v-if="displayUpload"
    >
        <b-field>
            <b-upload
              v-model="uploadFile"
              drag-drop
              type="is-info"
              expanded
              :loading="displayLoading"
              required
            >
                <section class="section">
                    <div class="content has-text-centered">
                        <p>
                           <img src="@/assets/img/document.svg" />
                        </p>
                        <p>Drop your document here or click to upload</p>
                    </div>
                </section>
            </b-upload>
        </b-field>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator'

@Component
export default class Validator extends Vue {
  @Prop() private msg!: string;

  uploadFile = []
  displayWelcome = true
  displayUpload = false
  displayLoading = false

  @Watch('uploadFile')
  processFile (file: any) {
    const allowedFormats = [
      'text/plain',
      'application/pdf',
      'application/msword',
      'application/x-abiword',
      'application/vnd.openxmlformats-officedocument.wordprocessingml.document'
    ]

    if (allowedFormats.includes(file.type)) {
      alert(file.name)

      const reader = new FileReader()
      // reader.readAsBinaryString(file[0])
    } else {
      alert('filetype not supported')
    }
  }

  upload () {
    this.displayWelcome = false
    this.displayUpload = true
    this.displayLoading = false
  }
}
</script>

<style scoped lang="scss">

.validation-box {
  min-height: 40vh;
  margin-top: -20vh;
  padding: 50px;
}

.welcome-text {
  margin-top: 3em;
  margin-bottom: 3em;
}
</style>
