<template>
  <div id="validate">
    <div
      id="welcome"
      class="box validation-box has-text-centered"
      v-if="displayWelcome"
      >
      <h1 class="is-size-3 has-text-secondary has-text-weight-bold">Welcome to the Afghanistan Land Registry portal</h1>

      <p class="welcome-text has-text-primary">
        This tool can be used by the public to verify the authenticity of any documents uploaded and shared by the United Nations utilizing the power of the LTO Network public blockchain.
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

    <div
      id="verified"
      class="box validation-box has-text-centered has-background-verified"
      v-if="displayVerified"
    >
      <p class="verified-icon has-text-white has-text-weight-semibold">
        <b-icon
            icon="check"
            size="is-large"
        >
        </b-icon>
      </p>

      <p class="verified-text has-text-white has-text-weight-semibold">
        Verified
      </p>
    </div>

    <div
      id="unverified"
      class="box validation-box has-text-centered has-background-unverified"
      v-if="displayUnverified"
    >
      <p class="verified-icon has-text-white has-text-weight-semibold">
        <b-icon
            icon="close"
            size="is-large"
        >
        </b-icon>
      </p>

      <p class="verified-text has-text-white has-text-weight-semibold">
        Unverified
      </p>
    </div>

    <div
      id="verifiedDetails"
      class="card validation-card"
      v-if="displayVerifiedDetails"
    >
      <header class="has-background-verified" style="padding:30px;">
        <p class="has-text-centered has-text-white is-uppercase has-text-weight-semibold">
          Verified
        </p>
      </header>

      <div class="card-content">
        <div class="content has-text-centered">
            <p>
                <img src="@/assets/img/view-document.svg" />
            </p>

            <p class="is-size-7 has-text-centered">

              <table>
                <tbody>
                  <tr>
                    <th class="has-text-primary">Filename</th>
                    <th class="has-text-primary">{{ uploadFile.name }}</th>
                  </tr>
                  <tr>
                    <th class="has-text-primary">Signed By</th>
                    <th class="has-text-primary">United Nations</th>
                  </tr>
                 <tr>
                    <th class="has-text-primary">TimeStamp</th>
                    <th class="has-text-primary">{{ formattedDate }}</th>
                  </tr>
                 <tr>
                    <th class="has-text-primary">Filesize</th>
                    <th class="has-text-primary">{{ (uploadFile.size / (1024*1024)).toFixed(2) }} MB</th>
                  </tr>
                </tbody>
              </table>

            </p>

        </div>
      </div>

      <footer class="has-text-centered" style="padding-top: 10px; padding-bottom: 10px;">
        <a href="https://explorer.lto.network" class="has-text-tertiary">View on LTO Network explorer</a>
      </footer>
    </div>

    <div
      id="unverifiedDetails"
      class="card validation-card"
      v-if="displayUnverifiedDetails"
    >
      <header class="has-background-unverified" style="padding:30px;">
        <p class="has-text-centered has-text-white is-uppercase has-text-weight-semibold">
          Unverified
        </p>
      </header>

      <div class="card-content">
        <div class="content has-text-centered">
            <p>
                <img src="@/assets/img/view-document.svg" />
            </p>

            <p class="is-size-7 has-text-centered">

              This file is either not valid or has not been anchored on the LTO Network blockchain. Check if you uploaded the right document and please try again.

            </p>

        </div>
      </div>

      <footer class="has-text-centered" style="padding-top: 10px; padding-bottom: 10px;">
        <a href="/" class="has-text-tertiary">Try Again</a>
      </footer>
    </div>

  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator'
import { sha256 } from 'js-sha256'
import * as bs58 from 'bs58'
import moment from 'moment'
import { EncoderServiceImpl } from '../plugins/encoder'

@Component
export default class Validator extends Vue {
  @Prop() private msg!: string;

  uploadFile = []
  formattedDate = moment()
  displayWelcome = true
  displayUpload = false
  displayLoading = false
  displayVerified = false
  displayUnverified = false
  displayVerifiedDetails = false
  displayUnverifiedDetails = false

  decodedAnchor: Uint8Array = new Uint8Array()
  encoder = new EncoderServiceImpl()

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
      this.formattedDate = moment(file.lastModified).format('YYYY-MM-DD HH:mm:ss')

      console.log(file)

      const reader = new FileReader()

      let hash

      reader.onload = function (e) {
        // console.log(e)

        hash = sha256.digest(e.target.result)
      }

      reader.readAsArrayBuffer(file)

      console.log('encrypted: ' + hash)

      // const base58 = bs58.encode(encrypted)

      // console.log('base58: ' + base58)

      // const fileHash = sha256.digest(file)
      // const fileBase58Hash = bs58.encode(fileHash)

      // console.log(fileBase58Hash)

      this.displayUpload = false
      this.displayVerified = true

      setTimeout(function () {
        this.displayVerified = false
        this.displayVerifiedDetails = true
      }.bind(this), 1000)
    } else {
      this.displayUpload = false
      this.displayUnverified = true

      setTimeout(function () {
        this.displayUnverified = false
        this.displayUnverifiedDetails = true
      }.bind(this), 1000)
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

.validation-card {
  min-height: 40vh;
  margin-top: -20vh;
}

.welcome-text {
  margin-top: 3em;
  margin-bottom: 3em;
}

.verified-text {
  font-size: 30px;
}

.verified-icon {
  font-size: 3em;
  margin-top: 1.8em;
}

</style>
