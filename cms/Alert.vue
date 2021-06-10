<template>
  <div
    v-if="document"
    class="jumbotron mb-3"
    :class="{ 'has-edit-button': true }"
  >
    <br-manage-content-button :content="document" />
    <SfAlert :message="'test'" :type="'info'" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { SfAlert } from '@storefront-ui/vue'

export default Vue.extend({
  name: 'Alert',
  components: {
    SfAlert,
  },
  props: {
    component: {},
    page: {},
  },
  computed: {
    document() {
      const document = this.page.getDocument()

      return document
    },
    data() {
      return this.document?.getData()
    },
  },
})
</script>
