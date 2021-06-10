<template>
  <div v-if="mapping && id">
    <render-content
      :url="id"
      channel="brxsaas"
      environment="vuestorefront"
      :mapping="mapping"
    />
  </div>
</template>

<script>
import Vue from 'vue'
import { onSSR } from '@vue-storefront/core'
import RenderContent from '~/cms/RenderContent'
import { onMounted, computed } from '@vue/composition-api'
import Alert from '~/cms/Alert'

/*
 * This page is prepared for CMS dynamic content rendering.
 */
export default Vue.extend({
  name: 'CMSDynamicPage',
  components: {
    RenderContent,
  },
  setup(props, { root }) {
    const { $route } = root
    const { id } = $route.params

    return {
      id,
      mapping: {
        VsfAlert: Alert,
      },
    }
  },
})
</script>

<style lang="scss">
.content-block {
  width: 100%;
  margin: 0 auto;
  margin-bottom: var(--spacer-xl);
}
</style>
