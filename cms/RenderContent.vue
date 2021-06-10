<template>
  <div v-if="configuration && mapping">
    <br-page :configuration="configuration" :mapping="mapping">
      <template #default>
        <section>
          <br-component component="main" />
        </section>
      </template>
    </br-page>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { BrSdk } from '@bloomreach/vue-sdk'
import axios from 'axios'

Vue.use(BrSdk)

export default Vue.extend({
  name: 'RenderContent',
  props: {
    environment: {
      type: String,
    },
    channel: {
      type: String,
    },
    url: {
      type: String,
    },
    mapping: {
      type: Object,
      required: true,
    },
    page: {
      type: Object,
      required: false,
    },
  },
  computed: {
    configuration() {
      if (!this.environment || !this.channel || !this.url) return null
      return {
        endpoint: `https://${this.environment}.bloomreach.io/delivery/site/v1/channels/${this.channel}/pages/${this.url}`,
        httpClient: axios,
        endpointQueryParameter: 'endpoint',
        path: this.$root.$route.fullPath,
      }
    },
  },
})
</script>
