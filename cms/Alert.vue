<template>
  <div v-if="document" :class="{ 'has-edit-button': page.isPreview() }">
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
    message: {
      type: String,
    },
    type: {
      type: String,
    },
    component: {},
    page: {},
  },
  computed: {
    document() {
      const document = this.page.getDocument()

      return document
    },
  },
})
</script>
